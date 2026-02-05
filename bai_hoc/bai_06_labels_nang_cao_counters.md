# Bài 6: Labels Nâng cao với Counters

## Mục tiêu bài học

Sau bài học này, bạn sẽ:
- Hiểu và sử dụng counters (biến đếm): `$k=0$`
- Tăng/giảm counter: `k++`, `++k`, `k--`, `--k`
- Tạo indexed labels tự động với counters
- Sử dụng `INDEX_ARRAY` để định nghĩa thứ tự tùy chỉnh
- Counter arithmetic: `(k++)%6`, `k*2+1`

## 1. Counter là gì?

### Khái niệm

**Counter** (biến đếm) = **biến số** tự động tăng/giảm, dùng để tạo labels động.

**Vấn đề cần giải quyết:**

```
# Viết tay nhiều labels - mệt!
sc.A[0],sc.A[1],sc.A[2],sc.A[3],sc.A[4]
```

**Giải pháp với counter:**

```
$k=0$
[sc.A[k++]]*5
```

→ Tự động tạo: `sc.A[0],sc.A[1],sc.A[2],sc.A[3],sc.A[4]`

## 2. Khởi tạo counter: `$k=0$`

### Cú pháp

```
$tên_biến=giá_trị$
```

**Ví dụ:**
```
$k=0$        # Khởi tạo k = 0
$m=1$        # Khởi tạo m = 1
$index=10$   # Khởi tạo index = 10
```

### Quy tắc

- Đặt **ở đầu dòng** hoặc **đầu expression**
- Tên biến: chữ cái, số, underscore
- Giá trị: số nguyên (dương/âm/0)

### Ví dụ

```
$k=0$
sc.A[k]*3
```

**Kết quả:** `sc.A[0],sc.A[0],sc.A[0]`  
→ Cả 3 mũi đều dùng giá trị k = 0!

## 3. Tăng counter: `k++` và `++k`

### Post-increment: `k++`

**"Dùng giá trị hiện tại, rồi mới tăng"**

```
$k=0$
[sc.A[k++]]*3
```

**Kết quả:** `sc.A[0],sc.A[1],sc.A[2]`

**Giải thích:**
- Mũi 1: Dùng k=0, sau đó tăng k lên 1
- Mũi 2: Dùng k=1, sau đó tăng k lên 2
- Mũi 3: Dùng k=2, sau đó tăng k lên 3

### Pre-increment: `++k`

**"Tăng trước, rồi mới dùng giá trị"**

```
$k=0$
sc.A[++k],sc.A[++k],sc.A[++k]
```

**Kết quả:** `sc.A[1],sc.A[2],sc.A[3]`

**Giải thích:**
- Mũi 1: Tăng k lên 1, dùng k=1
- Mũi 2: Tăng k lên 2, dùng k=2
- Mũi 3: Tăng k lên 3, dùng k=3

### So sánh `k++` vs `++k`

| | `k++` (Post) | `++k` (Pre) |
|---|---|---|
| **Khởi tạo** | `$k=0$` | `$k=0$` |
| **Giá trị đầu** | 0 | 1 |
| **Khi nào dùng** | Bắt đầu từ 0 | Bỏ qua giá trị đầu |

## 4. Giảm counter: `k--` và `--k`

### Post-decrement: `k--`

```
$k=5$
[sc.A[k--]]*3
```

**Kết quả:** `sc.A[5],sc.A[4],sc.A[3]`

### Pre-decrement: `--k`

```
$k=5$
[sc.A[--k]]*3
```

**Kết quả:** `sc.A[4],sc.A[3],sc.A[2]`

### Từ đồng nghĩa

```
prev k    # = --k (giảm trước)
next k    # = ++k (tăng trước)
```

**Ví dụ:**

```
$k=0$
sc.A[k],sc.A[next k],sc.A[prev k]
```

Tương đương với:

```
$k=0$
sc.A[k],sc.A[++k],sc.A[--k]
```

**Kết quả:** `sc.A[0],sc.A[1],sc.A[0]`

## 5. Counter với block multiplication

### ⚠️ Quy tắc quan trọng

**Cú pháp khác nhau → kết quả khác nhau!**

#### Dạng 1: `N*stitch` (có dấu `*`)

```
$k=0$
3*sc.A[k++]
```

**Phân tích trước → Tăng counter sau:**
1. Phân tích `*` trước: `3*sc.A[k++]` → `sc.A[k++],sc.A[k++],sc.A[k++]`
2. Tăng counter: `sc.A[0],sc.A[1],sc.A[2]`

#### Dạng 2: `Nstitch` (không có dấu `*`)

```
$k=0$
3sc.A[k++]
```

