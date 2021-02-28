# MHC subset for HPRC year 1

First, we map to the MHC ALT haps from GRCh38:

```
wfmash -t 48 -s 5000 -p 98 MHC.fa /lizardfs/erikg/HPRC/year1/parts/chr6.pan+refs.fa >HPRCy1.chr6.pan+refs_vs_MHC.paf
```

Then, we make a BED file for the mappings:

```
awk '{ print $1, $3, $4 }' HPRCy1.chr6.pan+refs_vs_MHC.paf | tr ' ' '\t' | sort -V >HPRCy1.MHC.bed
```

And merge the regions in it to make a single BED record per matching contig:

```
bedtools merge -d 1000000 -i HPRCy1.MHC.bed >HPRCy1.MHC.merge.bed
```

Finally, extracting the FASTA file for the regions:

```
bedtools getfasta -fi /lizardfs/erikg/HPRC/year1/parts/chr6.pan+refs.fa -bed HPRCy1.MHC.merge.bed >HPRCy1.MHC.fa
```

## access

The resulting file has been gzipped and posted publicly: http://hypervolu.me/~erik/HPRC/MHC/HPRCy1.MHC.fa.gz
