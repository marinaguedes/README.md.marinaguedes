**Copiar arquivo**
cp /tmp/mock/plant_viral_mock_v1.fastq.gz 

**1 - Contagem de reads**
 echo $(( (( `zcat plant_viral_mock_v1.fastq.gz | wc -l` ) / 4) ))  *10000000*

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
echo "1141019847 / 10000000" | *bc = 114*

**7 - Maior read**
zgrep -E "^[ATGCN]+$" plant_viral_mock_v1.fastq.gz | wc -L = 114
zcat plant_viral_mock_v1.fastq.gz | head -n 1 = @read_1

**8 - Filtragem por cumprimento**
zcat plant_viral_mock_v1.fastq.gz | paste - - - - > tabela.txt
awk 'length($2) >= 100' tabela.txt > tabela_filtrada.txt
tr "\t" "\n" < tabela_filtrada.txt > filtrado.fastq
head -n 4 filtrado.fastq

**9 - Conversão de qualidade**
paste - - - - < filtrado.fastq | awk '{print $1, $4}' > id_e_letras.txt
awk '{printf "%s", $1; for(i=1; i<=length($2); i++) printf " %d", index("!\"#$%&'\''()*+,-./0123456789:;<=>?@ABCDEFGHI", substr($2,i,1)) - 1; print ""}' id_e_letras.txt > exercicio9_resultado.txt
head -n 2 exercicio9_resultado.txt

**10 - Qualidade média**
awk '{ soma = 0; for(i=2; i<=NF; i++) soma += $i; media = soma / (NF-1); printf "%s %.1f\n", $1, media }' exercicio9_resultado.txt > exercicio10_resultado.txt
head -n 3 exercicio10_resultado.txt

**11 - Filtragem por qualidade**
awk '$2 >= 1.5 {print $1}' exercicio10_resultado.txt > ids_aprovados.txt
awk 'NR==FNR {aprovados[$1]; next} {id=$1; getline seq; getline sep; getline qual; if (id in aprovados) printf "%s\n%s\n%s\n%s\n", id, seq, sep, qual}' ids_aprovados.txt filtrado.fastq > exercicio11_resultado.txt
head -n 4 exercicio11_resultado.txt

**12 - Identificação de Ns**
awk '{id=$0; getline seq; getline sep; getline qual; if (seq ~ /N/) contador++} END {print contador+0}' filtrado.fastq > exercicio12_resultado.txt
cat exercicio12_resultado.txt *34*

**13 - Remoção de Ns**
awk '{id=$0; getline seq; getline sep; getline qual; if (seq !~ /N/) printf "%s\n%s\n%s\n%s\n", id, seq, sep, qual}' filtrado.fastq > exercicio13_resultado.txt
head -n 4 exercicio13_resultado.txt

**14 - Conteúdo GC**
awk '{id=$1; getline seq; getline sep; getline qual; g = gsub(/[Gg]/, "", seq); c = gsub(/[Cc]/, "", seq); total = length(seq) + g + c; gc = ((g + c) / total) * 100; printf "%s %.2f%%\n", id, gc}' filtrado.fastq > exercicio14_resultado.txt
head -n 3 exercicio14_resultado.txt
*@read_1 52.21%
@read_2 50.00%
@read_3 56.14%*

**15 - Filtragem por GC**
awk '{id=$0; getline seq; getline sep; getline qual; seq_copia=seq; g = gsub(/[Gg]/, "", seq_copia); c = gsub(/[Cc]/, "", seq_copia); total = length(seq_copia) + g + c; gc = ((g + c) / total) * 100; if (gc >= 50.0) printf "%s\n%s\n%s\n%s\n", id, seq, sep, qual}' filtrado.fastq > exercicio15_resultado.txt
head -n 8 exercicio15_resultado.txt





