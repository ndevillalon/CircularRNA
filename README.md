# CircularRNA

- Fastq original

Mapear a humano (6) y eliminar alineamientos perfectos (3 y 4)

- FASTQ Nicolas

Utilizamos el script de Rocio para aislar secuencias repetitivas (1)

- FASTQ Rocio

BWT para detectar duplicados de unidades repetitivas (2):

  Generamos un Excel con cada unidad repetitiva (sequence and id) y numero de veces que aparece
  
  Generamos un FASTQ con las unidades repetitivas unicas (sin hacer permutaciones) El fastq tendrá etiqueta "filtered"
  
  Repetimos los dos pasos anteriores pero teniendo en cuenta también el complemento invertido (El fastq tendrá etiqueta "final") 

- FASTQ2

Alineamos contra el mykoplasma y mosca y generamos un SAM file (6)

Quitamos del FASTQ2 las secuencias que han mapeado en el mykoplasma y mosca (4) El fastq tendrá etiqueta "final3"

Las secuencias restantes les hacemos el shift (5), generando el FASTQ3 (El fastq tendrá etiqueta "final3_shifted")


- FASTQ3
  
Mapear a humano, generando un SAM file (6)

- SAM file (3)
  
Detectar las secuencias con 1 soft clip

Detectar las secuencias con 2 soft clips

Detectar las secuencias con 3 soft clips

HERRAMIENTAS:

1. cirseq_adapt: Aisla la secuencia repetitiva en aquellas secuencias que lo sean

2. Filtrar_secuencias_duplicadas

3. Dividir_SAM_según_softclip: Separa un SAM en 3 SAM diferentes, uno con las secuencias sin softclip, otro con aquellas con un softclip y otro con softclip en ambas

4. Eliminar_secuencias_del_fastq_con_sam: Genera con un archivo SAM una lista de secuencias a eliminar de un fastq 

5. Shifting_de_las_secuencias: Introduciendo un fastq genera otro con todas las permutaciones de cada secuencia inicial.

6. BOWTIE: 
Para mapear utilizaremos un comando bowtie con esta estructura

bowtie2 --sensitive-local --score-min G,2,8 -k 1 --no-unal -x [index_escogido] -U FASTQ/[archivo fastq] -S SAM/[archivo sam de salida]
