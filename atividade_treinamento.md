**Copiar arquivo**
cp /tmp/mock/plant_viral_mock_v1.fastq.gz 

**1 - Contagem de reads**
 echo $(( $(zcat workspace/plant_viral_mock_v1.fastq.gz | wc -l) /4)) = 10000000

**2 - Extração de identificadores**
zgrep "^@" workspace/plant_viral_mock_v1.fastq.gz

**3 - Extração de sequências**
zgrep "^[ATGCN]\+$" workspace/plant_viral_mock_v1.fastq.gz

**4 - Conversão para FASTA**
