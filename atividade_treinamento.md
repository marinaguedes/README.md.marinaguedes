**Copiar arquivo**
cp /tmp/mock/plant_viral_mock_v1.fastq.gz 

**1 - Contagem de reads**
 echo $(( (( `zcat plant_viral_mock_v1.fastq.gz | wc -l` ) / 4) )) = 10000000

**2 - Extração de identificadores**
zgrep "^@" plant_viral_mock_v1.fastq.gz

**3 - Extração de sequências**
zgrep -E "^[ATGCN]+$" plant_viral_mock_v1.fastq.gz

**4 - Conversão para FASTA**
zgrep -E "^@|^[ATGCN]+$" plant_viral_mock_v1.fastq.gz

**5 - Comprimento dos reads**
zcat plant_viral_mock_v1.fastq.gz | awk 'NR % 4 == 1 {id=$0} NR % 4 == 2 {print id, length($0)}'

**6 - Comprimento médio**
zgrep -E "^[ATGCN]+$" plant_viral_mock_v1.fastq.gz | wc -m = 1141019847
echo "1141019847 / 10000000" | bc = 114

**7 - Maior read**
zgrep -E "^[ATGCN]+$" plant_viral_mock_v1.fastq.gz | wc -L = 114
zcat plant_viral_mock_v1.fastq.gz | head -n 1 = @read_1

**8 - Filtragem por cumprimento**
zcat plant_viral_mock_v1.fastq.gz | paste - - - - > tabela.txt
awk 'length($2) >= 100' tabela.txt > tabela_filtrada.txt
tr "\t" "\n" < tabela_filtrada.txt > filtrado.fastq
head -n 4 filtrado.fastq

**9 - Conversão de qualidade**






