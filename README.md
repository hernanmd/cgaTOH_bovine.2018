# cgaTOH_bovine.2018

ROH Bovine Analysis and Post-Analysis using cgaTOH and R 

# Requirements

  - Download and install:
    - [cgaTOH](http://www.cs.kent.edu/~zhao/TOH/) to your working directory. 
      - Place the cgaTOH executable file under your working directory. Example: /c/Users/MyUsername/Documents/my_working_dir
      - If you cannot download the software, contact me by e-mail.
    - [GitBash](http://www.techoism.com/how-to-install-git-bash-on-windows/)
    - [PLINK](https://www.youtube.com/watch?v=I62fp9HB0kg&feature=youtu.be)

# Input Files Preparation

  - Open a GitBash console.
  - cd to the directory where you placed the cgaTOH executable file (my_working_dir): ``` cd /c/Users/MyUsername/Documents/my_working_dir ```
  - ``` git clone https://github.com/hernanmd/cgaTOH_bovine.2018.git ```
  - ``` cd cgaTOH_bovine.2018/src ```
  - You must have the following input files:
    - A CSV file with run parameters. See SNP_Het_Mis.txt for a sample table. This table will be splitted during execution using always the two first columns and incrementing by two the following ones: First run take columns 1,2,3,4. Second run take columns 1,2,5,6. Third run: 1,2,7,8...etc.
    - Create a directory to place your .PED/.MAP files as subdirectory of my_working_dir: ``` mkdir pedmaps ``` 
    - Put your .PED/.MAP or multiple .PED/.MAP files into the new directory
    - Each PED/MAP pair matches one chromosome. These files can be produced from PLINK and --chr parameter: ``` for c in $(seq 1 29); do plink --file my_input --out my_input_chr$c --chr $c --recode tab --cow; done```

## Script parameters
  
  - You should check and adjust the following parameters in the script:
    - k = Number of iterations (script defaults to 1000000) = Maximum tree depth for binary clustering.
    - maxChr = Number of chromosomes in your organism.
    - globalInputFile = Name of the CSV file with run parameters (SNP_Het_Mis.txt)
    - n = Minimum SNP overlap, default is 10.
    - max_gap = Maximum physical gap between adjacent SNPs, if not given physical gaps won't be considered
    - min_length = Minimum physical length of a TOH run, if not given physical length won't be considered
  - You should check and adjust the following parameters in the CSV file (SNP_Het_Mis.txt)
    - max_missing = "Third" column in each generated table from each run = Maximum missing SNPs allowed in a TOH run, if none give n then any number will be allowed
    - max_hetero = "Fourth" column in each generated table from each run = Maximum heterozygous SNPs allowed in a TOH run, if none given then none will be allowed
    - l = Second column = TOH length, default is 100

# Usage

  - You will have to run two scripts.
    - First script executes a loop with the cgaTOH software with a set of input files.
      - The loop executes for each chromosome, run another loop with the parameters in a parameter file (see below).
    - Second script parses the cgaTOH output.
    
 ## Run cgaTOH script
 
  - Run the script:

```bash
bash
. ./run_cgaTOH_adjusted.sh
```

## Output

  - Depending on your parameters in the CSV file (SNP_Het_Mis.txt), the output could generate hundreds of files.
    - Output files are timestamped, so different runs will never overwrite existing output files.
  - The output files should be used as input files to extract the ROH valuable information such as how many ROHs were found.
  
## Run the parse output script



