# bioinformaticsHW1
Майнор биоинформатика, Анализ данных секвенирования HW#1

Караваева Екатерина 2 группа

## Описание команд

#### Создаем ссылки
> ln -s /usr/share/data-minor-bioinf/assembly/oil_R1.fastq  
> 
> ln -s /usr/share/data-minor-bioinf/assembly/oil_R2.fastq
> 
> ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R1_001.fastq
> 
> ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R2_001.fastq

#### Выбираем случайные чтения для каждого типа, SEED = 720

###### 5 млн чтений типа paired-end

>seqtk sample -s720 oil_R1.fastq 5000000 > sub1.fastq
>
>seqtk sample -s720 oil_R2.fastq 5000000 > sub2.fastq

###### 1.5 млн чтений типа mate-pairs

> seqtk sample -s720 oilMP_S4_L001_R1_001.fastq 1500000 > matep1.fastq
> 
> seqtk sample -s720 oilMP_S4_L001_R2_001.fastq 1500000 > matep2.fastq


#### Создаем папки для хранения результата, оцениваем качество чтений с помощью fastQC

> mkdir fastqc
>
> ls sub* matep* | xargs -tI{} fastqc -o fastqc {}


#### Создаем папки для хранения результата, оцениваем качество чтений с помощью MultiQC

> mkdir multiqc
>
> multiqc -o multiqc fastqc

#### Выводим теперь общий отчет по исходным данным чтения

![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/screens_general/first_screen_general.png)
![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/screens_general/second_screen_general.png)
![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/screens_general/third_screen_general.png)
![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/screens_general/fourth_screen_general.png)
![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/screens_general/fifth_screen_general.png)

#### Подрезаем чтения по качеству с помощью platanus_trim и platanus_internal_trim

> platanus_trim sub1.fastq sub2.fastq
> 
> platanus_internal_trim matep1.fastq matep2.fastq

#### Удаление изначальных файлов

Удаление производилось вручную с помощью MobaXtern.

Однако можно было применить:

> rm sub1.fastq 
> 
> rm sub2.fastq
> 
> rm matep1.fastq 
> 
> rm matep2.fastq

#### Создаем папки для хранения результата, oцениваем качество обрезанных чтений с помощью fastQC

> mkdir fastqc_trim
> 
> ls sub* matep*| xargs -tI{} fastqc -o fastqc_trim {}

#### Создаем папки для хранения результата, оцениваем качество обрезанных чтений с помощью MultiQC

> mkdir multiqc_trim
> 
> multiqc -o multiqc_trim fastqc_trim


#### Получили качество подрезанных чтений, теперь выводим по ним общую статистику

![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/s%D1%81reen_trimed/first_screen_trimed.png)
![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/s%D1%81reen_trimed/second_screen_trimed.png)
![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/s%D1%81reen_trimed/third_screen_trimed.png)
![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/s%D1%81reen_trimed/fourth_screen_trimed.png)
![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/s%D1%81reen_trimed/fifth_screen_trimed.png)


--> [Ссылка на коллаб](https://colab.research.google.com/drive/1XN57WApEhRWTBbDVSDELpeRlf4WfJSs-?usp=sharing)

#### Вводим screen

> screen

#### Собираем континги из подрезанных чтений с помощью platanus assemble

> time platanus assemble -o Poil -f sub1.fastq.trimmed sub2.fastq.trimmed 2> assemble.log

![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/screen_colab/contigs.png)

#### Cобираем скаффолды из контигов, а также из подрезанных чтений с помощью platanus scaffold

> time platanus scaffold -o Poil -c Poil_contig.fa -IP1 sub1.fastq.trimmed sub2.fastq.trimmed -OP2 matep1.fastq.int_trimmed matep2.fastq.int_trimmed 2> scaffold.log

![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/screen_colab/scaffolds.png)

#### Уменьшаем количество гэпов

> time platanus gap_close -o Poil -c Poil_scaffold.fa -IP1 sub1.fastq.trimmed sub2.fastq.trimmed -OP2 matep1.fastq.int_trimmed matep2.fastq.int_trimmed 2> gapclose.log


![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/screen_colab/gap_closed.png)


## Бонусная часть

#### Проделываем такие же действие как и ранее, но из меньшего кол-ва чтений (взяла в два раза меньше)

![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/bonus/first_command.png)
![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/bonus/second_command.png)
![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/bonus/third_command.png)
![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/bonus/fourth_command.png)
![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/bonus/fifth_command.png)
![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/bonus/six_command.png)
![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/bonus/seven_command.png)

#### Анализ бонусной части и сравнение

> старое
> ![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/screen_colab/contigs.png)
> новое
> ![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/bonus/analys1.png)


> старое
> ![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/screen_colab/scaffolds.png)
> 
> новое
> ![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/bonus/analys2.png)


> старое
> ![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/screen_colab/gap_closed.png)
> 
> новое
> ![image](https://github.com/KatyaKaravaeva/hse22_hw1/blob/main/bonus/analys3.png)

#### Вывод

> После сборки генома из меньшего кол-ва чтений (разница в 2 раза) - количество контигов и скаффолдов увеличилось

> Для контигов и скаффолдов N50 немного уменьшился.

> Длина самого длинного скаффолда у генома из меньшего количества чтений больше, чем у генома из большего.

> Количество гэпов в полученных скаффолдах в двух геномах из большего количества чтений >= количество гэпов в полученных скаффолдах в двух геномах из меньшего количества чтений
