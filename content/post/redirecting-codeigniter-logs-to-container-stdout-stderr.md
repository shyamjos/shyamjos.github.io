---
date: 2021-01-20
title: "Redirecting CodeIgniter logs to container's STDOUT and STDERR"
tags: [ "container", "logging"]
---
As part of migrating applications from EC2 instance to kubernetes I was assigned with a task of containerizing a CodeIgniter application. once the application was containerized I noticed that the application logs were writing to a local file inside the container. so I thought this can be easily fixed by changing the logging path in CodeIgniter config file to `php://stdout`. 

But it was not that easy!! 

![logging](/assets/img/logs/giphy.webp)

strangely the log path config in CodeIgniter is a combination of file path + file extension, so if I set the file path as `php://stdout` and left the file extension part blank, the application will throw an error `'Use a full server path with trailing slash'`.

After some digging on google. I found out that there is no easy way to set custom static log path in CodeIgniter and I also found an [open feature request](https://github.com/bcit-ci/CodeIgniter/issues/5648) for this issue which is not yet implemented by CodeIgniter team :(

Luckily I was able to fix the issue by modifying CodeIgniter logging module which is located at `system/core/Log.php`, I am not sure if this is an optimal solution , just in-case if you are stuck with similar issue give it a try! 

Firstly I removed the file path and file extension check conditions from below code block (`system/core/Log.php`)

```
public function __construct()
	{
		$config =& get_config();

		$this->_log_path = ($config['log_path'] !== '') ? $config['log_path'] : APPPATH.'logs/';
		$this->_file_ext = (isset($config['log_file_extension']) && $config['log_file_extension'] !== '')
			? ltrim($config['log_file_extension'], '.') : 'php';

		file_exists($this->_log_path) OR mkdir($this->_log_path, 0755, TRUE);

		if ( ! is_dir($this->_log_path) OR ! is_really_writable($this->_log_path))
		{
			$this->_enabled = FALSE;
		}

		if (is_numeric($config['log_threshold']))
		{
			$this->_threshold = (int) $config['log_threshold'];
		}
		elseif (is_array($config['log_threshold']))
		{
			$this->_threshold = 0;
			$this->_threshold_array = array_flip($config['log_threshold']);
		}

		if ( ! empty($config['log_date_format']))
		{
			$this->_date_fmt = $config['log_date_format'];
		}

		if ( ! empty($config['log_file_permissions']) && is_int($config['log_file_permissions']))
		{
			$this->_file_permissions = $config['log_file_permissions'];
		}
	}
```
This is how the code block looks after removing all the checks

```
	public function __construct()
	{
		$config =& get_config();

			$this->_enabled = TRUE;
	}
```	

Now you need to replace below line 

```
$filepath = $this->_log_path.'log-'.date('Y-m-d').'.'.$this->_file_ext;
```
with this line (use a static file path instead of a dynamic one)

```
$filepath = $this->_log_path;
```
Now find and remove the below block code from the file (used for changing permission of log file, not needed in our case)

```
		if (isset($newfile) && $newfile === TRUE)
		{
			chmod($filepath, $this->_file_permissions);
		}
```		

And finally make changes to the CodeIgniter main config file (`application/config/config.php`) as below

```
/*
|--------------------------------------------------------------------------
| Error Logging Threshold
|--------------------------------------------------------------------------
|
| You can enable error logging by setting a threshold over zero. The
| threshold determines what gets logged. Threshold options are:
|
|	0 = Disables logging, Error logging TURNED OFF
|	1 = Error Messages (including PHP errors)
|	2 = Debug Messages
|	3 = Informational Messages
|	4 = All Messages
|
| You can also pass an array with threshold levels to show individual error types
|
| 	array(2) = Debug Messages, without Error Messages
|
| For a live site you'll usually only enable Errors (1) to be logged otherwise
| your log files will fill up very fast.
|
*/
$config['log_threshold'] = 4;

/*
|--------------------------------------------------------------------------
| Error Logging Directory Path
|--------------------------------------------------------------------------
|
| Leave this BLANK unless you would like to set something other than the default
| application/logs/ directory. Use a full server path with trailing slash.
|
*/
$config['log_path'] = 'php://stdout';

/*
|--------------------------------------------------------------------------
| Log File Extension
|--------------------------------------------------------------------------
|
| The default filename extension for log files. The default 'php' allows for
| protecting the log files via basic scripting, when they are to be stored
| under a publicly accessible directory.
|
| Note: Leaving it blank will default to 'php'.
|
*/
$config['log_file_extension'] = '';

/*
|--------------------------------------------------------------------------
| Log File Permissions
|--------------------------------------------------------------------------
|
| The file system permissions to be applied on newly created log files.
|
| IMPORTANT: This MUST be an integer (no quotes) and you MUST use octal
|            integer notation (i.e. 0700, 0644, etc.)
*/
$config['log_file_permissions'] = '';

/*
|--------------------------------------------------------------------------
| Date Format for Logs
|--------------------------------------------------------------------------
|
| Each item that is logged has an associated date. You can use PHP date
| codes to set your own date formatting
|
*/
$config['log_date_format'] = '';

/*
|--------------------------------------------------------------------------
| Error Views Directory Path
|--------------------------------------------------------------------------
|
| Leave this BLANK unless you would like to set something other than the default
| application/views/errors/ directory.  Use a full server path with trailing slash.
|
*/
$config['error_views_path'] = '';

```

Once these changes are deployed you will be able to the see the application logs in container's STDOUT and STDERR logs (docker/kubernetes logs).

