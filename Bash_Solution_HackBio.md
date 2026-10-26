# My cuent working directory
# /home/prathamesh_bobale/hackbio/bash_course/biocomputing_task

# 1. Printing my name
my_name="Prathamesh K. Bobale"
echo "$my_name"

# 2. Creating folder titled in my name
mkdir prathamesh_k_bobale

# 3. Creating another directory with new title and changing the current working directory  new on
mkdir biocomputing && cd biocomputing

# 4. Downloading files from the given links
wget https://raw.githubusercontent.com/HackBio-Internship/Bash_NGS_Starters/refs/heads/main/biocomp_samp/wildtype.fna
https://raw.githubusercontent.com/HackBio-Internship/Bash_NGS_Starters/refs/heads/main/biocomp_samp/wildtype.gbk
https://raw.githubusercontent.com/HackBio-Internship/Bash_NGS_Starters/refs/heads/main/biocomp_samp/wildtype.gbk
# files are downloaded within the current working directory, to check 
ls -lh  # using listing command to list the working directory contents


# 5. Moving the designated file '.fna' to another directory, from current working directory
mv wildtype.fna ../prathamesh_k_bobale/

# 6. Deleting the duplicate 'gbk' file
	# using fdupes command
	fdupes -d .
	# selecting the files to be kept and deleting the rest
	# other option
	cmp -s wildtype.gbk wildtype.gbk.1 && rm -i wildtype.gbk.1

# 7. Confirm if the .fna file is mutant or wild type (tatatata vs tata)
# creating a bash script to execute the task
touch mutant.sh
# using nano editor to write the below script
# !/bin/bash
if grep -qi 'tatatata' ../prathamesh_k_bobale/wildtype.fna; then
    echo "Mutant sequence detected"
elif grep -qi 'tata' ../prathamesh_k_bobale/wildtype.fna; then
    echo "Wild-type motif detected"
else
    echo "Neither specified motif was detected"
fi
# file execution 
bash mutant.sh

# 8. Printing matching lines to new file 
if grep -qi 'tatatata' ../prathamesh_k_bobale/wildtype.fna; then
    grep -i 'tatatata' ../prathamesh_k_bobale/wildtype.fna > mutant.fna
fi

# 9. Count number of lines (excluding header) in the .gbk file
awk '!/^LOCUS/' wildtype.gbk | wc -l

# 10. Print the sequence length of the .gbk file. (Use the LOCUS tag in the first line)
awk '/^LOCUS/ { print $3, $4 }' wildtype.gbk

# 11. Print the source organism of the .gbk file. (Use the SOURCE tag in the first line)
awk '/SOURCE/ { print $2, $3 }' wildtype.gbk

# 12. List all the gene names of the .gbk file. Hint {grep '/gene='}
grep '/gene=' wildtype.gbk | sed -E 's/.*\/gene="([^"]+)".*/\1/' | sort -u

# 13. Clear your terminal space and print all commands used today
	# to clear space
	clear
	# other option - press Ctrl + L
	
	# to print all the commands used
	history 


# 14. List the files in the two folders
ls -lh ../biocomputing ../prathamesh_k_bobale

