# Useful Snippets
Some useful scripting snippets in Bash/Python.


# Use Cases


**Convert Bash seperated values to a literal array/list string** 

The example is using space separated values but the separator could be anything.

```
args="1 2 apple orange arg1 arg2"
sepArgs=`echo -n '['; for arg in ${args}; do case "$arg" in +([0-9]) ) echo -n "${arg}, " ;;+([-a-zA-Z0-9_]) ) echo -n "\"${arg}\", " ;; esac; done`
echo "${sepArgs:0:-2}]"
```

The output would be like this:

`[1, 2, "apple", "orange", "arg1", "arg2"]`

Now the above array/list is a BASH text value. You will need to convert that text into the appropriate data type in your PL.

Now assuming that the above snippet was put into a file called "to_list.sh", we could just execute the script from Python to get the output and evaluate it into an actual Python list, which brings us to the next use case.

**Convert Bash literal array/list string into a Python list** 

Iterating on the previous use case, we could just simply call the Bash script from our python script like this:

```
try:
        output = subprocess.check_output(bashCommand)
	l = ast.literal_eval(output)
except Exception as e:
        error = str(e)

if l:
	print(l, l[0])
```
