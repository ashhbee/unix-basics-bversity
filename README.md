# STCC Course Documentation -- Unix Basics for Bioinformatics

## Objective

The objective of this repository is to learn, practice, and document Unix command-line skills introduced during the STCC course, particularly in the context of bioinformatics data handling and workflow execution.

This repository serves as:

* A structured learning record of commands and concepts practiced during the course
* A reference guide for handling biological data using Unix-based tools
* A demonstration of proper documentation and reproducible computational practices

## Tools and Environment

- **Operating System:** Linux (via WSL)
- **Shell:** Bash
- **Version Control:** Git and GitHub
- **Data Types Used:** FASTA, FASTQ, GTF, BED, TSV, CSV, TXT
- **Editor:** Terminal-based tools

## Why Unix is Essential for Bioinformatics

Modern biological research generates large-scale sequencing data (often several GBs).  
Unix provides:

- Efficient handling of large files through streaming
- Powerful text-processing utilities
- Automation via command chaining
- Reproducibility through scripting and version control

Unix is therefore a foundational skill for any bioinformatician.

## Reproducible and Robust Research

### Reproducible Research

Reproducibility ensures that the same data and methods produce the same results.

Best practices include:

- Sharing code and datasets
- Recording software versions and parameters
- Proper project planning
- Maintaining detailed documentation (README files)

### Robust Research

Robust research focuses on error prevention and reliability, especially in computational workflows where errors may be silent.

Key principles:

- Write readable and modular code
- Use consistent file naming conventions
- Automate repetitive tasks
- Test scripts wherever possible
- Treat raw data as read-only
- Develop frequently used scripts into reusable tools

A README file acts as the **computational equivalent of a wet-lab notebook**.

## Unix File System Navigation

```bash
pwd      # Display current working directory
ls       # List files and directories
ls -l    # Detailed listing
cd data/ # Move into a directory
cd ..    # Move one directory up
```

**Key Notes:**

- Unix is case-sensitive
- Absolute paths start with `/`
- Relative paths depend on the current directory

## File and Directory Management

### Creating Files and Directories

```bash
mkdir test-project
touch sample.txt
```

### Writing and Viewing Files

```bash
echo "Hello World" > sample.txt
echo "Hello India" >> sample.txt
cat sample.txt
```

- `>` overwrites a file
- `>>` appends to an existing file

### Copying and Moving Files

```bash
cp demo_1/sample.txt -t demo_2
mv demo_2/sample.txt test/
mv test old_test  # Rename directory
```

### Deleting Files and Directories

```bash
rmdir empty_dir
rm file.txt
rm -rf project_dir
```

**Warning:** Unix deletions are permanent (no recycle bin).

## Getting Help and Command History

```bash
man ls
history
```

- `man` provides the official documentation for commands
- `history` shows previously executed commands

## Shell Expansion and File Subsetting

### Brace Expansion

```bash
echo languages-{python,r,rust}
touch sample{A,B,C}_R{1,2}.fastq
```

### Wildcards and Ranges

```bash
ls sampleA*
ls sample[AB]_R1.fastq
ls sample[A-C]_R2.fastq
```

These techniques are widely used when handling multiple sequencing files.

## Streaming, Redirection, and Pipes

### Streaming Large Files

```bash
cat tb1.fasta
less Mus_musculus.GRCm38.75.gtf
```

Streaming allows files to be processed **without loading them entirely into memory**.

### Output Redirection

```bash
cat file1.fasta file2.fasta > combined.fasta
echo "New entry" >> combined.fasta
```

### Handling Errors

```bash
cat valid.fasta invalid.fasta > output.fasta 2> error.log
```

### Pipes

```bash
grep -v "^>" tga1-protein.fasta | grep --color "[^GPSTVEF]"
```

This pipeline:

1. Removes FASTA headers
2. Highlights unexpected amino acids

## Pattern Matching Using grep

The `grep` command is used to search for specific patterns inside files. It is widely used in bioinformatics for searching gene names, sequence motifs, and filtering annotation files.

### Example Commands

```bash
grep "GENE1" genes.txt
grep -c "^>" sequences.fasta
grep -o "ATG" sequence.fasta
grep -v "^#" annotation.gtf

## Counting with wc

```bash
wc file.txt
wc -l file.txt
wc -w file.txt
wc -m file.txt
```

### FASTQ Read Count

```bash
wc -l reads.fastq
# Number of reads = total lines / 4
```

## Working with Tabular and Genomic Files

### cut - Column Extraction

```bash
cut -f1 genes.tsv
cut -f2,3 random.bed
```

### Sorting and Uniqueness

```bash
sort genes.txt
sort genes.txt | uniq
sort genes.txt | uniq -c
```

Sorting by columns:

```bash
sort -k1,1 file.txt
sort -k2,2n file.txt
```

## FASTA and FASTQ File Handling

### FASTA

```bash
grep "^>" sequences.fasta
grep -c "^>" sequences.fasta
```

### FASTQ Structure

Each FASTQ entry has **4 lines**:

1. Header (@)
2. Sequence
3. Separator (+)
4. Quality scores

```bash
head reads.fastq
sed -n '2~4p' reads.fastq
```

## Version Control with Git and GitHub

### Git Configuration

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

### SSH Key Setup

```bash
ssh-keygen -t rsa -b 4096 -C "your@email.com"
cat ~/.ssh/id_rsa.pub
```

**Warning:** Never share `id_rsa` (private key).

### Basic Git Workflow

```bash
git init
git status
git add README.md
git commit -m "Initial commit"
git log
```

### Undoing Changes

```bash
git restore file.txt
git restore --staged file.txt
git rm -f file.txt
git mv old.txt new.txt
```

### Ignoring Files

```bash
touch .gitignore
echo "*.fastq" >> .gitignore
git add .gitignore
git commit -m "Add gitignore"
```

### Connecting to GitHub

```bash
git remote add origin <repo-url>
git branch -M main
git push origin main
git pull origin main
```

## Key Learnings

- Unix enables efficient handling of large biological datasets
- Streaming avoids memory overload
- Pipes allow modular data processing
- Proper documentation ensures reproducibility
- Git preserves project history and enables collaboration

## Conclusion

This repository serves as documentation of Unix command-line skills and bioinformatics data handling concepts learned during the STCC course. The commands and workflows demonstrated here were practiced using publicly available datasets and standard Unix tools.

The content reflects course-based learning and hands-on exercises and is intended as structured learning documentation rather than a research project.

## Repository Information

- **Course:** STCC -- Unix Basics for Bioinformatics
- **Student:** Ashish Balan S
- **Institution:** Bversity School of Biosciences
- **Purpose:** Academic submission and learning documentation