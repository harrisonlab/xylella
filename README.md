## Xylella fastidiosa genomics README ##

# First built a xylella genus prokka database 
# Downloaded all sequences associated with complete xylella genomes (32 in total) In /home/hulinm/xylella/annotation
# Download puts all sequences into one big file. Need to split into seperate genomes
# Split by "//" into separate files and then remove any files that have blank space in their first line  

awk -v n=1 '/^\/\//{close("out"n);n++;next} {print > "out"n}' complete_genomes.gb 

find -type f | xargs sed -i -e '2,$b' -e '/^$/d' 


# rename each file as its accession number 

for file in out* ; do
accession=$(head -1 $file | tr -s ' ' | cut  -d " " -f2)
echo $accession
mv $file "$accession".gbk
done


# Create a database for prokka 
prokka-genbank_to_fasta_db *gbk > ps.faa
cd-hit -i xf.faa -o xf -T 0 -M 0 -g 1 -s 0.8 -c 0.9
rm -fv xf.faa xf.bak.clstr xf.clstr
makeblastdb -dbtype prot -in xf
mv xf.p* /home/hulinm/local/src/prokka/db/genus/



# Downloaded complete set of X.fa genomes available on NCBI (29.03/18, 43 genomes)
# 2 additional non-fastidiosa strains taiwanensis strain and UBA6001 also downloaded from ncbi directly  

wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/006/725/GCA_000006725.1_ASM672v1/GCA_000006725.1_ASM672v1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/007/245/GCA_000007245.1_ASM724v1/GCA_000007245.1_ASM724v1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/019/325/GCA_000019325.1_ASM1932v1/GCA_000019325.1_ASM1932v1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/019/765/GCA_000019765.1_ASM1976v1/GCA_000019765.1_ASM1976v1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/148/405/GCA_000148405.1_ASM14840v1/GCA_000148405.1_ASM14840v1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/698/805/GCA_000698805.1_ASM69880v1/GCA_000698805.1_ASM69880v1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/698/825/GCA_000698825.1_ASM69882v1/GCA_000698825.1_ASM69882v1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/001/456/195/GCA_001456195.1_ASM145619v1/GCA_001456195.1_ASM145619v1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/001/456/235/GCA_001456235.1_ASM145623v1/GCA_001456235.1_ASM145623v1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/001/456/275/GCA_001456275.1_ASM145627v1/GCA_001456275.1_ASM145627v1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/001/456/295/GCA_001456295.1_ASM145629v1/GCA_001456295.1_ASM145629v1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/001/456/315/GCA_001456315.1_ASM145631v1/GCA_001456315.1_ASM145631v1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/001/456/335/GCA_001456335.2_ASM145633v2/GCA_001456335.2_ASM145633v2_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/002/117/875/GCA_002117875.1_ASM211787v1/GCA_002117875.1_ASM211787v1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/002/954/185/GCA_002954185.1_ASM295418v1/GCA_002954185.1_ASM295418v1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/002/954/205/GCA_002954205.1_ASM295420v1/GCA_002954205.1_ASM295420v1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/428/665/GCA_000428665.1_ASM42866v1/GCA_000428665.1_ASM42866v1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/001/886/315/GCA_001886315.1_BB01/GCA_001886315.1_BB01_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/166/855/GCA_000166855.2_ASM16685v2/GCA_000166855.2_ASM16685v2_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/219/235/GCA_000219235.2_ASM21923v2/GCA_000219235.2_ASM21923v2_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/466/025/GCA_000466025.1_Red_Oak_Large_Contigs/GCA_000466025.1_Red_Oak_Large_Contigs_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/506/405/GCA_000506405.1_X._fastidiosa_32/GCA_000506405.1_X._fastidiosa_32_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/506/905/GCA_000506905.2_ASM50690v2/GCA_000506905.2_ASM50690v2_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/567/985/GCA_000567985.1_Xylella_fastidiosa_Mul-MD/GCA_000567985.1_Xylella_fastidiosa_Mul-MD_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/732/705/GCA_000732705.1_ASM73270v1/GCA_000732705.1_ASM73270v1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/767/565/GCA_000767565.1_ASM76756v1/GCA_000767565.1_ASM76756v1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/811/965/GCA_000811965.1_ASM81196v1/GCA_000811965.1_ASM81196v1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/001/417/925/GCA_001417925.1_ASM141792v1/GCA_001417925.1_ASM141792v1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/001/549/735/GCA_001549735.1_XFAS004-SEQ-2-ASM-1/GCA_001549735.1_XFAS004-SEQ-2-ASM-1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/001/549/745/GCA_001549745.1_XFAS002-SEQ-2-ASM-1/GCA_001549745.1_XFAS002-SEQ-2-ASM-1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/001/549/755/GCA_001549755.1_XFAS005-SEQ-1-ASM-1/GCA_001549755.1_XFAS005-SEQ-1-ASM-1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/001/549/765/GCA_001549765.1_XFAS001-SEQ-2-ASM-1/GCA_001549765.1_XFAS001-SEQ-2-ASM-1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/001/549/815/GCA_001549815.1_XFAS003-SEQ-2-ASM-1/GCA_001549815.1_XFAS003-SEQ-2-ASM-1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/001/549/825/GCA_001549825.1_XFAS006-SEQ-1-ASM-1/GCA_001549825.1_XFAS006-SEQ-1-ASM-1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/001/572/105/GCA_001572105.1_ASM157210v1/GCA_001572105.1_ASM157210v1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/001/684/415/GCA_001684415.1_ASM168441v1/GCA_001684415.1_ASM168441v1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/001/971/465/GCA_001971465.1_ASM197146v1/GCA_001971465.1_ASM197146v1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/001/971/505/GCA_001971505.1_ASM197150v1/GCA_001971505.1_ASM197150v1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/166/835/GCA_000166835.1_ASM16683v1/GCA_000166835.1_ASM16683v1_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/001/469/345/GCA_001469345.1_XYFPCFBP8072/GCA_001469345.1_XYFPCFBP8072_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/001/469/395/GCA_001469395.1_XYFPCFBP8073/GCA_001469395.1_XYFPCFBP8073_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/900/129/695/GCA_900129695.1_IMG-taxon_2595698223_annotated_assembly/GCA_900129695.1_IMG-taxon_2595698223_annotated_assembly_genomic.fna.gz    .
wget    ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/001/971/475/GCA_001971475.1_ASM197147v1/GCA_001971475.1_ASM197147v1_genomic.fna.gz    .


