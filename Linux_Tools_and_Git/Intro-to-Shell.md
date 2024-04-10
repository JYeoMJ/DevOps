# Bash Command Cheatsheet

## Environment Variables

- `HOME`: User's home directory (e.g., `/home/repl`)
- `PWD`: Present working directory (same as `pwd` command)
- `SHELL`: Which shell program is being used (e.g., `/bin/bash`)
- `USER`: User's ID (e.g., `repl`)

## Shell Commands

- `pwd`: Print current working directory
- `ls`: List directories
  - `ls ~`: List contents of home directory
  - `ls -R`: List everything underneath directory (recursive)
- `cd`: Change directory
  - `cd ..`: Move up one directory
  - `cd ~`: Move to home directory
- `touch`: Create a new file
- `cp`: Copy file (provide existing file and destination file paths, overwrites if exists)
- `mv`: Move file (can also be used to rename files, overwrites if exists)
- `rm`: Remove (delete) files
- `rmdir`: Remove directories (only works when directory is empty)
- `mkdir`: Make directory
- `cat`: Print file content
- `less`: Page print file content (view piece by piece for large files)
  - Spacebar: Page down
  - `q`: Quit
  - `:n`: Move to next file (when viewing multiple files)
  - `:p`: Go back to previous file
- `head`: Print top 10 lines of a file
  - `-n`: Command-line flag to control number of lines (use before filename)
- `cut`: Select columns from a file
  - `-f`: Fields (to specify columns)
  - `-d`: Delimiter (to specify separator)
- `man <cmd>`: Get help for command `<cmd>`
- `history`: Print list of recently run commands
  - `!<n>`: Run the `<n>`th command in history
  - `!<cmd>`: Re-run most recent use of `<cmd>`
  - `!!`: Run the last command
- `grep`: Find in files
- `paste`: Merge lines of files
- `wc`: Word count (print number of characters, words, and lines in a file)
  - `-c`: Print number of characters
  - `-w`: Print number of words
  - `-l`: Print number of lines
- `sort`: Sort lines of text
  - `-n`: Sort numerically
  - `-r`: Reverse order
  - `-b`: Ignore leading blanks
  - `-f`: Case insensitive
- `uniq`: Remove duplicate lines (use with `sort`)
- `^C` (Ctrl + C): Terminate running program
- `echo $foo`: Print variable `foo`
- `nano`: Nano text editor (open filename for editing)

## Defining and Printing Shell Variables

To define a shell variable, use `=` (without any spaces):
```bash
training=seasonal/summer.csv
```

To print a shell variable, remember to use the `$` sign:
```bash
echo $training
```

## For Loops

```bash
for filename in seasonal/*.csv; do echo $filename; done
```

```bash
for file in seasonal/*.csv; do grep 2017-07 $file | tail -n 1; done
```

## Nano Text Editor Commands

- Ctrl + K: Delete a line
- Ctrl + U: Un-delete a line
- Ctrl + O: Save the file ('O' stands for 'output'). You will also need to press Enter to confirm the filename!
- Ctrl + X: Exit the editor

## Shell Scripts (`.sh` files)

To run a shell script (where `foo.sh` contains a set of shell commands):
```bash
bash foo.sh
```

Example: Shell replaces `$@` with each file to sort, then pipes to `uniq`:
```bash
bash unique-lines.sh seasonal/*.csv
```
(where `unique-lines.sh` contains: `sort $@ | uniq`)

Example: Substitutes second parameter "1" into `$2`, first parameter "filename" into `$1`:
```bash
bash column.sh seasonal/autumn.csv 1
```
(where `column.sh` contains: `cut -d , -f $2 $1`)

## `grep` Flags for Pattern Recognition

- `-c`: Print a count of matching lines (instead of lines themselves)
- `-h`: Do not print the names of files when searching multiple files
- `-i`: Ignore case
- `-l`: Print names of files that contain the matches, not the matches
- `-n`: Print line numbers for matching lines
- `-v`: Invert the match (show only lines that do not match)

## Wildcards

- `*`: Match zero or more characters
- `?`: Match a single character (e.g., `201?.txt` matches `2017.txt` or `2018.txt`)
- `[...]`: Match any characters inside the square brackets
- `{...}`: Match any comma-separated patterns inside (e.g., `{*.txt, *.csv}` for any `.txt` or `.csv` file)

## Additional Notes and Examples

- Concept of relative vs. absolute path (identifying file directories)
- `cd` for navigating down to subdirectories
- `..` as a special path for the parent directory
- `.` as a special path for the current directory
- `~` as a special path for the home directory

```bash
cp seasonal/summer.csv backup/summer.bck   # Make a copy of seasonal/summer.csv in the backup directory, name the file copy summer.bck
cp seasonal/spring.csv seasonal/summer.csv backup   # Copy two files from the seasonal directory into the backup directory
mv seasonal/spring.csv seasonal/summer.csv backup   # Move two files from the seasonal directory to the backup directory
cd /tmp   # Move into the temp folder (where intermediate files are stored)
```

- Concept of tab completion in the shell (start typing, then press Tab to autocomplete)
- `ls -R -F /home/repl`: Print everything underneath the directory with paths
- `cut -f 2-5,8 -d , values.csv`: Select columns 2 through 5 and 8, using comma as the separator
  - Note: It is good practice (style) to put all flags before other values
- Concept of redirection `>` to save any command's outputs wherever you want
  - `tail -n 5 seasonal/winter.csv > last.csv`
- Pipe symbol for shell `|` used to combine commands
  - `head -n 3 seasonal/s*`: Wildcard to get first 3 lines from both `spring.csv` and `summer.csv`
  - `history | tail -n 3 > steps.txt`: Record last 3 commands, redirect output to `steps.txt`
