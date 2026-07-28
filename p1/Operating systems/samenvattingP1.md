# Linux Operating System Fundamentals Summary

## 1. Introduction to the Shell
* **The Shell:** The program that interprets and executes commands is called the shell . While many exist (sh, csh, zsh), this course uses **bash** (Bourne Again Shell) .
* **Command Structure:** Commands consist of three parts separated by spaces: the command name, options, and arguments .
* **The Prompt:** The command prompt typically displays the username, hostname, and current directory .
    * `$` indicates a normal user .
    * `#` indicates the root user .
* **Remote Access:** **SSH** (Secure Shell) is used to connect to "headless" servers (no monitor/keyboard) .
    * Command: `ssh username@host` .
* **Basic Logic:**
    * `;` runs commands sequentially .
    * `&&` runs the second command only if the first succeeds .
    * `||` runs the second command only if the first fails .

## 2. Getting Help
* **Man Pages:** The `man` command reads documentation from `/usr/share/man` .
    * Section 1: User commands; Section 5: File formats; Section 8: Admin commands .
    * Search: `man -k keyword` searches titles and descriptions (equivalent to `apropos`) .
* **Synopsis:** In help text, `[]` indicates optional arguments and `|` indicates mutually exclusive options .

## 3. The File System and Navigation
* **Structure:** Linux uses a hierarchical structure starting at the root `/`, with no drive letters . Paths are case-sensitive .
* **Key Directories:**
    * `/home`: Regular user data .
    * `/root`: Administrative superuser home .
    * `/etc`: Configuration files .
    * `/var`: Variable data (logs, websites) .
* **Navigation Commands:**
    * `pwd`: Prints the current working directory .
    * `cd`: Changes directory .
    * `ls`: Lists files (`-l` for details, `-a` for hidden files) .
* **Paths:**
    * **Absolute:** Starts from root `/` .
    * **Relative:** Relative to the current directory .
    * `.`: Current directory; `..`: Parent directory .

## 4. File Management
* **Creation:**
    * `mkdir`: Creates directories (`-p` creates parent directories) .
    * `touch`: Creates an empty file or updates timestamps .
* **Deletion:**
    * `rmdir`: Removes *empty* directories .
    * `rm`: Removes files (`-r` for recursive deletion) .
* **Manipulation:**
    * `cp`: Copies files or directories (with `-r`) .
    * `mv`: Moves or renames files .
* **Links:**
    * **Symbolic (Soft) Link (`ln -s`):** Reference to a path; can cross filesystems and link directories .
    * **Hard Link (`ln`):** Direct reference to data on disk; restricted to the same filesystem .

## 5. Shell Expansions
* **Globbing (Wildcards):**
    * `*`: Matches 0 or more characters .
    * `?`: Matches exactly 1 character .
    * `[abc]`: Matches one character from the set .
* **Brace Expansion:** Generates combinations, e.g., `mkdir {a,b,c}` .
* **Command Substitution:** Uses `$(command)` to insert command output .

## 6. Text Processing and Redirection
* **Viewing Files:**
    * `cat`: Views full content .
    * `less` / `more`: Paged viewing .
    * `head` / `tail`: Views the start/end of a file .
    * `wc`: Counts lines (`-l`), words (`-w`), or characters .
* **Redirection:**
    * `>`: Redirects stdout to a file (overwrite) .
    * `>>`: Appends stdout to a file .
    * `2>`: Redirects stderr .
* **Pipelines (`|`):** Passes the output of one command as input to the next .
* **Processing Tools:**
    * `sort`: Sorts text .
    * `uniq`: Removes consecutive duplicates .
    * `cut`: Selects columns .
    * `tr`: Translates or deletes characters .

## 7. Regular Expressions and Editing
* **Grep:** Searches text for patterns .
    * `-i` (case insensitive), `-v` (invert match) .
* **Regex Anchors:** `^` (start of line), `$` (end of line) .
* **Vim Editor:** A modal editor .
    * **Modes:** Command (default), Insert (`i`), Visual (`v`), Extended Command (`:`) .
    * **Saving/Exiting:** `:wq` (save & quit), `:q!` (quit without saving) .

## 8. Environment Variables
* **Usage:** Variables are assigned as `NAME=value` and accessed as `$NAME` .
* **Environment Variables:** System-wide variables usually in uppercase (e.g., `USER`, `HOME`, `SHELL`) .
    * `PATH`: List of directories to search for executables .
* **Export:** The `export` command turns a variable into an environment variable .