# Genome annotation using prokka 

for file in /home/hulinm/xylella/assembly/ncbi_genomes/*.fna ; do 
file_short=$(basename $file | sed s/".fna"//g) 
prokka  --usegenus --genus xf $file --outdir $file_short

# OrthoMCL 

# Rename ffn file to contain genome name not PROKKA output 
for file in /home/hulinm/xylella/assembly/ncbi_genomes/*.fna ; do 
file_short=$(basename $file | sed s/".fna"//g) 
cp /home/hulinm/xylella/assembly/ncbi_genomes/"$file_short"/*.faa /home/hulinm/xylella/assembly/ncbi_genomes/"$file_short"/"$file_short".faa 

# Move all faa files to orthomcl directory within Xylella/analysis/orthomcl/nucleotide

cp /home/hulinm/xylella/assembly/ncbi_genomes/*/*.faa .

# Modify all fasta files to remove description and get into correct format for OrthMCL
# Each fasta item must be in format of strain|peg.number

for file in /home/hulinm/xylella/analysis/orthomcl/formatted/*.faa ; do  
file_short=$(basename $file | sed s/".faa"//g | cut -f1 -d ".") 
echo $file_short
sed -e 's/^\(>[^[:space:]]*\).*/\1/' $file | sed s/"_"/"|peg."/g  > "$file_short".fa
done

