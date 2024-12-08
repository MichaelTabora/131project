# BioE C131 Final Project: Filovirus
## 1. Load and process test data
### 1.1. Download and process Filoviridae family genomes
When adding the genomes into Jbrowse 2, we will refer to the Jbrowse 2 root directory. For Linux installation, the folder should be `/var/www/jbrowse2` or `/var/www/html/jbrowse2`. For macOS, the folder should be `/opt/homebrew/var/www/jbrowse2` (for M1) or `/usr/local/var/www/jbrowse2` (for Intel).

```
export APACHE_ROOT='/path/to/rootdir'
```

First, create a temporary working directory as a staging area to load the genomes into JBrowse 2. You can use any folder you want and it does not have to be in the `APACHE_ROOT` directory, but moving forward we are assuming you created a `temp` folder.

```
mkdir temp
```
```
cd temp
```

Make sure you are in the temporary folder you created, then download the genomes for the different species of the Filoviridae family including Cuevavirus, Dianlovirus, Marburg, Ebola, and Sudan species in fasta format and load them into JBrowse 2.

#### Cuevavirus

```
wget "https://www.ncbi.nlm.nih.gov/sviewer/viewer.fcgi?id=OQ630505.1&db=nuccore&report=fasta&extrafeat=null&fmt_mask=0&retmode=fasta&withmarkup=on&tool=portal&log$=seqview" -O cuevavirus.fasta
mv cuevavirus.fasta cuevavirus.fa
samtools faidx cuevavirus.fa
jbrowse add-assembly cuevavirus.fa --out $APACHE_ROOT/jbrowse2 --load copy
```

#### Dianlovirus

```
wget "https://www.ncbi.nlm.nih.gov/sviewer/viewer.fcgi?id=NC_055510.1&db=nuccore&report=fasta&extrafeat=null&fmt_mask=0&retmode=fasta&withmarkup=on&tool=portal&log$=seqview" -O dianlovirus.fasta
mv dianlovirus.fasta dianlovirus.fa
samtools faidx dianlovirus.fa
jbrowse add-assembly dianlovirus.fa --out $APACHE_ROOT/jbrowse2 --load copy
```

#### Marburg

```
wget "https://www.ncbi.nlm.nih.gov/sviewer/viewer.fcgi?id=DQ217792.2&db=nuccore&report=fasta&extrafeat=null&fmt_mask=0&retmode=fasta&withmarkup=on&tool=portal&log$=seqview" -O marburg.fasta
mv marburg.fasta marburg.fa
samtools faidx marburg.fa
jbrowse add-assembly marburg.fa --out $APACHE_ROOT/jbrowse2 --load copy
```

#### Ebola

```
wget "https://www.ncbi.nlm.nih.gov/sviewer/viewer.fcgi?id=KY786027.1&db=nuccore&report=fasta&extrafeat=null&fmt_mask=0&retmode=fasta&withmarkup=on&tool=portal&log$=seqview" -O ebola.fasta
mv ebola.fasta ebola.fa
samtools faidx ebola.fa
jbrowse add-assembly ebola.fa --out $APACHE_ROOT/jbrowse2 --load copy
```

#### Sudan

```
wget "https://www.ncbi.nlm.nih.gov/sviewer/viewer.fcgi?id=FJ968794.1&db=nuccore&report=fasta&retmode=text" -O sudan.fasta
mv sudan.fasta sudan.fa
samtools faidx sudan.fa
jbrowse add-assembly sudan.fa --out $APACHE_ROOT/jbrowse2 --load copy
```


### 1.2. Download and process genome annotations

Download the genome annotations in the GFF3 format from the Github repo. Make sure the GFF3 files are in the temporary folder. Then, use jbrowse to sort the annotations, compress the GFF with bgzip, and index with tabix. Once you sort the annotations, load the annotation tracks into jbrowse.

#### Cuevavirus annotations

```
jbrowse sort-gff cuevavirus.gff3 > cuevavirus_sorted.gff
bgzip cuevavirus_sorted.gff
tabix cuevavirus_sorted.gff.gz
jbrowse add-track cuevavirus_sorted.gff.gz --out $APACHE_ROOT/jbrowse2 --load copy --assemblyNames cuevavirus
```

#### Dianlovirus annotations

```
jbrowse sort-gff dianlovirus.gff3 > dianlovirus_sorted.gff
bgzip dianlovirus_sorted.gff
tabix dianlovirus_sorted.gff.gz
jbrowse add-track dianlovirus_sorted.gff.gz --out $APACHE_ROOT/jbrowse2 --load copy --assemblyNames dianlovirus
```

#### Marburg annotations

```
jbrowse sort-gff marburg.gff3 > marburg_sorted.gff
bgzip marburg_sorted.gff
tabix marburg_sorted.gff.gz
jbrowse add-track marburg_sorted.gff.gz --out $APACHE_ROOT/jbrowse2 --load copy --assemblyNames marburg
```

#### Ebola annotations

```
jbrowse sort-gff ebola.gff3 > ebola_sorted.gff
bgzip ebola_sorted.gff
tabix ebola_sorted.gff.gz
jbrowse add-track ebola_sorted.gff.gz --out $APACHE_ROOT/jbrowse2 --load copy --assemblyNames ebola
```

#### Sudan annotations

```
jbrowse sort-gff sudan.gff3 > sudan_sorted.gff
bgzip sudan_sorted.gff
tabix sudan_sorted.gff.gz
jbrowse add-track sudan_sorted.gff.gz --out $APACHE_ROOT/jbrowse2 --load copy --assemblyNames sudan
```

### 1.3. Download and process Zaire and Marburg variants

#### Zaire Ebola virus strain Mayinga 1

