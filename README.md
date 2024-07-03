# GL_Dedup_Intern2024
Setting up this repo to create a Gitpod environment for the 2024 GL interns to run UMI-tools, Picard, and RSEM.

### Initiating the GitPod environment

To start a gitpod with the [UMI-tools](https://umi-tools.readthedocs.io/en/latest/reference/dedup.html), [Picard tools](https://broadinstitute.github.io/picard/), and [RSEM](https://deweylab.github.io/RSEM/rsem-calculate-expression.html) installed, add `https://gitpod.io#` to the start of the web address for this repository:
[https://gitpod.io#https://github.com/asaravia-butler/GL_Dedup_Intern2024](https://gitpod.io#https://github.com/asaravia-butler/GL_Dedup_Intern2024)

**Activate each environment as follows:**

UMI-tools:
`source activate umi_tools_v1.1.5`

Picard:
`source activate picard_v3.1.1`

RSEM:
`source activate rsem_v1.3.1`

**Deactivate a conda environment as follows:**

To deactivate:
`conda deactivate`


### Files used for testing deduplication tools

In the terminal of the active GitPod environent, run the following command to download the files to use for deduplication testing:

```bash
curl -LO https://figshare.com/ndownloader/files/47387071 && unzip 47387071 && rm 47387071
```

Both the genome- and transciptome-aligned bam files are in the `Dedup_Test_Files` directory.

*Note: These test files were created by first truncating the RNAseq raw fastq files from sample RRRM1_MG_VIV_LAR_OLD_VL19 in [OSD-511/GLDS-511](https://osdr.nasa.gov/bio/repo/data/studies/OSD-511/4) down to 1M reads. The truncated raw fastq files were then processed through Step 4 of the [GeneLab standard RNAseq processing pipeline](https://github.com/nasa/GeneLab_Data_Processing/blob/master/RNAseq/Pipeline_GL-DPPD-7101_Versions/GL-DPPD-7101-F.md).*


### Files used for quantification with RSEM

After generating the deduplicated BAM files, you can use the RSEM conda environment for quantification. If you are using mouse-derived data files that contain [ERCC spike-ins](https://www.thermofisher.com/order/catalog/product/4456740), run the following command to download the RSEM index files:

```bash
curl -LO https://figshare.com/ndownloader/files/47413399 && unzip 47413399 && rm 47413399
```

The RSEM index files are in the `Mus_musculus.GRCm39.dna.primary_assembly_and_ERCC92` directory and have the prefix `Mmus`.

*Note: These RSEM index files were generated using Step 7 of the [GeneLab standard RNAseq processing pipeline](https://github.com/nasa/GeneLab_Data_Processing/blob/master/RNAseq/Pipeline_GL-DPPD-7101_Versions/GL-DPPD-7101-F.md#7-build-rsem-reference).*

Use the following command to quantitate your deduplicated BAM file following Step 8 of the [GeneLab standard RNAseq processing pipeline](https://github.com/nasa/GeneLab_Data_Processing/blob/master/RNAseq/Pipeline_GL-DPPD-7101_Versions/GL-DPPD-7101-F.md#8a-count-aligned-reads-with-rsem):

First, create an RSEM output directory:

```bash
mkdir RSEM_output
```

Then run the following RSEM command to quantitate: 

```bash
rsem-calculate-expression --alignments \
  --bam \
  --paired-end \ # remove if single-end
  --seed 12345 \
  --seed-length 20 \
  --estimate-rspd \
  --no-bam-output \
  --strandedness reverse|forward|none \ # use the option that is consistent with the strandedness of your data
  deduplicated.bam \ # replace with deduplicated BAM file name
  ./Mus_musculus.GRCm39.dna.primary_assembly_and_ERCC92/Mmus \
  ./RSEM_output/samplename
```


