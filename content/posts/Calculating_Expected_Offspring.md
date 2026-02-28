+++
date = '2026-02-24T19:06:50+07:00'
draft = false
title = 'ROSALIND - IEV'
math = true
tags = ['Python','ROSALIND','Evolution of Population' ,'Di truyền quần thể', 'Di truyền học','Mendel'] 
categories = ['Lập trình sinh học']   
[cover]
  image = "/images/rosalind_iev.jpg"
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
### Định nghĩa Giá trị Kỳ vọng

Đối với một biến ngẫu nhiên $X$ nhận các giá trị nguyên từ $1$ đến $n$, **Giá trị kỳ vọng** (Expected Value) của $X$ được tính bằng công thức:

$$E(X) = \sum_{k=1}^{n} k \times Pr(X = k)$$

Giá trị kỳ vọng cung cấp cho chúng ta một cách để tính toán giá trị trung bình dài hạn của một biến ngẫu nhiên qua một số lượng lớn các phép thử.

### Ví dụ minh họa: Con xúc xắc sáu mặt

Hãy xét ví dụ về $X$ là số nút trên một con xúc xắc sáu mặt đồng chất. Sau một số lượng lớn các lần tung, chúng ta mong đợi nhận được giá trị trung bình là $3.5$ (ngay cả khi việc tung ra một mặt $3.5$ là điều không thể).

Công thức tính giá trị kỳ vọng xác nhận điều này:

$$E(X) = \sum_{k=1}^{6} k \times Pr(X = k) = 3.5$$
### Biến ngẫu nhiên đồng nhất (Uniform Random Variable)

Tổng quát hơn, một biến ngẫu nhiên mà trong đó mọi kết quả cách đều nhau đều có cùng một xác suất được gọi là **Biến ngẫu nhiên đồng nhất** (trong ví dụ về con xúc xắc, "khoảng cách đều" này bằng $1$).

Chúng ta có thể khái quát hóa ví dụ về con xúc xắc: Nếu $X$ là một biến ngẫu nhiên đồng nhất với giá trị nhỏ nhất có thể là $a$ và giá trị lớn nhất là $b$, thì:

$$E(X) = \frac{a + b}{2}$$

### Thử thách nhỏ
Nếu $Y$ là biến ngẫu nhiên liên quan đến kết quả của lần tung xúc xắc thứ hai, dựa trên tính chất tuyến tính của kỳ vọng:
$$E(X + Y) = E(X) + E(Y)$$

Hãy tính toán và nhập kết quả vào ô dưới đây:

{{< quiz question="Giá trị kỳ vọng của tổng hai con xúc xắc E(X + Y) bằng bao nhiêu?" answer="7" >}}
**Giải thích:**
Vì $X$ và $Y$ là hai lần tung xúc xắc độc lập nhưng có cùng phân phối, ta có:
- $E(X) = 3.5$
- $E(Y) = 3.5$
Do đó: $E(X + Y) = 3.5 + 3.5 = 7$.
{{< /quiz >}}

## 2. Góc độ Sinh học
{{< quiz question="Biết Allele A (Xanh) trội hơn Allele a (Vàng). Cây đậu Hà Lan thuần chủng hạt vàng (AA) lai với hạt xanh cho F1 toàn hạt gì?" answer="vàng" >}}
**Cách giải:**
Dựa theo quy luật phân ly của Mendel:
- Allele A (vàng) là trội hoàn toàn so với allele a (xanh).
- P: AA x aa -> F1: 100% Aa (Kiểu hình: vàng).
{{< /quiz >}}

Với câu hỏi cơ bản ở phía trên, thì các bạn có thể thấy rằng, nếu cặp bố mẹ kiểu số 3.AA-aa này sinh 2 con non, thì số con non có kiểu hình trội (A-, Xanh) là 2 con.
Như vậy với mỗi cặp từ 1 - 6 tương ứng có số con non kiểu hình trội tương ứng là - 

  `2 2 2 1.5 1 0`

Giá trị kỳ vọng (Expected value) sau một thế hệ, sẽ có phương trình
$$E = a\cdot2 + b\cdot2 + c\cdot2 + d\cdot1.5 + e\cdot1 + f\cdot o $$

## 3. Bài giải
```Python
def iev(a, b, c, d, e, f):
    return str(a*2 + b*2 + c*2 + d*1.5 + e)
print(iev(17463, 16365, 19779, 19776, 18820, 19228))
```