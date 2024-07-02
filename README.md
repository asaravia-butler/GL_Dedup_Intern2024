# GL_Dedup_Intern2024
Setting up this repo to create a Gitpod environment for the 2024 GL interns to run UMI-tools and Picard.

### Files used for testing deduplication tools

To start a gitpod with the UMI-tools and Picard tools installed, add `https://gitpod.io#` to the start of the web address for this repository:
[https://gitpod.io#https://github.com/asaravia-butler/GL_Dedup_Intern2024](https://gitpod.io#https://github.com/asaravia-butler/GL_Dedup_Intern2024)

Then run the following command to download the files to use for deduplication testing:

```bash
curl -LO https://figshare.com/ndownloader/files/47387071 && unzip 47387071 && rm 47387071
```

Both the genome- and transciptome-aligned bam files are in the `Dedup_Test_Files` directory.

*Note: These test files were created by first truncating the RNAseq raw fastq files from sample RRRM1_MG_VIV_LAR_OLD_VL19 in [OSD-511/GLDS-511](https://osdr.nasa.gov/bio/repo/data/studies/OSD-511/4) down to 1M reads. The truncated raw fastq files were then processed through Step 4 of the [GeneLab standard RNAseq processing pipeline](https://github.com/nasa/GeneLab_Data_Processing/blob/master/RNAseq/Pipeline_GL-DPPD-7101_Versions/GL-DPPD-7101-F.md).*
