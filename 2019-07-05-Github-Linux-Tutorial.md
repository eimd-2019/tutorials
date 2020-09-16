# Github and Linux tutorial

In this tutorial, students will practice basic `bash` commands while setting up a Github repository. Students should join the [EMID 2019 organization](github.com/eimd-2019) and download [Github Desktop](desktop.github.com) before starting this tutorial. [ExplainShell](explainshell.com) is a good resource to keep open while working through the tutorial!

1. Clone [this repository](https://github.com/eimd-2019/tutorials) to your personal Desktop.
2. Open Terminal and type `echo hello world :) `
3. Explore directory structure.
	- Use `pwd` to identify the present working directory.
	- To see what files and subdirectories exist in the present working directory, use `ls`. Adding the argument `-F` to `ls` (*e.g.* `ls -F`) will allow you to differentiate bewteen subdirectories and files.
	- To change the present working directory, use `cd`. Practice moving down the directory structure with `cd` and up directory structure with `cd` and `..` (hint: use `ls` or `ls ..` to look at directory structure before changing working directories).
	- It is best practice to use tab-complete while typing folder or file names instead of typing names out manually. Tab-complete expedites coding and prevents careless errors. If you are unsure what files or folders can be called in a certain command, press tab twice. The Terminal will list your options.
4. Download FASTA files [from this folder](https://gannet.fish.washington.edu/spartina/2019-07-05-eimd/).
	- Create a folder with your name using `mkdir`.
	- Change your working directory to the folder you just created with `cd`.
	- `curl` a FASTA file and save it in the present working directory (ex. `curl https://gannet.fish.washington.edu/spartina/2019-07-05-eimd/Colleen.fasta > Colleen.fasta`).
		- When downloading files, it helps you keep track of a file's origin within your code if you do not change the name of the file as you're downloading it.
		- This `curl` command will not work when attempting to download multiple files at once. For that, use `wget`.
		- The redirect (`>`) is used to take the output and save it somewhere else instead of printing it to the Terminal screen.
	- Download a second FASTA file from the same folder and save it in the present working directory.
5. Move files to a new directory and remove undesired files.
	- Create a `data` subdirectory within the current working directory with `mkdir`.
	- Move both FASTA files to the `data` directory with `mv`(ex. `mv *fasta data/.`). Use `cd` to change the working directory to the `data` subdirectory.
		-  What commands would you use to change the working directory to `data` first, then move the files?
	- Remove one of the FASTA files using `rm`. It is highly recommended to use the `-i` argument to ensure you do not permanently remove files you did not mean to remove (ex. `rm -i Colleen.fasta`).
6. Explore the contents of the remaining FASTA file.
	- Use `head` to look at the first few lines of the FASTA file (ex. `head Colleen.fasta`). Use the `-n` argument to set the number of lines you would like to look at (ex. `head -n3 Colleen.fasta`).
	- Use `tail` to look at the last few lines of the FASTA file. `tail` and `head` have the same command syntax.
	- Count the number of lines, words, and characters (bytes) in the file.
		- `wc Colleen.fasta` provides the line, word, and character count in the output.
		- `wc -l Colleen.fasta` only counts the number of lines.
		- `wc -w Colleen.fasta` only counts the number of words.
		- `wc -c Colleen.fasta` only counts the number of characters.
7. Specify and count character strings (patterns) of interest.
	- Use `grep` to obtain lines with a pattern of interest (ex. `grep "A" Colleen.fasta`).
	- Use `fgrep` to obtain all instances of a pattern of interest within the FASTA file (ex. `fgrep -o -i ATCG Colleen.fasta`).
		- By default, `grep` prints lines that contain a pattern of interest. `fgrep -o` will print instances of the pattern within the file. `-i` ignores case differences when matching patterns.
		- How does the content and structure of the `fgrep` output differ from that of the `grep` output?
		- How would you redirect the `fgrep` output to a new file (hint: `>`)?
		- After redirecting the `fgrep` output to a new file, count the number of instances the pattern of interest was found in the FASTA file. What command would you use for this (hint: Use `wc`. Do you need to specify anthing else)?
	- Use a pipe (`|`) to take the output from `fgrep` and use it in another command, `wc`. How can you use `|` to count the number of matching patterns from  `fgrep`?
	- Test this the efficacy of the `-i` argument for yourself. What commands would you use for this (hint: use two commands with `|`)?