for file in /home/hulinm/xylella/analysis/orthomcl/formatted/*.fa ; do 
id=$(less $file | grep ">" | cut -f1 -d "|" | sed s/">"//g | uniq) 
file_short=$(basename $file | sed s/".fa"//g) 
echo $id 
echo $file_short
sed s/"$id"/"$file_short"/g $file > $file_short.fasta


# OrthoMCL commands 

#Running ORTHO-MCL

 ProjDir=/home/hulinm
  cd $ProjDir
  IsolateAbrv=Pcac_10300_414_404_Pinf
  WorkDir=xylella/analysis/orthomcl/
  mkdir -p $WorkDir
  #mkdir -p $WorkDir/formatted
  mkdir -p $WorkDir/goodProteins
  mkdir -p $WorkDir/badProteins

## Run orthomclFilterFasta on 108 genomes

WorkDir=/home/hulinm/xylella/analysis/orthomcl

Input_dir=$WorkDir/formatted
echo $Input_dir
  Min_length=50
  Max_percent_stops=20
  Good_proteins_file=$WorkDir/goodProteins/goodProteins.fasta
  Poor_proteins_file=$WorkDir/badProteins/poorProteins.fasta
  orthomclFilterFasta $Input_dir $Min_length $Max_percent_stops $Good_proteins_file $Poor_proteins_file

#checks
grep ">" poorProteins.fasta | wc -l : 3964 poor proteins
grep ">" goodProteins.fasta | wc -l : 110479 good proteins
#grep -c ">" ./formatted/*.fasta > features_no


## Run all v all blast

WorkDir=/home/hulinm/xylella/analysis/orthomcl
Good_proteins_file=$WorkDir/goodProteins/goodProteins.fasta
Poor_proteins_file=$WorkDir/badProteins/poorProteins.fasta

BlastDB=$WorkDir/blastall/all.db

  makeblastdb -in $Good_proteins_file -dbtype prot -out $BlastDB
  BlastOut=$WorkDir/all_results.tsv
  mkdir -p $WorkDir/splitfiles

  SplitDir=/home/armita/git_repos/emr_repos/tools/seq_tools/feature_annotation/signal_peptides
  $SplitDir/splitfile_500.py --inp_fasta /home/hulinm/xylella/analysis/orthomcl/goodProteins/goodProteins.fasta --out_dir $WorkDir/splitfiles --out_base goodProteins

  ProgDir=/home/hulinm/pseudomonas_data/pseudomonas/analysis/orthomcl
  for File in $(find $WorkDir/splitfiles); do
    Jobs=$(qstat | grep 'blast_500' | wc -l)
    while [ $Jobs -gt 32 ]; do
      sleep 10
      printf "."
      Jobs=$(qstat | grep 'blast_500' | wc -l)
    done
    printf "\n"
    echo $File
    BlastOut=$(echo $File | sed 's/.fa/.tab/g')
    qsub $ProgDir/blast_500.sh $BlastDB $File $BlastOut
  done


## merge hits
  WorkDir=/home/hulinm/xylella/analysis/orthomcl
  MergeHits=all_blast.tab
  printf "" > $MergeHits
  for Num in $(ls $WorkDir/splitfiles/*.tab | rev | cut -f1 -d '_' | rev | sort -n); do
    File=$(ls $WorkDir/splitfiles/*_$Num)
    cat $File
  done > $MergeHits

## find orthologs. Run from home directory

  ProgDir=/home/hulinm/git_repos/tools/pathogen/orthology/orthoMCL
  MergeHits=xylella/analysis/orthomcl/all_blast.tab
  GoodProts=xylella/analysis/orthomcl/goodProteins/goodProteins.fasta
  qsub $ProgDir/qsub_orthomclMH.sh $MergeHits $GoodProts 1.5






# Phylogenetics 
# Recombination analysis
# Effector identification through homology to known and through orthomcl look at enrichment in particular strains/groups of different gene families 
# SignalP
# Gain and loss of gene families on phylogeny (GLOOME)
# GWAS
