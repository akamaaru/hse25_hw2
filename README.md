### Эпигеномика
# Домашнее задание №2. Отчёт
В данном практическом задании определяются участки генома, где присутствует определенная гистоновая модификация в конкретном типе клеток с помощью анализа ChIP-Seq данных.

Работа проводилась в [блокноте Google Colab](https://colab.research.google.com/drive/1vNY6Gd5PF2tE6JCybgyyHxBQqTt5Ni12?usp=sharing).

## Основное задание
Скачаем чтения и с помощью `FastQC` оценим их качество:

![](https://github.com/akamaaru/hse25_hw2/blob/main/img/multi.png)

Видим, что у `ERN` чтения довольно хорошие, их можно не подрезать. Остальные подрежем до качества 20 с помощью команды `trimmomatic`:

![](https://github.com/akamaaru/hse25_hw2/blob/main/img/trimmed_comparison.png)

Скачаем 14-ю хромасому и выровняем на неё подрезанные чтения с помощью `bowtie2`. В итоге программа выдала следующую информацию о выравнивании:

| ID             | Тип        | Общее число чтений | Число уникально откартированных чтений | Число не уникально откартированных чтений | Общее число откартированных чтений
|----------|:----------:|:----------------:|:----------------:|:----------------:|:----------------:|
| **ERN** | реплика | 18259162   | 787424 (4.31%) | 2937508 (16.09%)  | 3724932 (20.40%) |
| **ERO** | реплика | 18347553   | 803215 (4.38%) | 2992631 (16.31%) | 3795846 (20.69%) |
| **HAG** | контроль | 19660965   | 899551 (4.58%) | 2883508 (14.67%) | 3783059 (19.24%) |
