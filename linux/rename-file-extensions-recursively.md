# Recursive Renaming of File Extensions in Linux

In Linux, you can use the `find` command to recursively rename file extensions. This is particularly useful when you need to change the extensions of multiple files in a directory and its subdirectories.

Here's an example of how you can do this:

```shell
find . -iname "*.oldext" -exec bash -c 'mv "$1" "${1%.oldext}".newext' - {} \;
```

Let's break down this command:

- ```find . -iname "*.oldext"```: This part of the command finds all files in the current directory (and its subdirectories) with the extension `.oldext`. The `-iname` option makes the search case insensitive.

- `-exec bash -c 'mv "$1" "${1%.oldext}".newext' - {} \;`: This part of the command executes a bash command for each file found. The `mv` command is used to rename the files. The `${1%.oldext}` part removes the `.oldext` extension from the file name, and `.newext` appends the new extension.

Remember to replace `.oldext` with the current extension of your files and `.newext` with the new extension you want to give your files.

Note: Be careful when running this command, as it will immediately rename all matching files. It's a good idea to first run the `find` command alone to check that it's finding the correct files.
