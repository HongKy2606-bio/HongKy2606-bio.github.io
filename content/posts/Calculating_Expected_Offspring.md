+++
date = '2026-02-24T19:06:50+07:00'
draft = false
title = 'ROSALIND - IEV'
math = true
tags = ['Python','ROSALIND','Evolution of Population' ,'Di truyền quần thể', 'Di truyền học'] 
categories = ['Lập trình sinh học']   
[cover]
  image = "/images/Law-of-Segregation.jpg"
  caption = "Quy luật 1 của Mendel"
+++
# ROSALIND | Calculating Expected Offspring
[This](https://rosalind.info/problems/iev/) problem:

**Given**: Six non-negative integers, each of which does not exceed 20,000. The integers correspond to the number of couples in a population possessing each genotype pairing for a given factor. In order, the six given integers represent the number of couples having the following genotypes:

1. AA-AA
2. AA-Aa
3. AA-aa
4. Aa-Aa
5. Aa-aa
6. aa-aa

Sample Data Set:
`1 0 0 1 0 1`

**Output**: The expected number of offspring displaying the dominant phenotype in the next generation, under the assumption that every couple has exactly two offspring.

Sample Output:
`3.5`

## 1. Góc độ Toán học - Xác suất & Thống kê
Quan trọng để hiểu được mục này, cần blablabla
## 2. Góc độ Sinh học
{{< quiz question="Biết Allele A (Xanh) trội hơn Allele a (Vàng). Cây đậu Hà Lan thuần chủng hạt vàng (AA) lai với hạt xanh cho F1 toàn hạt gì?" answer="vàng" >}}
**Cách giải:**
Dựa theo quy luật phân ly của Mendel:
- Allele A (vàng) là trội hoàn toàn so với allele a (xanh).
- P: AA x aa -> F1: 100% Aa (Kiểu hình: vàng).
{{< /quiz >}}
## 3. Bài giải
Defin