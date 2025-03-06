### Эпигеномика
# Домашнее задание №2. Отчёт
В данном практическом задании определяются участки генома, где присутствует определенная гистоновая модификация в конкретном типе клеток с помощью анализа ChIP-Seq данных.

Работа проводилась в [блокноте Google Colab](https://colab.research.google.com/drive/1vNY6Gd5PF2tE6JCybgyyHxBQqTt5Ni12?usp=sharing).

## Основное задание
Скачаем чтения и с помощью `FastQC` оценим их качество:

![](https://github.com/akamaaru/hse25_hw2/blob/main/img/multi.png)

Видим, что у `ERN` чтения довольно хорошие, их можно не подрезать. Остальные подрежем до качества 20 с помощью команды `trimmomatic`:

![](https://github.com/akamaaru/hse25_hw2/blob/main/img/trimmed_comparison.png)

Скачаем 14-ю хромосому и выровняем на неё подрезанные чтения с помощью `bowtie2`. В итоге программа выдала следующую информацию о выравнивании:

| ID             | Тип        | Общее число чтений | Число уникально откартированных чтений | Число не уникально откартированных чтений | Общее число откартированных чтений
|----------|:----------:|:----------------:|:----------------:|:----------------:|:----------------:|
| **ERN** | реплика | 18259162   | 787424 (4.31%) | 2937508 (16.09%)  | 3724932 (20.40%) |
| **ERO** | реплика | 18347553   | 803215 (4.38%) | 2992631 (16.31%) | 3795846 (20.69%) |
| **HAG** | контроль | 19660965   | 899551 (4.58%) | 2883508 (14.67%) | 3783059 (19.24%) |

Видим, что общее число откартированных чтений относительно небольшое. Причем у всех трёх экземпляров примерно одинаковая доля откартированных чтений. Поэтому можно предположить, что это из-за того, что мы взяли только одну 14-ю хромасому и картировали на неё, из-за чего только какие-то чтения попали на неё.

После картирования, отфильтруем наши чтения и удалим PCR-реплики с помощью `picard`. 
С помощью `macs2` запустим поиск пиков, а затем построим диаграммы Венна через `intervenne`. Теперь по диаграммам можно сравнить результат с результатом на сайте:

![](https://github.com/akamaaru/hse25_hw2/blob/main/img/venn/multi_venn.png)

Сразу можно обратить внимание на то, что в референсном файле пиков в среднем в 11.5 раз больше, чем в нашем. 
Это всё ещё объясняется тем, что наши чтения мы картировали на одну хромосому, в то время как референсные чтения были картированы на весь геном. 
Также, при поиске пересечений, алгоритм сначала сравнивает длины чтений, и в случае, если длина первого чтения меньше, он ищет его во втором, но не наоборот. 
Поэтому есть предположение, что какие-то чтения пересекались в обоих запусках алгоритма (так как длины чтений у них совпадали); 
какие-то чтения находились только при первом прохождении алгоритма; какие-то -- при втором.

## Бонусное задание 1
Возьмём полученные `.bam` файлы из основной части задания. 
Переведём их в формат `.bigWig`. 
Скачаем аннотацию нашего генома и с помощью `computeMatrix` составим матрицы, на основании которых получим следующие графики:

| Референс | Получившиеся результаты |
| --- | --- |
|  ![](https://github.com/akamaaru/hse25_hw2/blob/main/img/ngs/reference.png) | ![](https://github.com/akamaaru/hse25_hw2/blob/main/img/ngs/results.png) |

Видно, что в обоих графиках расположение метки типично для середины генома. 
Но графики не полностью соответствуют друг другу, так как наши графики строились на основе выборки из одной хромосомы.
