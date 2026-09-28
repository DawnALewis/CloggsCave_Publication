### About the Data

Data files
240909_INO_BLlDLeLTaSRaYSo_CloggsCaveResequenceIndoHumanCapDingoShotgun (shotgun and capture)
240308_INO_BLlXRRVPeDLe_TwistCaptureCloggsCaveShotgunLepeChangShotgun (shotgun)
230202_INS_BLlDLe_CloggsCave (Homo sapiens capture only)
221115_INO_VPe_LWe_DLe_BatvirusPeriodontalCHDCLizardCloggs (shotgun)
210816_INvS_KM_CABAHprojects (shotgun and capture)

#Indexes for different library batches
GAII_9 - Human Captures from Env and Mega libraries 
GAII_19 - Marsupial Captures from extracellular  libraries
GAII_18 - Marsupial Captures from extracellular libraries
GAII_20 - Shotgun from Mega Libraries
GAII_9 - Shotgun from Env libraries
GAII_9 - shotgun from 2307 libraries
GAII_8 - shotgun from 2307 libraries
GAII_11 - shotgun from extracellular Libraries

##### 240909_INO_BLlDLeLTaSRaYSo_CloggsCaveResequenceIndoHumanCapDingoShotgun (shotgun and capture)
```
#Untar the files
tar -xvf <file>

#Make SampleSheet.csv
[Header],,,
IEMFileVersion,4,,
Investigator Name,Dawn,,
Experiment Name,CloggsCaveReSeq,,
Date,10/9/2024,,
Workflow,GenerateFASTQ,,
,,,
[Reads],,,
101,,,
101,,,
,,,
[Settings],,,
CreateFastqForIndexReads,1,,
,,,
[Data],,,
Lane,Sample_ID,Sample_Name,I7_Index_ID,index
1,index9,EnvShotgun_EnvCapture_2307Shotgun_resequence,GAII_Indexing_9,ACCAACT
1,index8,2307_shotgun_resequence,GAII_Indexing_8,GCTCGAA
1,index18,MegaMarsupCapture_18,GAII_Indexing_18,TGCGTCC
1,index19,MegaMarsupCapture_19,GAII_Indexing_19,GAATCTC
1,index20,MegaShotgun,GAII_Indexing_20,CATGCTC
1,index11,Mega_ALL_resequence,GAII_Indexing_11,AACTCCG
2,index9,EnvShotgun_EnvCapture_2307Shotgun_resequence,GAII_Indexing_9,ACCAACT
2,index8,2307_shotgun_resequence,GAII_Indexing_8,GCTCGAA
2,index18,MegaMarsupCapture_18,GAII_Indexing_18,TGCGTCC
2,index19,MegaMarsupCapture_19,GAII_Indexing_19,GAATCTC
2,index20,MegaShotgun,GAII_Indexing_20,CATGCTC
2,index11,Mega_ALL_resequence,GAII_Indexing_11,AACTCCG
3,index9,EnvShotgun_EnvCapture_2307Shotgun_resequence,GAII_Indexing_9,ACCAACT
3,index8,2307_shotgun_resequence,GAII_Indexing_8,GCTCGAA
3,index18,MegaMarsupCapture_18,GAII_Indexing_18,TGCGTCC
3,index19,MegaMarsupCapture_19,GAII_Indexing_19,GAATCTC
3,index20,MegaShotgun,GAII_Indexing_20,CATGCTC
3,index11,Mega_ALL_resequence,GAII_Indexing_11,AACTCCG

#Run BCL2fastq2.sh
#!/bin/bash
#SBATCH -p icelake
#SBATCH -N 1
#SBATCH -n 16
#SBATCH --time=06:00:00
#SBATCH --mem=24GB

# Notification configuration
#SBATCH --mail-type=END 
#SBATCH --mail-type=FAIL
#SBATCH --mail-user=a1867445@adelaide.edu.au

module purge
module use /apps/modules/all
module load bcl2fastq2/2.19.1

INDIR=/hpcfs/users/a1867445/240909_INO_BLlDLeLTaSRaYSo_CloggsCaveResequenceIndoHumanCapDingoShotgun
OUTDIR=/gpfs/users/a1867445/240909_INO_BLlDLeLTaSRaYSo_CloggsCaveResequenceIndoHumanCapDingoShotgun/DEMUX/L002/2307_shotgun

bcl2fastq \
--runfolder-dir /hpcfs/groups/acad_users/NGS/240909_INO_BLlDLeLTaSRaYSo_CloggsCaveResequenceIndoHumanCapDingoShotgun/ \
--output-dir /hpcfs/users/a1867445/240909_INO_BLlDLeLTaSRaYSo_CloggsCaveResequenceIndoHumanCapDingoShotgun/ \
--sample-sheet /hpcfs/groups/acad_users/NGS/240909_INO_BLlDLeLTaSRaYSo_CloggsCaveResequenceIndoHumanCapDingoShotgun/SampleSheet_Lanes_2_3_samples.csv \
--ignore-missing-positions \
--ignore-missing-controls \
--ignore-missing-filter \
--ignore-missing-bcls 

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
cd /hpcfs/users/a1867445/240909_INO_BLlDLeLTaSRaYSo_CloggsCaveResequenceIndoHumanCapDingoShotgun/find_index

Performed subset index check on the following files:
2307_shotgun_resequence_S2_L003_R*_001.fastq.gz - OK
Mega_ALL_resequence_S6_L003_R*_001.fastq.gz - ok

 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#####AdapterRemoval
cd /hpcfs/users/a1867445/240909_INO_BLlDLeLTaSRaYSo_CloggsCaveResequenceIndoHumanCapDingoShotgun/

#####adapterRemoval.sh

#!/bin/bash
#SBATCH -p icelake
#SBATCH -N 1
#SBATCH -c 8
#SBATCH --time=04:00:00
#SBATCH --mem=32GB
# Notification configuration
#SBATCH --mail-type=END 
#SBATCH --mail-type=FAIL
#SBATCH --mail-user=@adelaide.edu.au

module purge
module use /apps/modules/all
module load AdapterRemoval/2.2.1-foss-2016b

INDIR=/hpcfs/users/a1867445/240909_INO_BLlDLeLTaSRaYSo_CloggsCaveResequenceIndoHumanCapDingoShotgun
OUTDIR=/gpfs/users/a1867445/240909_INO_BLlDLeLTaSRaYSo_CloggsCaveResequenceIndoHumanCapDingoShotgun/DEMUX/L002/2307_shotgun

AdapterRemoval  --file1 ${INDIR}/2307_shotgun_resequence_S2_L002_R2_001.fastq.gz \
                --file2 ${INDIR}/2307_shotgun_resequence_S2_L002_R2_001.fastq.gz \
                --basename ${OUTDIR}/2307shotgun \
                --barcode-mm 1 \
                --gzip \
                --adapter1 AGATCGGAAGAGCACACGTCTGAACTCCAGTCACNNNNNNATCTCGTATGCCGTCTTCTGCTTG \
                --adapter2 AGATCGGAAGAGCGTCGTGTAGGGAAAGAGTGTAGATCTCGGTGGTCGCCGTATCATT \
                --barcode-list ${INDIR}/SampleSheet.tsv \
                --demultiplex-only \
                --threads 8

```


### Make inputfile_complete.sh

