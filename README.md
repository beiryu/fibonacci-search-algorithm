
# Fibonacci Search Chapter Bracketing

Với giới hạn về số lần chúng ta truy vấn Fibonacci Search đảm bảo chúng ta thu nhỏ tối đa đoạn [a, b] chứa minimum.

**Trước hết chúng ta tìm hiểu thế nào là tỉ lệ Kiefer**

## Kiefer's Ratios
[Sequence Minimmax Search For A Maximum](https://www.ams.org/journals/proc/1953-004-03/S0002-9939-1953-0055639-3/S0002-9939-1953-0055639-3.pdf)

Hai tỉ lệ quan trọng mà mình sử dụng
- $y_1 = U_{N-2}/U_N$
- $y_2 = U_{N-1}/U_N$

```math
SE = \frac{\sigma}{\sqrt{n}}
```

$`\sqrt{2}`$

![formula](https://render.githubusercontent.com/render/math?math=e^{i \pi} = -1)

Ví dụ:
- $N = 6$
- $F = 1, 1, 2, 3, 5, 8, 13$
- $y1 = 5/13$
- $y2 = 8/13$

Với 1 đoạn thẳng 13 đơn vị, bằng cách sử dụng 2 số Fibonacci trước đó, chúng ta có thể chia thành 5 và 8 tại điểm chia c, và d.

Với giá trị mới là 8, chúng ta tiếp tục dùng 3 và 5 để chia. Tiếp tục như thế cho đến khi còn 1 - 1

Vì quá trình này đối xứng nên có không thực sự quan trọng nếu bạn chọn bên trái hay bên phải. Cuối cùng thì cũng phải chia nhỏ thành đoạn 1 - 1

## Finding n
Ví dụ trong trường hợp:
- $\frac{b-a}{\epsilon} = F_n$
- $b-a=1$
- $\epsilon = 0.01$
- $\frac{1}{0.01} = 100$

Chúng ta cần chọn n sao cho $F_n = 100$ hoặc $F_n > 100$

| n | $F_n$ |
| :---: | :---: |
| 0 | 1 |
| 1 | 1 |
| 2 | 2 |
| ... | ... |
| 10 | 89 |
| 11 | 144 |

**Johnson nhật xét trên n:** với $F_{20} > 10000$, khoảng tối đa luôn nằm trong $10^{-4}$ với 20 phếp tính, trong khi đó Dichotomous Search cần đến 28.

[Best Exploration For Maximum Is Fibonaccian By S. M. Johnson](https://apps.dtic.mil/sti/pdfs/AD0224385.pdf)

## Binet's Formula
Số Fibonacci có thể được xác định bằng công thức của Binet
$
F_n = \frac{\varphi^n - (1 - \varphi)^n}{\sqrt{5}}, \varphi = \frac{1+\sqrt5}{2} \approx 1.61803  
$
$\varphi$ được gọi là golden ratio.

**Tỷ lệ giữa các giá trị liên tiếp trong chuỗi Fibonacci là:**

$
\frac{F_n}{F_{n-1}} = \varphi\frac{1 - s^{n + 1}}{1 - s^n}, s = (1-\sqrt5)/(1+\sqrt5) \approx -0.382
$


## Fibonacci Search Algorithm
- $c = a + \frac{F_{n-2}}{F_n}(b - a)$
- $d = a + \frac{F_{n-1}}{F_n}(b - a)$
- Khi f(c) < f(d) thì bỏ khoảng ngoài cùng bên phải.
- Ngược lại, thì bỏ khoảng ngoài cùng bên trái.  
- Ngược lại giảm bộ xuống cho đến khi gặp điều kiện dừng.