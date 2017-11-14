## How to get STDOUT and STDERR?
If you want to check stderr and stdout seperately when executing a shell command in python.

### How to do it?
Writing a wrapper on the proc apis will help you to achieve the same. PFB code snippet for the same.

```
import subprocess

def my_shell_exec(cmd):
    #Execute a given shell command and return the STDOUT and STDERR data seperately
    pipe = subprocess.Popen(cmd, stdout=subprocess.PIPE, stderr=subprocess.PIPE, shell=True)
    stdout, stderr = pipe.communicate()
    return stdout, stderr


//Execute the delete command
cmd = "rm arun.txt"
print "Executing command : "+cmd
stdout, stderr = my_shell_exec(cmd)

stderr = stderr.strip('\n')

print "stdout = "+stdout
print "stderr = "+stderr

if stderr != None and stderr != '':
  print "STD ERROR!"

```
