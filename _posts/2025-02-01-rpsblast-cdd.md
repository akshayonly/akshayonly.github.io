---
title: NCBI Conserved Domain Database (CDD) and Setup on Google Colab
layout: article
mode: immersive
header:
  theme: dark
article_header:
  type: cover
  image:
    src: assets/postimages/130124/img_01.jpg
tags: bioinformatics CDD RPS-BLAST MSA
---

## **Introduction**
The **NCBI Conserved Domain Database (CDD)** is a collection of annotated multiple sequence alignments representing protein domain families. It is widely used in **bioinformatics** to identify functional and evolutionary relationships in proteins.

One of the most efficient ways to analyze **conserved domains** in proteins is through **RPS-BLAST (Reverse Position-Specific BLAST)**. In this guide, we will **set up and run RPS-BLAST with CDD on Google Colab**.

---

## **Why Use CDD?**
- Identifies **functional protein domains** in sequences.
- Helps in **annotating proteins** with domain structures.
- Supports **comparative genomics** and **phylogenetic studies**.

---

## **Setting Up CDD on Google Colab**
Google Colab provides a cloud-based **Linux environment**, making it easy to install and run **RPS-BLAST with CDD**.

### **1. Create Required Directories**
```bash
!mkdir -p /content/ncbi
!mkdir -p /content/cdd
!mkdir -p /content/query
```
This step ensures that:
- **BLAST executables** are stored in `/content/ncbi`
- **CDD database files** are stored in `/content/cdd`
- **Query sequences** are saved in `/content/query`

---

### **2. Install RPS-BLAST**
Download and install **NCBI BLAST+**, which includes `rpsblast`:
```bash
!wget https://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/ncbi-blast-2.16.0+-x64-linux.tar.gz
!tar -xvzf ncbi-blast-2.16.0+-x64-linux.tar.gz -C /content/ncbi --strip-components=1
```

Add BLAST to the system path:
```python
import os
os.environ["PATH"] += ":/content/ncbi/bin"
```

Check if **RPS-BLAST** is installed:
```bash
!rpsblast -version
```

---

### **3. Download the CDD Database**
CDD contains domain alignments used for RPS-BLAST searches. Download and extract the **CDD database**:
```bash
!wget https://ftp.ncbi.nlm.nih.gov/pub/mmdb/cdd/little_endian/Cdd_LE.tar.gz
!tar -xvzf Cdd_LE.tar.gz -C /content/cdd
```

---

### **4. Install `rpsbproc` for Processing Results**
The `rpsbproc` tool is used to **interpret and format RPS-BLAST results**.

```bash
!wget https://ftp.ncbi.nih.gov/pub/mmdb/cdd/rpsbproc/RpsbProc-x64-linux.tar.gz
!tar -xvzf RpsbProc-x64-linux.tar.gz -C /content/ncbi/bin
!chmod +x /content/ncbi/bin/RpsbProc-x64-linux/rpsbproc
```

Confirm the installation:
```bash
!/content/ncbi/bin/RpsbProc-x64-linux/rpsbproc -help
```

---

### **5. Prepare a Protein Query Sequence**
Create a **FASTA file** with a sample protein sequence:
```python
query_fasta = """>example_protein
MAVQGPELFVRLVKPDVDYLGAGGELFDSLGKTVVKVGRGAIMPYMGAGAHTYFSNYPMFYDE
"""

with open("/content/query/protein.fasta", "w") as file:
    file.write(query_fasta)
```

---

### **6. Run RPS-BLAST**
Now, run **RPS-BLAST** using the CDD database:
```bash
!rpsblast -query /content/query/protein.fasta -db /content/cdd/Cdd -out /content/query/output.asn -outfmt 11
```

---

### **7. Process Results with `rpsbproc`**
Format the output for easier interpretation:
```bash
!/content/ncbi/bin/RpsbProc-x64-linux/rpsbproc -i /content/query/output.asn -o /content/query/output.txt
!cat /content/query/output.txt
```

This will display the **conserved domain annotations** found in the query protein.

---

## **Conclusion**
Setting up **RPS-BLAST with CDD on Google Colab** is straightforward and enables powerful **protein domain analysis**. This approach is especially useful for **biologists and bioinformaticians** working with **functional annotations and evolutionary studies**.

By following these steps, you can quickly **analyze conserved domains in protein sequences** without requiring a local installation.