**Tăng counter trước → Phân tích sau:**
1. Tăng counter: `3sc.A[0]`
2. Phân tích `3sc`: `sc.A[0],sc.A[0],sc.A[0]`

#### Dạng 3: `[N]stitch` hoặc `(N)stitch`

```
$k=0$
[3sc].A[k++]
```

**Kết quả:** Giống dạng 2 - `sc.A[0],sc.A[0],sc.A[0]`

### Bảng tổng hợp

| Cú pháp | Kết quả |
|---------|---------|
| `$k=0$; 3*sc.A[k++]` | `sc.A[0],sc.A[1],sc.A[2]` |
| `$k=0$; 3sc.A[k++]` | `sc.A[0],sc.A[0],sc.A[0]` |
| `$k=0$; [3sc].A[k++]` | `sc.A[0],sc.A[0],sc.A[0]` |

💡 **Quy tắc vàng:**
- Muốn tự động tăng → Dùng `*`
- Muốn giữ nguyên → Không dùng `*`

## 6. Counter trong label definition

Counter được đánh giá **trước khi** thay thế definition.

```
$k=0$
DEF: scA=sc@A[k]
5ch,ch.A[0],ch.A[1],ch,turn
$k=1$,sk,3ch,scA
```

**Phân tích:**
1. `scA` thay thế thành literal `sc@A[k]`
2. Đến dòng cuối, `k=1` → `sc@A[1]`
3. Kết quả: sc móc vào `ch.A[1]`

## 7. Counter arithmetic (Phép toán)

### Modulo (chia lấy dư): `%`

```
$k=3$
[sc@A[(k++)%5]]*7
```

**Kết quả:** `sc@A[3],sc@A[4],sc@A[0],sc@A[1],sc@A[2],sc@A[3],sc@A[4]`

**Giải thích:** `k % 5` lấy dư khi chia cho 5
- k=3: 3%5 = 3
- k=4: 4%5 = 4
- k=5: 5%5 = 0
- k=6: 6%5 = 1
- ...

💡 **Dùng khi:** Móc vòng tròn, quay lại label đầu

### Các phép toán khác

```
k+1        # Cộng
k-1        # Trừ
k*2        # Nhân
k/2        # Chia lấy nguyên
k%6        # Chia lấy dư
(k+1)*2    # Kết hợp
```

## 8. INDEX_ARRAY - Thứ tự tùy chỉnh

### Khái niệm

**INDEX_ARRAY** = **mảng giá trị** cho counter, thứ tự không theo số tự nhiên.

**Vấn đề:** Khi móc biên (periphery), thứ tự móc ≠ thứ tự label cần thiết.

### Cú pháp

```
INDEX_ARRAY: tên_biến={giá_trị_1,giá_trị_2,...}
```

**Ví dụ:**
```
INDEX_ARRAY: k={4,3,1,2,0}

5*sc.A[k++]
```

**Kết quả:** `sc.A[4],sc.A[3],sc.A[1],sc.A[2],sc.A[0]`

**Giải thích:**
- Lần 1: Lấy giá trị đầu tiên = 4
- Lần 2: Lấy giá trị thứ 2 = 3
- Lần 3: Lấy giá trị thứ 3 = 1
- ...

### Khi nào dùng INDEX_ARRAY?

✅ **Dùng khi:**
- Thứ tự label không liên tiếp
- Periphery labeling (biên)
- Pattern phức tạp (lace, Irish crochet)

✅ **Ưu điểm:**
- Giữ pattern gọn gàng
- Dễ chỉnh sửa thứ tự
- Kết hợp tốt với Tools → Simplify

## Bài tập thực hành

### Bài tập 1: Counter cơ bản

**Yêu cầu:** Viết pattern với counter:
- 10 chain, mỗi chain gắn label A[0] đến A[9]

<details>
<summary>Đáp án</summary>

```
$k=0$
[ch.A[k++]]*10
```

**Giải thích:**
- `$k=0$`: Khởi tạo k = 0
- `ch.A[k++]`: Mỗi chain dùng k hiện tại, rồi tăng k
- Lặp 10 lần

</details>

### Bài tập 2: `k++` vs `++k`

**Yêu cầu:** Tính kết quả:

**a:** `$k=0$; [sc.A[k++]]*3`  
**b:** `$k=0$; [sc.A[++k]]*3`  

<details>
<summary>Đáp án</summary>

**a:** `sc.A[0],sc.A[1],sc.A[2]`  
**b:** `sc.A[1],sc.A[2],sc.A[3]`  

</details>

### Bài tập 3: Counter với `*` vs không `*`

**Yêu cầu:** Tính kết quả:

