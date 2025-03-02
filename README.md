### Эпигеномика
# Домашнее задание №2. Отчёт
В данном практическом задании определяются участки генома, где присутствует определенная гистоновая модификация в конкретном типе клеток с помощью анализа ChIP-Seq данных.

Работа проводилась в [блокноте Google Colab](https://colab.research.google.com/drive/1vNY6Gd5PF2tE6JCybgyyHxBQqTt5Ni12?usp=sharing).

## Основное задание
Скачаем чтения и с помощью `FastQC` оценим их качество:

![](https://github.com/akamaaru/hse25_hw2/blob/main/img/multi.png)

Видим, что у `ERN` чтения довольно хорошие, их можно не подрезать. Остальные подрежем до качества 20 с помощью команды `trimmomatic`:

![](https://github.com/akamaaru/hse25_hw2/blob/main/img/trimmed_comparison.png)
