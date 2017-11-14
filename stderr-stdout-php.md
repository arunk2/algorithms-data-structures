## How to get STDOUT and STDERR in SHELL_EXEC php?
If you want to check stderr and stdout seperately when executing a shell command in php.
Typicall **exec()** or **shell_exec()** wont give you both the outputs.

### Code samples:

```
$result = exec("rm arun.txt");
```
or
```
$result = shell_exec("rm arun.txt");
```
cannot identify stdout and stderr seperately.


### How to do it?
Writing a wrapper on the proc apis will help you to achieve the same. PFB code snippet for the same.

```

//Execute a given shell command and return the STDOUT and STDERR data seperately
function my_shell_exec($cmd, &$stdout=null, &$stderr=null) {
		
		$proc = proc_open($cmd,[
				1 => ['pipe','w'],
				2 => ['pipe','w'],
				],$pipes);
		$stdout = stream_get_contents($pipes[1]);
		fclose($pipes[1]);
		$stderr = stream_get_contents($pipes[2]);
		fclose($pipes[2]);
		return proc_close($proc);
    
}

//Execute the delete command
$cmd = "rm arun.txt";
echo "Executing command : ".$cmd;
$result = my_shell_exec($cmd, $stdout, $stderr);
echo "\nResult = ".$result;
echo "\nstdout = ".$stdout;
echo "\nstderr = ".$stderr;
if ($stderr != null) {
  echo "STD ERROR!";
}

```
