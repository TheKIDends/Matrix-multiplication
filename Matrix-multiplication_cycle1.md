# Nhân ma trận (Matrix multiplication)

**Nguồn**: Biên soạn lại từ bài viết của Nguyễn *RR* Thành Trung, Nguyễn Mạnh Quân.

**Tác giả**: 

- Nguyễn Châu Khanh - VNU University of Engineering and Technology (VNU-UET)

**Reviewer:** 

> [TOC]

# Mở đầu

Thông thường, để đạt được độ phức tạp thuật toán như mong muốn, cách làm thường là tìm ra một thuật toán ban đầu làm cơ sở, rồi từ đó dùng các kỹ năng để giảm độ phức tạp của thuật toán. Trong bài viết này, tôi xin giới thiệu với bạn đọc một kỹ năng khá thông dụng: **Nhân ma trận**.

# Định nghĩa 

**Tham khảo:** [Ma trận_wikipedia](https://vi.wikipedia.org/wiki/Ma_tr%E1%BA%ADn_(to%C3%A1n_h%E1%BB%8Dc))

## Ma trận

**Ma trận** là một mảng chữ nhật gồm các số, ký hiệu, hoặc biểu thức, sắp xếp theo hàng và cột mà mỗi ma trận tuân theo những quy tắc định trước. 
Các ô trong ma trận được gọi là các phần tử của ma trận. Các phần tử được xác định bằng $2$ địa chỉ hàng $i$ và cột $j$ tương ứng (Kí hiệu là $a_{ij}$).

Ma trận thường được viết trong dấu ngoặc vuông: 

\begin{bmatrix} a_{11} & a_{12} & ... & a_{1n} \\ a_{21} & a_{22} & ... & a_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ a_{m1} & a_{m2} & ... & a_{mn} \end{bmatrix}

Độ lớn hay kích thước của ma trận được định nghĩa bằng số lượng hàng và cột. Một ma trận $m$ hàng và $n$ cột được gọi là ma trận $(m \times n)$, trong khi $m$ và $n$ được gọi là **chiều** của nó. 

- **Ví dụ:** Ma trận $A$ là ma trận $(3 \times 2)$

    $A = \begin{bmatrix} 1 & 2 \\ 5 & 7 \\ 6 & 3 \end{bmatrix}$
    
### Ma trận vuông

Ma trận vuông là ma trận có số hàng và số cột bằng nhau. Ma trận $(n \times n)$ còn gọi là ma trận vuông cấp $n$. Các phần tử $a_{ii}$ tạo thành **đường chéo chính** của ma trận vuông.

- **Ví dụ:** Ma trận vuông cấp $3$ (số hàng và số cột bằng $3$)

    \begin{bmatrix} 1 & 2 & 0 \\ 3 & 0 & 1 \\ 2 & 3 & 1 \end{bmatrix}
 
### Ma trận đơn vị (Identity Matrix)

Ma trận đơn vị $I_n$ cấp $n$ là một ma trận $(n \times n)$ trong đó mọi phần tử trên [đường chéo chính](https://vi.wikipedia.org/wiki/%C4%90%C6%B0%E1%BB%9Dng_ch%C3%A9o_ch%C3%ADnh) bằng $1$ và tất cả những phần tử khác đều bằng $0$. Ma trận đơn vị cấp $n$ cũng chính là ma trận vuông cấp $n$.

- **Ví dụ**

    $I_1 = \begin{bmatrix} 1 \end{bmatrix}$
    
    $I_2 = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}$
    
    ...
    
    $I_n = \begin{bmatrix} 1 & 0 & ... & 0 \\ 0 & 1 & ... & 0 \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & ... & 1 \end{bmatrix}$

### Vector hàng và vector cột

**Vector hàng** hay **ma trận hàng** là một ma trận $(1 \times n)$, tức là ma trận chỉ gồm một một hàng đơn gồm $n$ phần tử.

$\mathbf{a} = \begin{bmatrix} a_1 & a_2 & ... & a_n \end{bmatrix}$

**Vector cột** hay **ma trận cột** là một ma trận $(m \times 1)$, tức là ma trận chỉ gồm một cột đơn gồm $m$ phần tử.

$\mathbf{b} = \begin{bmatrix} b_1 \\ b_2 \\ \vdots \\ b_m \end{bmatrix}$

Tích của vector hàng $\mathbf{a}$ $(1 \times n)$ với vector cột $\mathbf{b}$ $(n \times 1)$ tương đương với [tích vô hướng](https://vi.wikipedia.org/wiki/T%C3%ADch_v%C3%B4_h%C6%B0%E1%BB%9Bng) của hai vector $\mathbf{a}$ và $\mathbf{b}$.

$\mathbf{a} \cdot \mathbf{b} = \begin{bmatrix} a_1 & a_2 & ... & a_n \end{bmatrix} \begin{bmatrix} b_1 \\ b_2 \\ \vdots \\ b_n \end{bmatrix} = \displaystyle\sum_{i = 1}^{n} a_{i} b_{i} = a_1b_1+a_2b_2+...+a_nb_n$

**Tham khảo:** [Vector hàng và cột](https://vi.wikipedia.org/wiki/Vect%C6%A1_h%C3%A0ng_v%C3%A0_c%E1%BB%99t)

## Phép nhân ma trận

Phép nhân hai ma trận chỉ thực hiện được khi số lượng cột trong ma trận thứ nhất phải bằng số lượng hàng trong ma trận thứ hai. Ma trận kết quả, được gọi là **tích ma trận**, có số lượng hàng của ma trận đầu tiên và số cột của ma trận thứ hai. 

Nếu ma trận $A$ có kích thước $(m \times n)$ và ma trận $B$ có kích thước $(n \times p)$, thì ma trận tích $C = A \times B$ có kích thước $(m \times p)$, phần tử đứng ở hàng thứ $i$, cột thứ $j$ xác định bởi công thức:

$C_{ij} = A_{i1} B_{1j} + A_{i2} B_{2j} + ... + A_{in} B_{nj} = \displaystyle\sum_{k = 1}^{n} A_{ik} B_{kj}$ (Với $1 \le i \le m; 1 \le j \le p$)

Hay viết $C_{ij} = \begin{bmatrix} a_{i1} & a_{i2} & ... & a_{in} \end{bmatrix} \begin{bmatrix} b_{1j} \\ b_{2j} \\ ... \\ b_{nj} \end{bmatrix}$, tức là phần tử ở hàng thứ $i$, cột thứ $j$ của $C$ là tích của vector hàng thứ $i$ của ma trận $A$ với vector cột thứ $j$ của ma trận $B$.

- Minh họa tích ma trận $AB$ của hai ma trận $A$ và $B$: 

![](https://i.imgur.com/IUXt8Lx.png)

- **Ví dụ:** Cho $2$ ma trận

    $A = \begin{bmatrix} 2 & 3 & 4 \\ 1 & 0 & 0 \end{bmatrix}$ và $B = \begin{bmatrix} 0 & 1000 \\ 1 & 100 \\ 0 & 10 \end{bmatrix}$

    Phần tử $C_{12}$ của ma trận tích $AB$ là tích của vector hàng thứ nhất của $A$ và vector cột thứ hai của $B$, ta có:
    
    $C_{12} = \displaystyle\sum_{k = 1}^{3} A_{1k} B_{k2} = \begin{bmatrix} 2 & 3 & 4 \end{bmatrix} \begin{bmatrix} 1000 \\ 100 \\ 10 \end{bmatrix} = 2 \times 1000 + 3 \times 100 + 4 \times 10= 2340$
    
    Tính tương tự với tất cả phần tử còn lại của ma trận tích $C$. Ta được ma trận tích $AB$ có dạng:
    
    $C = A \times B = \begin{bmatrix} 2 & 3 & 4 \\ 1 & 0 & 0 \end{bmatrix} \begin{bmatrix} 0 & 1000 \\ 1 & 100 \\ 0 & 10 \end{bmatrix} = \begin{bmatrix} 3 & 2340 \\ 0 & 1000 \end{bmatrix}$

    Mô tả quá trình nhân ma trận:

![](https://i.imgur.com/k2XpJwF.gif)

### Tính chất của phép nhân ma trận

- Tính chất kết hợp: $(AB)C = A(BC)$.
- Tính chất phân phối: $(A+B)C = AC+BC$, cũng như $C(A+B) = CA+CB$. 
    Bạn có thể tìm hiểu thêm về **phép cộng ma trận** tại [đây](https://vi.wikipedia.org/wiki/Ph%C3%A9p_c%E1%BB%99ng_ma_tr%E1%BA%ADn).
- Phép nhân ma trận **không** có tính chất giao hoán: Tích $AB$ có thể xác định trong khi $BA$ không nhất thiết phải xác định, tức là nếu $A$ và $B$ lần lượt có số chiều $(m \times n)$ và $(n \times p)$, và $m \neq p$. Thậm chí khi cả hai tích này đều tồn tại thì chúng không nhất thiết phải bằng nhau, tức là $AB \neq BA$.
    - **Ví dụ:**
    
        $\begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix} \begin{bmatrix} 0 & 1 \\ 0 & 0 \end{bmatrix} = \begin{bmatrix} 0 & 1 \\ 0 & 3 \end{bmatrix}$, trong khi $\begin{bmatrix} 0 & 1 \\ 0 & 0 \end{bmatrix} \begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix} = \begin{bmatrix} 3 & 4 \\ 0 & 0 \end{bmatrix}$.
 - Khi thực hiện nhân một ma trận bất kì với **ma trận đơn vị** thì vẫn thu được kết quả của chính ma trận đó, tức là: $AI_n = I_mA = A$ (với ma trận $A$ kích thước $(m \times n)$ bất kỳ). 
     Cũng chính vì tính chất này mà $I$ có tên gọi là **ma trận đơn vị**.

## Lũy thừa ma trận

Cho ma trận vuông $A$ cấp $n$. Khi đó ta có phép tính ma trận $A$ lũy thừa $k$ (kí hiệu: $A^k$), với $k$ là một số nguyên không âm.

$A^k = \underbrace{A \times A \times A \times ... \times A}_\text{k}$

**Trường hợp đặc biệt**: Với $k = 0$, ma trận $A^0$ được xác định là **ma trận đơn vị** có cùng kích thước, tức là $A^0 = I_n$.

- **Ví dụ:** Cho ma trận vuông $A$ cấp $3$ 

    $A = \begin{bmatrix} 1 & 2 & 0 \\ 3 & 0 & 1 \\ 2 & 3 & 1 \end{bmatrix}$
    
    $A^0 = I_3 = \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix}$
    
    $A^2 = A \times A = \begin{bmatrix} 1 & 2 & 0 \\ 3 & 0 & 1 \\ 2 & 3 & 1 \end{bmatrix} \begin{bmatrix} 1 & 2 & 0 \\ 3 & 0 & 1 \\ 2 & 3 & 1 \end{bmatrix} = \begin{bmatrix} 7 & 2 & 2 \\ 5 & 9 & 1 \\ 13 & 7 & 4 \end{bmatrix}$ 
    
    $A^3 = A \times A \times A = A^2 \times A = \begin{bmatrix} 7 & 2 & 2 \\ 5 & 9 & 1 \\ 13 & 7 & 4 \end{bmatrix} \begin{bmatrix} 1 & 2 & 0 \\ 3 & 0 & 1 \\ 2 & 3 & 1 \end{bmatrix} = \begin{bmatrix} 17 & 20 & 4 \\ 34 & 13 & 10 \\ 42 & 38 & 11 \end{bmatrix}$ 

Nhờ **tính chất kết hợp** của phép nhân ma trận nên ta có thể tính nhanh lũy thừa của ma trận tương tự như cách tính hàm mũ thông thường  bằng phương pháp **chia để trị**  (tính $a^k$ với $a$ là số nguyên). Bạn có thể tìm hiểu về cách tính hàm mũ tại [đây](https://vnoi.info/wiki/translate/he/Number-Theory-3.md).

# Cài đặt

``` cpp=
#include <bits/stdc++.h>

using namespace std;

struct matrix {
    static const int sizeMatrix = 100;
    static const long long mod  = 1e18;
    int row, column;
    long long a[sizeMatrix][sizeMatrix];

    long long* operator[] (int i) { return a[i]; }

    // Ma trận đơn vị
    matrix identityMatrix(int n) {
        matrix tmp(n, n);
        for (int i = 1; i <= n; ++i) tmp[i][i] = 1;
        return tmp;
    }

    // Phép gán ma trận
    void operator = (matrix b) {
        row = b.row, column = b.column;
        for (int i = 1; i <= b.row; ++i)
            for (int j = 1; j <= b.column; ++j) a[i][j] = b[i][j];
    }

    // Nhân ma trận
    matrix operator * (matrix b) {
        matrix c(row, b.column);
        for (int i = 1; i <= row; ++i)
            for (int j = 1; j <= b.column; ++j)
                for (int k = 1; k <= column; ++k) {
                    c[i][j] += (a[i][k] % mod) * (b[k][j] % mod) % mod;
                    c[i][j] %= mod;
                }
        return c;
    }

    matrix power(matrix tmp, int k) {
        if (k == 0) return identityMatrix(column);
        if (k == 1) return tmp;
        matrix p = power(tmp, k / 2);
        p = p * p;
        if (k & 1) return p * tmp;
        return p;
    }
    
    // Lũy thừa ma trận
    matrix operator ^ (int k) {
        matrix tmp(row, column);
        for (int i = 1; i <= row; ++i)
            for (int j = 1; j <= column; ++j) tmp[i][j] = a[i][j];
        return power(tmp, k);
    }

    // Khởi tạo ma trận
    void clear(int m, int n) { 
        row = m, column = n; 
        for (int i = 1; i <= row; ++i) 
            fill_n(a[i], column + 1, 0); 
    }
    matrix (int m, int n) { clear(m, n); }
};

void coutMatrix(matrix a) {
    for (int i = 1; i <= a.row; ++i) {
        for (int j = 1; j <= a.column; ++j) cout << a[i][j] << ' ';
        cout << '\n';
    }
}

int main(){
    matrix a(2, 2);
    a[1][1] = 1; a[1][2] = 2; // 1 2
    a[2][1] = 3; a[2][2] = 4; // 3 4

    matrix b(2, 3);
    b[1][1] = 0; b[1][2] = 10; b[1][3] = 100; // 0 10 100
    b[2][1] = 1; b[2][2] =  1; b[2][3] =  10; // 1  1  10

    coutMatrix(a * b);
    // 2 12 120 
    // 4 34 340 

    coutMatrix(a ^ 3);
    // 37 54 
    // 81 118

    b = a;
    coutMatrix(b);
    // 1 2 
    // 3 4

    b = b ^ 0;
    coutMatrix(b);
    // 1 0 0 
    // 0 1 0 
    // 0 0 1

    b.clear(3, 2);
    coutMatrix(b);
    // 0 0 
    // 0 0 
    // 0 0
}
```
## Đánh giá

**Độ phức tạp**

- **Nhân ma trận:** Độ phức tạp $O(n \times m \times p)$.
    
    - **Ghi chú:** Đối với phép nhân các ma trận vuông kích thước $(n \times n)$, có thuật toán nhân ma trận [Strassen](https://en.wikipedia.org/wiki/Strassen_algorithm) với độ phức tạp $O(N^{\log_2{7}}) \approx O(N^{2.807})$ theo tư tưởng chia nhỏ ma trận (tương tự cách nhân nhanh $2$ số lớn). Tuy nhiên cài đặt rất phức tạp và trên thực tế với giá trị $n$ thường gặp, cách này không chạy nhanh hơn nhân ma trận thông thường $O(n^3)$.

- **Lũy thừa ma trận:** Với ma trận vuông $A$ cấp $n$, thuật toán tính $A^k$ có độ phức tạp $O(n^3 \times logk)$.

# Ví dụ 1

Chúng ta hãy cùng xem xét một ví dụ kinh điển nhất trong ứng dụng của phép nhân ma trận.

## Đề bài

[LATGACH4 - Lát gạch 4](https://oj.vnoi.info/problem/latgach4)

Cho một hình chữ nhật kích thước $2 \times N$ $(1 \le N \le 10^9)$. Hãy đếm số cách lát các viên gạch nhỏ kích thước $1 \times 2$ và $2 \times 1$ vào hình trên sao cho không có phần nào của các viên gạch nhỏ thừa ra ngoài, cũng không có vùng diện tích nào của hình chữ nhật không được lát.

## Phân tích

Gọi $F_i$ là số cách lát các viên gạch nhỏ vào hình chữ nhật kích thước $2 \times i$. Ta có:

- Nếu sử dụng viên gạch kích thước $1 \times 2$ thì $F_i = F_{i - 2}$.
- Nếu sử dụng viên gạch kích thước $2 \times 1$ thì $F_i = F_{i - 1}$.

$\Rightarrow$ $F_i = F_{i - 1} + F_{i - 2}$.

![](https://i.imgur.com/TVx8hZ2.png)

Do đó, bài toán quy về tìm số $Fibonacci$ thứ $N$ với dãy $Fibonacci$ được định nghĩa như sau:

> $F_0 = 1$
> $F_1 = 1$
> $...$
> $F_i = F_{i-1} + F_{i-2}$ (với $i \ge 2$)

Hiển nhiên cách làm thông thường là tính lần lượt các $F_i$. Tuy nhiên, cách làm này hoàn toàn không hiệu quả với $N$ lên đến $10^9$, và ta cần một cách tiếp cận khác.

Ta xét các lớp số:

- Lớp $1$: $F_1, F_0$
- Lớp $2$: $F_2, F_1$
- Lớp $3$: $F_3, F_2$
- $...$
- Lớp $i-1$: $F_{i-1}, F_{i-2}$
- Lớp $i$: $F_{i}, F_{i-1}$

Ta hình dung mỗi lớp là một ma trận $(2 \times 1)$. Tiếp đó, ta sẽ biến đổi từ lớp $i-1$ đến lớp $i$. Sau mỗi lần biến đổi như vậy, ta tính thêm được một giá trị $F_i$. Để thực hiện phép biến đổi này, chú ý là các số ở lớp sau chỉ phụ thuộc vào lớp ngay trước nó theo các phép cộng, ta tìm được cách biến đổi bằng nhân ma trận:

$A \times \begin{bmatrix} F_{i-1} \\ F_{i-2} \end{bmatrix} = \begin{bmatrix} F_i \\ F_{i-1} \end{bmatrix}$

Chắc hẳn đọc đến đây bạn đọc sẽ thắc mắc, làm thế nào để tìm được ma trận $A$ ? Để tìm được ma trận này, ta làm như sau:

$A = \begin{bmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{bmatrix}$

$\Rightarrow$ $\begin{bmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{bmatrix} \begin{bmatrix} F_{i-1} \\ F_{i-2} \end{bmatrix} = \begin{bmatrix} F_i \\ F_{i-1} \end{bmatrix}$

Suy ra:

- $F_i = a_{11} \times F_{i-1} + a_{12} \times F_{i-2} = 1 \times F_{i-1} + 1 \times F_{i-2}$, do đó hàng đầu của ma trận $A$ là $\begin{bmatrix} 1 & 1 \end{bmatrix}$.
- $F_{i-1} = a_{21} \times F_{i-1} + a_{22} \times F_{i-2} = 1 \times F_{i-1} + 0 \times F_{i-2}$, do đó hàng thứ hai của ma trận $A$ là $\begin{bmatrix} 1 & 0 \end{bmatrix}$.

$\Rightarrow A = \begin{bmatrix} 1 & 1 \\ 1 & 0 \end{bmatrix}$

Ta có:

$\begin{bmatrix} F_i \\ F_{i-1} \end{bmatrix} = A \times \begin{bmatrix} F_{i-1} \\ F_{i-2} \end{bmatrix} = A^2 \times \begin{bmatrix} F_{i-2} \\ F_{i-3} \end{bmatrix}$ $\Bigg($vì $\begin{bmatrix} F_{i-1} \\ F_{i-2} \end{bmatrix} = A \times \begin{bmatrix} F_{i-2} \\ F_{i-3} \end{bmatrix}$ $\Bigg)$

$= A^3 \times \begin{bmatrix} F_{i-3} \\ F_{i-4} \end{bmatrix} = ... = A^{i-1} \times \begin{bmatrix} F_1 \\ F_0 \end{bmatrix}$

$\Rightarrow \begin{bmatrix} F_N \\ F_{N-1} \end{bmatrix} = A^{N-1} \times \begin{bmatrix} F_1 \\ F_0 \end{bmatrix} = \begin{bmatrix} 1 & 1 \\ 1 & 0 \end{bmatrix} ^{N-1} \times \begin{bmatrix} 1 \\ 1 \end{bmatrix}$ (vì $F_0 = 1$ và $F_1 = 1$)

Vậy bài toán trên được đưa về dạng **nhân ma trận**. $F_N$ được tính dựa vào phép lũy thừa của ma trận $A$    .

## Cài đặt

``` cpp=
#include <bits/stdc++.h>

using namespace std;

struct matrix {
    static const int sizeMatrix = 100;
    static const long long mod  = 111539786;
    int row, column;
    long long a[sizeMatrix][sizeMatrix];

    long long* operator[] (int i) { return a[i]; }

    matrix identityMatrix(int n) {
        matrix tmp(n, n);
        for (int i = 1; i <= n; ++i) tmp[i][i] = 1;
        return tmp;
    }

    void operator = (matrix b) {
        row = b.row, column = b.column;
        for (int i = 1; i <= b.row; ++i)
            for (int j = 1; j <= b.column; ++j) a[i][j] = b[i][j];
    }

    matrix operator * (matrix b) {
        matrix c(row, b.column);
        for (int i = 1; i <= row; ++i)
            for (int j = 1; j <= b.column; ++j)
                for (int k = 1; k <= column; ++k) {
                    c[i][j] += (a[i][k] % mod) * (b[k][j] % mod) % mod;
                    c[i][j] %= mod;
                }
        return c;
    }

    matrix power(matrix tmp, int k) {
        if (k == 0) return identityMatrix(column);
        if (k == 1) return tmp;
        matrix p = power(tmp, k / 2);
        p = p * p;
        if (k & 1) return p * tmp;
        return p;
    }
    
    matrix operator ^ (int k) {
        matrix tmp(row, column);
        for (int i = 1; i <= row; ++i)
            for (int j = 1; j <= column; ++j) tmp[i][j] = a[i][j];
        return power(tmp, k);
    }

    void clear(int m, int n) { 
        row = m, column = n; 
        for (int i = 1; i <= row; ++i) 
            fill_n(a[i], column + 1, 0); 
    }
    matrix (int m, int n) { clear(m, n); }
};

void coutMatrix(matrix a) {
    for (int i = 1; i <= a.row; ++i) {
        for (int j = 1; j <= a.column; ++j) cout << a[i][j] << ' ';
        cout << '\n';
    }
}

int main(){
    matrix a(2, 2);
    a[1][1] = 1; a[1][2] = 1;
    a[2][1] = 1; a[2][2] = 0;

    int t;
    cin >> t;
    while (t--) {
        int n;
        cin >> n;
        matrix tmp = a ^ (n - 1);
        cout << (tmp[1][1] + tmp[1][2]) % 111539786 << '\n';
    }
}
```
## Đánh giá

**Độ phức tạp**

Độ phức tạp của thuật toán là $O(T \times 2^3 \times logN)$. Với $T$ là số lượng bộ test.

# Ví dụ 2

Bây giờ chúng ta sẽ cùng xem xét một ví dụ tổng quát hơn của **ví dụ 1**.

## Đề bài

[SPOJ - SEQ](http://www.spoj.com/problems/SEQ)

Cho số nguyên $N$ $(N \le 100)$ và 2 dãy số độ dài $N$: $a_1, a_2, ..., a_N$; $b_1, b_2, ..., b_N$. Dãy số $c$ được định nghĩa như sau:

- $c_i = a_i$ với $i \le N$
- $c_i = c_{i-1} \times b_1 + c_{i-2} \times b_2 + ... + c_{i-N} \times b_N$

Yêu cầu: Tính $c_k$ với $k \le 10^9$.

## Phân tích

Cũng như trong ví dụ 1, ta xét các lớp số:

- Lớp 1: $c_1, c_2, ..., c_N$
- Lớp 2: $c_2, c_3, ..., c_{N+1}$
- ...
- Lớp $i$: $c_i, c_{i+1}, ..., c_{i+N-1}$

Ta cũng sẽ áp dụng phép nhân ma trận để biến đổi từ lớp $i$ sang lớp $i+1$ như sau:

![](https://sites.google.com/site/ngthanhtrung23/_/rsrc/1401391791677/algorithm/matrix-multiplication/p2.PNG?height=256&width=320)

Để xây dựng ma trận vuông như trên, ta thực hiện tương tự như trong ví dụ trước: Phân tích $a_{i+1}$ đến $a_{i+N}$ dưới dạng $a_i, ..., a_{i+N-1}$:

- $a_{i+1} = 0 * a_i + 1 * a_{i+1} + ... + 0 * a_{i+N-1}$ nên hàng 1 là $0, 1, 0, ...., 0$
- ...
- $a_{i+N-1} = 0 * a_i + 0 * a_{i+1} + ... + 1 * a_{i+N-1}$ nên hàng $N-1$ là $0, 0, 0, ..., 1$
- $a_{i+N} = b_N * a_i + b_{N-1} * a_{i+1} + ... + b_1 * a_{i+N-1}$ nên hàng $N$ là $b_N, b_{N-1}, ..., b_1$

Từ đó, ta thu được cách làm như trong ví dụ 1. Cài đặt cụ thể xin nhường lại cho bạn đọc.

Chú ý rằng ta hoàn toàn có thể thay thế phép nhân và phép cộng trong định nghĩa phép nhân ma trận, chỉ cần đảm bảo giữ nguyên tính chất kết hợp. Cụ thể hơn, thay vì $C(i,j) = \sum{A(i,k) * B(k,j)}$, ta có thể định nghĩa phép nhân ma trận: $C(i,j) = min(A(i,k) + B(k,j))$. Từ đó, ta có thể thu được một lớp các bài toán khác.

Sau đây là một ví dụ minh hoạ cho nhóm các bài toán này

# Ví dụ 3

**Bài toán**

Cho đồ thị có hướng $N$ đỉnh $(N \le 100)$. Tính ma trận $C(k)$ kích thước $N \times N$, với $C(k) [i,j]$ là độ dài đường đi ngắn nhất từ $i$ đến $j$ đi qua đúng $k$ cạnh

**Phân tích**

Xét ma trận $A$ là ma trận kề của đồ thị đã cho. Ta có:

- $A = C(1)$
- $C(2)[i,j] = \min{A[i,u] + A[u,j]}$ với $u$ chạy từ 1 đến $N$
- $C(k)[i,j] = \min{C(k-1)[i,u] + A[u,j]}$ với $u$ chạy từ 1 đến $N$

Như vậy, nếu ta thay phép nhân và phép cộng trong việc nhân ma trận thông thường lần lượt bởi phép cộng và phép lấy min, ta thu được một phép ”nhân ma trận” mới, tạm dùng ký hiệu `x`, thì:

```
C1 = A
C2 = C1 x C1 = A x C1
C3 = C1 x C2 = A x C2
C4 = C1 x C3 = A x C3
...
Ck = C1 x C(k-1) = A x C(k-1)
```

Do đó, $C(k) = A^k$

Như vậy, bài toán được đưa về bài toán tính lũy thừa của một ma trận, ta hoàn toàn có thể giải tương tự các ví dụ trước. Cài đặt phép nhân ma trận mới này hoàn toàn không phức tạp hơn cài đặt phép nhân ma trận thông thường. Việc cài đặt xin nhường lại cho bạn đọc.

# Ví dụ 4

[VNOJ - THBAC](https://oj.vnoi.info/problem/thbac/)

**Bài toán**

Người ta mới tìm ra một loại vi khuẩn mới. Chúng sống thành $N$ bầy $(N \le 100)$, đánh số từ 0 đến $N-1$. Ban đầu, mỗi bầy này chỉ có một con vi khuẩn. Tuy nhiên, mỗi giây, số lượng vi khuẩn trong các bầy lại có sự thay đổi. Ví dụ:

- một bầy có thể bị chết đi
- số lượng vi khuẩn trong một bầy có thể tăng lên
- một bầy có thể di chuyển vị trí.

Các thay đổi này tuân theo một số quy luật cho trước. Tại mỗi giây chỉ xảy ra đúng một quy luật. Các quy luật này được thực hiện nối tiếp nhau và theo chu kỳ. Có nghĩa là, nếu đánh số các quy luật từ 0 đến $M-1$, tại giây thứ $S$ thì quy luật được áp dụng sẽ là $(S-1) \space mod \space M$ $(M \le 1000)$

Nhiệm vụ của bạn là tìm xem, với một bộ các quy luật cho trước, sau $T$ đơn vị thời gian $(T \le 10^{18})$, mỗi bầy có bao nhiêu vi khuẩn.

Các loại quy luật có thể có:

- `A i 0`: Tất cả các vi khuẩn thuộc bầy $i$ chết.
- `B i k`: Số vi khuẩn trong bầy $i$ tăng lên $k$ lần.
- `C i j`: số vi khuẩn bầy thứ $i$ tăng lên một số lượng bằng với số vi khuẩn bầy $j$.
- `D i j`: Các vi khuẩn thuộc bầy $j$ di chuyển toàn bộ sang bầy $i$.
- `E i j`: Các vi khuẩn thuộc bầy $i$ và bầy $j$ đổi vị trí cho nhau.
- `F 0 0`: Vị trí các vi khuẩn di chuyển trên vòng tròn.

**Phân tích**

Cách làm đơn giản nhất là chúng ta mô phỏng lại số lượng vi khuẩn trong mỗi bầy qua từng đơn vị thời gian. Cách làm này có độ phức tạp $\mathcal{O}(T \times N \times k)$ với $\mathcal{O}(k)$ là độ phức tạp cho xử lý số lớn. Cách này không thể chạy được với $T$ lớn.

Ta hình dung số lượng vi khuẩn trong mỗi bầy trong một đơn vị thời gian là một dãy số. Như vậy, mỗi quy luật cho trước thực chất là một phép biến đổi từ một dãy số thành một dãy số mới, và ta hoàn toàn có thể thực hiện biến đổi này bằng một phép nhân ma trận.

Cụ thể hơn, ta coi số lượng vi khuẩn trong $N$ bầy tại một thời điểm xác định là một ma trận $1 \times N$, và mỗi phép biến đổi là một ma trận $N \times N$. Khi áp dụng mỗi phép biến đổi, ta nhân hai ma trận nói trên với nhau.

Bây giờ, xét trường hợp $N = 4$, tôi xin lần lượt mô tả các ma trận tương ứng với các phép biến đổi:

- Biến đổi: `A 2 0`
  ```
  1 0 0 0
  0 1 0 0
  0 0 0 0
  0 0 0 1
  ```

- Biến đổi: `B 2 6`
  ```
  1 0 0 0
  0 1 0 0
  0 0 6 0
  0 0 0 1
  ```

- Biến đổi: `C 1 3`
  ```
  1 0 0 0
  0 1 0 0
  0 0 1 0
  0 1 0 1
  ```

- Biến đổi: `D 1 3`
  ```
  1 0 0 0
  0 1 0 0
  0 0 1 0
  0 1 0 0
  ```

- Biến đổi: `E 1 3`
  ```
  1 0 0 0
  0 0 0 1
  0 0 1 0
  0 1 0 0
  ```

- Biến đổi: `F 0 0`
  ```
  0 1 0 0
  0 0 1 0
  0 0 0 1
  1 0 0 0
  ```

Cũng như các bài toán trước, ta sẽ cố gắng áp dụng việc tính toán lũy thừa, kết hợp với phép nhân ma trận để giảm độ phức tạp từ $T$ xuống $\log{T}$. Tuy nhiên, có thể thấy việc sử dụng phép lũy thừa trong bài toán này phần nào phức tạp hơn bởi các ma trận được cho không giống nhau. Để giải quyết vấn đề này, ta làm như sau:

Gọi $X_1, X_2, ..., X_m$ là các ma trận tương ứng với các phép biến đổi được cho.

Đặt $X = X_1 \times X_2 \times ... \times X_m$.

Đặt $S = [1, 1, ..., 1]$ (dãy số lượng vi khuẩn tại thời điểm đầu tiên).

Như vậy, $Y = S \times X^t \times X_1 \times X_2 \times ... \times X_r$ là ma trận thể hiện số lượng vi khuẩn tại thời điểm $M \times t + r$.

Như vậy, thuật toán đến đây đã rõ. Ta phân tích $T = M \times t + r$, nhờ đó, ta có thể giải quyết bài toán trong $\mathcal{O}(N^3 \times M)$ cho bước tính ma trận $X$ và $\mathcal{O}(N^3 \times (\log{T/M} + M)$ cho bước tính $Y$. Bài toán được giải quyết.

# Phép toán kết hợp và độ phức tạp tính toán

## Nhân tổ hợp dãy ma trận
Trong phần [Mở Đầu](http://vnoi.info/contributor/preview#mở-đầu) ta đã có thuật toán nhân hai ma trận $A$ kích cỡ $M * N$ và $B$ kích cỡ $N * P$ cần độ phức tạp $O(M * N * P)$. Giả sử ta có thêm ma trận $C$ có kích cỡ $P * Q$ và ta cần tính tích $A * B * C$. Xét hai cách thực hiện phép nhân này:

- *Cách 1*: $(A * B) * C$ thực hiện nhân $A$ và $B$ rồi nhân với $C$ cần độ phức tạp $O(M * N * P) + O(M * P * Q) = O(M * P * (N + Q))$
- *Cách 2*: $A * (B * C)$ thực hiện nhân $B$ và $C$ rồi nhân với $A$ cần độ phức tạp $O(N * P * Q) + O(M * N * Q) = O(N * Q * (M + P))$

Như vậy là hai cách thực hiện khác nhau cần hai độ phức tạp khác nhau. Chọn $M = N = 500, P = 1000, Q = 2$, cách 1 sẽ cần tới $500 * 1000 * (500 + 2) = 251 * 10^6$ phép tính, trong khi cách 2 chỉ cần $500 * 2 * (500 + 1000) = 1.5 * 10^6$ phép tính, nghĩa là cách 1 chậm hơn cách 2 tới gần 200 lần.

Khi độ dài của dãy ma trận tăng lên, sự khác biệt có thể còn lớn hơn nữa. Ví dụ trên đã cho thấy rằng trong một số trường hợp thứ tự thực hiện phép nhân ma trận có ý nghĩa rất lớn đối với việc tìm lời giải của các bài toán.

Trong thực tế, bài toán xác định thứ tự nhân ma trận hiệu quả nhất là một bài toán rất phổ biến, bạn có thể tìm đọc chi tiết thêm ở [Mục 3.5 Phép Nhân Tổ Hợp dãy Ma Trận trong ebook của thầy Lê Minh Hoàng](http://cntt.epu.edu.vn/images/book_LeMinhHoang.pdf).

## Giải thuật Freivalds kiểm tra tích hai ma trận
[Giải thuật Freivalds](https://courses.cs.washington.edu/courses/cse525/13sp/scribe/lec1.pdf) là một ví dụ điển hình về việc áp dụng thứ tự thực hiện phép nhân ma trận để giảm độ phức tạp tính toán của phép nhân một dãy ma trận. Bài toán đặt ra là cho ba ma trận vuông $A, B, C$ có kích cỡ $N * N$ với $N \le 1000$. Ta cần kiểm tra xem $C$ có phải là tích của $A$ và $B$, nói cách khác ta cần kiểm tra $A*B = C$ có phải là mệnh đề đúng hay không (đây chính là bài [VMATRIX - VNOI Marathon 2014](https://oj.vnoi.info/problem/vmatrix/)).

**Phân tích**

Cách làm thông thường là nhân trực tiếp hai ma trận $A, B$ rồi so sánh kết quả với $C$. Như phân tích trong phần [Mở Đầu](http://vnoi.info/contributor/preview#mở-đầu) độ phức tạp của cách làm này là $O(N^3)$, với $N = 1000$ thì cách làm này không đủ nhanh. Giải thuật Freivalds thực hiện việc kiểm tra thông qua thuật toán xác suất kiểu Monte Carlo với $k$ lần thử cho xác suất kết luận sai là xấp xỉ $1 / 2^k$, mỗi lần thử có độ phức tạp $O(N^2)$. Các bước cơ bản của một phép thử Freivalds như sau:

1. Sinh ngẫu nhiên một ma trận $v$ kích cỡ $N * 1$ với các phần tử chỉ nhận giá trị $0$ hoặc $1$.
2. Tính hiệu $P = A * B * v - C * v$. Dễ thấy rằng $P$ là ma trận kích cỡ $N * 1$.
3. Trả về `True` nếu $P$ chỉ gồm phần tử $0$ (bằng với vector $0$) và `False` nếu ngược lại. 

Ta thực hiện $k$ lần thử, nếu gặp phép thử trả về `False` thì ta kết luận là $A * B \neq C$. Ngược lại nếu sau $k$ phép thử mà luôn thấy `True` thì ta kết luận $A * B = C$. Vì xác suất lỗi giảm theo hàm mũ của $k$ nên thông thường chỉ cần chọn $k$ vừa đủ là sẽ thu được xác suất đúng rất cao ($k = 5$ với bài **VMATRIX** ở trên). Một nhận xét quan trọng khác là cận trên của đánh giá xác suất kiểm tra lỗi không phụ thuộc vào kích cỡ $N$ của ma trận được cho mà chỉ phụ thuộc vào số lần thực hiện phép thử.

Xét bước thứ 2, ta thấy rằng phép thử Freivalds chỉ có ý nghĩa nếu như ta có thể thực hiện phép nhân $A * B * v$ trong thời gian $O(N^2)$ (vì phép nhân $C * v$ đã đạt sẵn $O(N^2)$ rồi). Thay vì thực hiện tuần tự từ trái qua phải sẽ cần $O(N^3)$, ta thực hiện theo thứ tự $A * (B * v)$. Vì kết quả của phép nhân $B$ và $v$ là một ma trận $N * 1$ nên độ phức tạp tổng cộng sẽ là $O(N^2)$. Trên tất cả các phép thử, độ phức tạp là $O(k * N^2)$. 

# Bài tập áp dụng

[HackerEarth - PK and interesting language](https://www.hackerearth.com/problem/algorithm/pk-and-interesting-language/description/)

[HackerEarth - Long walks from Office to Home Sweet Home](https://www.hackerearth.com/problem/algorithm/long-walks-from-office-to-home-sweet-home-1/)

[HackerEarth - Tiles](https://www.hackerearth.com/problem/algorithm/tiles/)

[HackerEarth - ABCD Strings](https://www.hackerearth.com/problem/algorithm/abcd-strings/description/)

[HackerEarth - Mehta and the difficult task](https://www.hackerearth.com/problem/algorithm/mehta-and-the-difficult-task-3/)

[HackerEarth - Mehta and the Evil Strings](https://www.hackerearth.com/problem/algorithm/mehta-and-the-evil-strings/)

[VNOJ - PA06ANT](https://oj.vnoi.info/problem/pa06ANT/)

[VNOJ - CONNECTE](https://oj.vnoi.info/problem/connecte)