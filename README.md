These are hg38 event level annotations for use with MISO, from Crossmap.

# How these were made

```bash
source activate miso
conda install -c bioconda crossmap
```

## Get hg19 annotations

```bash
mkdir -p hg19
cd hg19
wget http://genes.mit.edu/burgelab/miso/annotations/ver2/miso_annotations_hg19_v2.zip
unzip miso_annotations_hg19_v2.zip
cd ..
```

## Get hg19->hg38 chain file

```bash
mkdir -p crossmap
cd crossmap
wget http://hgdownload.soe.ucsc.edu/goldenPath/hg19/liftOver/hg19ToHg38.over.chain.gz
```


```bash
mkdir -p hg38
for file in hg19/*.gff3
do
  event=`basename ${file} .hg19.gff3`
  echo "Processing ${file} as event ${event}."
  CrossMap.py gff crossmap/hg19ToHg38.over.chain.gz ${file} hg38/${event}.hg38.gff3
done
```
