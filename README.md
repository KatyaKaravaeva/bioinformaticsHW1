# bioinformaticsHW1
Майнор биоинформатика, Анализ данных секвенирования HW#1

Караваева Екатерина 2 группа

## Описание команд

#### Создаем ссылки
> $ ln -s /usr/share/data-minor-bioinf/assembly/oil_R1.fastq  
> 
> $ ln -s /usr/share/data-minor-bioinf/assembly/oil_R2.fastq
> 
> $ ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R1_001.fastq
> 
> $ ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R2_001.fastq

#### Выбираем случайные чтения для каждого типа, SEED = 720

###### 5 млн чтений типа paired-end

>seqtk sample -s720 oil_R1.fastq 5000000 > sub1.fastq
>
>seqtk sample -s720 oil_R2.fastq 5000000 > sub2.fastq

###### 1.5 млн чтений типа mate-pairs

> seqtk sample -s720 oilMP_S4_L001_R1_001.fastq 1500000 > matep1.fastq
> 
> seqtk sample -s720 oilMP_S4_L001_R2_001.fastq 1500000 > matep1.fastq


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

![image]()
![image]()
![image]()
![image]()
![image]()





