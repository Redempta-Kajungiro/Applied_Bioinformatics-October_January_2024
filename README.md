#!/bin/bash -l
#SBATCH -A xxxx
#SBATCH -p core
#SBATCH -n 4
#SBATCH -t 02:00:00
#SBATCH -J trimmomatic-job-Cc
#SBATCH --mail-type=ALL
#SBATCH --mail-user xxx
L=$1
SPECIES=Cc
INPUT=/proj/naiss2023-6-185/bioinformatics-project/raw-data/RNA-seq/$SPECIES
OUTPUT=/proj/naiss2023-6-185/bioinformatics-project/analysis/trimmed-data/$SPECIES

module load bioinfo-tools
module load trimmomatic/0.39
trimmomatic PE \
-threads 4 -phred33 \
$INPUT/$1_R1 \
$INPUT/$1_R2 \
-baseout $OUTPUT/$1_trimmed-$SPECIES.fq.gz \
ILLUMINACLIP:/proj/naiss2023-6-185/bioinformatics-project/code/trimmomatic/TrueSeq3-PE.fa:2:30:10:2:true \
LEADING:20 TRAILING:20 SLIDINGWINDOW:5:20 MINLEN:20 \