**a:** `$k=0$; 3*sc.A[k++]`  
**b:** `$k=0$; 3sc.A[k++]`  

<details>
<summary>Đáp án</summary>

**a:** `sc.A[0],sc.A[1],sc.A[2]` (tăng counter)  
**b:** `sc.A[0],sc.A[0],sc.A[0]` (không tăng)

</details>

### Bài tập 4: Modulo arithmetic

**Yêu cầu:** Viết pattern móc 10 sc, gắn label A[0-5] lặp lại:
- sc.A[0], sc.A[1], ..., sc.A[5], sc.A[0], sc.A[1], ...

<details>
<summary>Đáp án</summary>

```
$k=0$
[sc.A[k++%6]]*10
```

**Kết quả:** `sc.A[0],sc.A[1],sc.A[2],sc.A[3],sc.A[4],sc.A[5],sc.A[0],sc.A[1],sc.A[2],sc.A[3]`

</details>

### Bài tập 5: INDEX_ARRAY

**Yêu cầu:** Sử dụng INDEX_ARRAY để tạo thứ tự: 5, 3, 1, 2, 4

<details>
<summary>Đáp án</summary>

```
INDEX_ARRAY: k={5,3,1,2,4}

[sc.A[k++]]*5
```

**Kết quả:** `sc.A[5],sc.A[3],sc.A[1],sc.A[2],sc.A[4]`

</details>

## Bài tập nâng cao

### Challenge 1: Pattern hoa với counters

**Yêu cầu:** Viết pattern hoa 6 cánh:
- Ring
- Mỗi cánh: 5 chain (Petal[0-5]), ss về ring
- Móc 5 sc vào từng cánh (dùng counter)

<details>
<summary>Đáp án</summary>

```
ring
sc6inc
$k=0$
[5ch.Petal[k],ss@[1,k++]]*6
$m=0$
[5sc@Petal[m++]]*6
```

</details>

### Challenge 2: Complex indexing

**Yêu cầu:** Tạo pattern với thứ tự: 0,2,4,1,3,5
- Dùng INDEX_ARRAY
- Móc 6 sc với labels tương ứng

<details>
<summary>Đáp án</summary>

```
INDEX_ARRAY: k={0,2,4,1,3,5}
$m=0$
6*ch.A[m++],turn
[sc.A[k++]]*6
```

</details>

## Tổng kết bài học

Trong bài 6, bạn đã học:

✅ **Khởi tạo counter:** `$k=0$`  
✅ **Post-increment:** `k++` (dùng rồi tăng)  
✅ **Pre-increment:** `++k` (tăng rồi dùng)  
✅ **Post-decrement:** `k--` (dùng rồi giảm)  
✅ **Pre-decrement:** `--k` (giảm rồi dùng)  
✅ **Arithmetic:** `k%6`, `(k+1)*2`  
✅ **INDEX_ARRAY:** Thứ tự tùy chỉnh  

### Bảng tra cứu nhanh

| Toán tử | Ý nghĩa | Ví dụ | Kết quả (k=0) |
|---------|---------|-------|---------------|
| `k` | Giá trị hiện tại | `.A[k]` | `.A[0]` |
| `k++` | Dùng, rồi tăng | `.A[k++]` | `.A[0]` (k→1) |
| `++k` | Tăng, rồi dùng | `.A[++k]` | `.A[1]` (k→1) |
| `k--` | Dùng, rồi giảm | `.A[k--]` | `.A[0]` (k→-1) |
| `--k` | Giảm, rồi dùng | `.A[--k]` | `.A[-1]` (k→-1) |

### Best practices

✅ **Nên:**
- Dùng counter cho labels lặp lại (>3 lần)
- Dùng `*` khi muốn tự động tăng counter
- Dùng tên biến có ý nghĩa: `k`, `m`, `index`

❌ **Không nên:**
- Lạm dụng counter cho pattern đơn giản
- Quên khởi tạo counter
- Nhầm lẫn giữa `k++` và `++k`

## Bài tiếp theo

Trong **Bài 7**, chúng ta sẽ học:
- Labeled groups nâng cao
- Modifiers: `^` (post), `!` (skip edge), `+` (add edge), `~` (reverse)
- Multiple stitch sets: `@A[;0]`, `@A[;1]`
- `SORT_LABEL`: sắp xếp labels

---

**Lưu ý cho giảng viên:**
- Counter là **khái niệm lập trình**, cần giải thích kỹ cho học viên không biết code
- So sánh `k++` vs `++k` bằng nhiều ví dụ cụ thể
- Nhấn mạnh sự khác biệt giữa `3*sc` và `3sc` khi dùng counter
- INDEX_ARRAY khó, nên để phần cuối và có thể bỏ qua nếu không cần