```
export FASTA_ROOT="https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?db=nuccore&id=AF272001.1&report=fasta"
wget -O Zaire_Ebola_virus_strain_Mayinga_1.fa $FASTA_ROOT
samtools faidx Zaire_Ebola_virus_strain_Mayinga_1.fa
jbrowse add-assembly Zaire_Ebola_virus_strain_Mayinga_1.fa --out $APACHE_ROOT/jbrowse2 --load copy
```

#### Zaire Ebola virus strain Mayinga 2

```
export FASTA_ROOT="https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?db=nuccore&id=AF499101.1&report=fasta"
wget -O Zaire_Ebola_virus_strain_Mayinga_2.fa $FASTA_ROOT
samtools faidx Zaire_Ebola_virus_strain_Mayinga_2.fa
jbrowse add-assembly Zaire_Ebola_virus_strain_Mayinga_2.fa --out $APACHE_ROOT/jbrowse2 --load copy
```

#### Marburgvirus strain guinea pig lethal variant

```
export FASTA_ROOT="https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?db=nuccore&id=AY430365.1&report=fasta"
wget -O Marburg_guinea_pig_lethal_variant.fa $FASTA_ROOT
samtools faidx Marburg_guinea_pig_lethal_variant.fa
jbrowse add-assembly Marburg_guinea_pig_lethal_variant.fa --out $APACHE_ROOT/jbrowse2 --load copy
```


#### Marburgvirus strain guinea pig nonlethal variant

```
export FASTA_ROOT="https://www.ncbi.nlm.nih.gov/sviewer/viewer.cgi?db=nuccore&id=AY430366.1&report=fasta"
wget -O Marburg_guinea_pig_nonlethal_variant.fa $FASTA_ROOT
samtools faidx Marburg_guinea_pig_nonlethal_variant.fa
jbrowse add-assembly Marburg_guinea_pig_nonlethal_variant.fa --out $APACHE_ROOT/jbrowse2 --load copy
```

### 1.4. Variant annotations
Again, download the variant genome annotations in the GFF3 format from the Github repo and make sure you are downloading them into your temporary folder.

#### Zaire Ebola virus strain Mayinga 1 annotations

```
jbrowse sort-gff Zaire_Ebola_virus_strain_Mayinga_1.gff3 > Zaire_Ebola_virus_strain_Mayinga_1_sorted.gff
bgzip Zaire_Ebola_virus_strain_Mayinga_1_sorted.gff
tabix Zaire_Ebola_virus_strain_Mayinga_1_sorted.gff.gz
jbrowse add-track Zaire_Ebola_virus_strain_Mayinga_1_sorted.gff.gz --out $APACHE_ROOT/jbrowse2 --load copy --assemblyNames Zaire_Ebola_virus_strain_Mayinga_1
```

#### Zaire Ebola virus strain Mayinga 2 annotations

```
jbrowse sort-gff Zaire_Ebola_virus_strain_Mayinga_2.gff3 > Zaire_Ebola_virus_strain_Mayinga_2_sorted.gff
bgzip Zaire_Ebola_virus_strain_Mayinga_2_sorted.gff
tabix Zaire_Ebola_virus_strain_Mayinga_2_sorted.gff.gz
jbrowse add-track Zaire_Ebola_virus_strain_Mayinga_2_sorted.gff.gz --out $APACHE_ROOT/jbrowse2 --load copy --assemblyNames Zaire_Ebola_virus_strain_Mayinga_2
```

#### Marburgvirus strain guinea pig lethal variant annotations

```
jbrowse sort-gff Marburg_guinea_pig_lethal_variant.gff3 > Marburg_guinea_pig_lethal_variant_sorted.gff
bgzip Marburg_guinea_pig_lethal_variant_sorted.gff
tabix Marburg_guinea_pig_lethal_variant_sorted.gff.gz
jbrowse add-track Marburg_guinea_pig_lethal_variant_sorted.gff.gz --out $APACHE_ROOT/jbrowse2 --load copy --assemblyNames Marburg_guinea_pig_lethal_variant
```

#### Marburgvirus strain guinea pig nonlethal variant annotations

```
jbrowse sort-gff Marburg_guinea_pig_nonlethal_variant.gff3 > Marburg_guinea_pig_nonlethal_variant_sorted.gff
bgzip Marburg_guinea_pig_nonlethal_variant_sorted.gff
tabix Marburg_guinea_pig_nonlethal_variant_sorted.gff.gz
jbrowse add-track Marburg_guinea_pig_nonlethal_variant_sorted.gff.gz --out $APACHE_ROOT/jbrowse2 --load copy --assemblyNames Marburg_guinea_pig_nonlethal_variant
```

### 1.5. Index for search-by-gene

Run the “jbrowse text-index” command to allow users to search by gene name within JBrowse 2.

In the temporary work directory, run the following command.

```
jbrowse text-index --out $APACHE_ROOT/jbrowse2
```

### 1.6. Download Protein3d plugin

We will index into the jbrowse2 directory and edit the config.json file directly from the terminal.

```
cd $APACHE_ROOT/jbrowse2
nano config.json
```

Copy and paste the lines below at the very top of the file.

```
"plugins": [
  {
    "name": "Protein3d",
    "url": "https://unpkg.com/jbrowse-plugin-protein3d/dist/jbrowse-plugin-protein3d.umd.production.min.js"
  }
],
```

The copy and pasted text should look like this in the config.json file.
![alt text](protein3d.png "Protein3d")

Save file by Ctrl+O, Enter to write, Ctrl+X to exit. Then, restart the server.

For linux,
```
sudo systemctl restart apache2
```

For macOS,
```
brew services restart httpd
```

