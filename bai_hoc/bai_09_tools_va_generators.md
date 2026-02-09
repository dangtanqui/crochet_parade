# Bài 9: Tools và Pattern Generators

## Mục tiêu bài học

Sau bài học này, bạn sẽ:

- Sử dụng Tools → Expand Instructions để debug
- Sử dụng Tools → Simplify Instructions để nén pattern
- Sử dụng Tools → Find Project Periphery để gắn label biên tự động
- Sử dụng Sphere Generator để tạo hình cầu
- Sử dụng Axial Shape Generator để tạo hình trụ/mũ/amigurumi
- Sử dụng Object Transform để di chuyển/xoay các mảnh rời

## 1. Tools → Expand Instructions

### Mục đích

**"Bung" pattern ra** để:

- Debug từng mũi cụ thể
- Chỉnh sửa individual stitches
- Chuẩn bị cho Find Periphery

### Chức năng

**Expand làm gì:**

- `3*[sc,dc]` → `[sc,dc],[sc,dc],[sc,dc]`
- `4sc` → `sc,sc,sc,sc`
- `$k=0$; sc.A[k++]*3` → `sc.A[0],sc.A[1],sc.A[2]`
- Thay thế DEF (nếu có thể)

### Cách sử dụng

1. **Tools → Expand Instructions**
2. Chọn options:
   - `Substitute index counters?` → ✅ (tính counters)
   - `Run twice?` → ✅ (bung hoàn toàn + enable cross-highlighting)
3. Trả lời câu hỏi toán (chống nhầm lẫn)
4. Click OK

### Ví dụ

**Trước:**

```
$k=0$
[3sc.A[k++]]*3
```

**Sau expand (run twice, substitute counters):**

```
sc.A[0],sc.A[0],sc.A[0],sc.A[1],sc.A[1],sc.A[1],sc.A[2],sc.A[2],sc.A[2]
```

### Khi nào dùng?

✅ **Dùng khi:**

- Debug pattern (mũi nào sai?)
- Chỉnh sửa từng mũi cụ thể
- Trước khi dùng Find Periphery
- Cross-highlighting: Ctrl+Click mũi trong editor → highlight trong 3D

⚠️ **Cảnh báo:** Expand **ghi đè** code hiện tại! Lưu backup trước!

## 2. Tools → Simplify Instructions

### Mục đích

**"Nén" pattern lại** sau khi expand và chỉnh sửa.

### Chức năng

**Simplify làm gì:**

- `[sc,dc],[sc,dc],[sc,dc]` → `3*[sc,dc]`
- `sc.A[0],sc.A[1],sc.A[2]` → `$k=0$; [sc.A[k++]]*3`

### Cách sử dụng

1. **Tools → Simplify Instructions**
2. Chọn options:
   - `Expand before simplification?` → ✅ (khuyên dùng)
   - `Simplify numerical indexing?` → ✅ (tạo counters)
3. Trả lời câu hỏi toán
4. Click OK

### Ví dụ

**Trước:**

```
sc,sc,sc,dc,dc,dc,sc,sc,sc,dc,dc,dc
```

**Sau simplify:**

```
[3sc,3dc]*2
```

### Khi nào dùng?

✅ **Dùng khi:**

- Sau khi expand và chỉnh sửa xong
- Pattern dài, nhiều lặp lại
- Cần chia sẻ pattern (gọn hơn)

⚠️ **Experimental!** Có thể sinh code không tối ưu.

## 3. Tools → Find Project Periphery ⭐⭐⭐

### Mục đích

**Tìm biên** (periphery/border) của project và **gắn label tự động**.

### Vấn đề cần giải quyết

Khi móc biên/viền:

- Các mũi trên biên **không liên tiếp** trong code
- Thứ tự móc ≠ thứ tự biên

**Ví dụ:** Móc vuông, các mũi biên:

- Hàng 0: mũi 0-9 (đáy)
- Hàng 1: mũi 9 (cạnh phải)
- ...
- Hàng 10: mũi 0-9 (đỉnh)

→ Không liên tiếp!

### Chức năng

**Find Periphery làm gì:**

- Tìm **đường biên** (edge graph)
- **Sắp xếp** mũi theo thứ tự biên
- **Gắn labels** tự động theo thứ tự biên
- Tạo `INDEX_ARRAY` hoặc `SORT_LABEL`

### Workflow

1. **Calculate** project (shift+Enter)
2. **Tools → Expand instructions** (run twice, recommended)
3. **Tools → Find Project Periphery**
4. Chọn **Periphery candidate** từ dropdown
5. (Optional) **Custom periphery editor** nếu không đúng
6. **Apply label**: Nhập template (ví dụ: `Border[k++]`)
7. Chọn options:
   - `Evaluate counter?` → ✅
   - `Start:` → 0 (hoặc giá trị bắt đầu)
   - `Save counter values as INDEX_ARRAY?` → ✅ (khuyên dùng)

### Ví dụ

**Trước:**
```
10ch,turn
[9sc,turn
]*9
9sc
```

**Sau Find Periphery + Apply label `Border[k]`:**

```
INDEX_ARRAY: k = {36, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 17, 16, 28, 29, 15, 14, 30, 31, 13, 12, 32, 33, 11, 10, 34, 35, 9, 8, 7, 6, 5, 4, 3, 2, 1, 0}
10*[ch.A[k]],9*[turn
sc.A[k],7sc,sc.A[k]],turn
9*[sc.A[k]]
```

→ Biên được đánh số theo thứ tự liên tiếp!

### Custom Periphery Editor

Nếu tự động không đúng:

1. Click **Edit edges**
2. Nhập edges thủ công: `stitch1 -- stitch2`
3. Hoặc Alt+Click trên 3D canvas
4. Save

### Khi nào dùng?

✅ **Dùng khi:**

- Móc biên/viền (edging, border)
- Ráp mảnh (joining motifs)
- Lace phức tạp
- Filet crochet

## 4. Pattern Generators

### 4.1. Generate a Sphere

**Mục đích:** Tạo hình cầu tự động (amigurumi head, ball...)

#### Cách sử dụng

1. Dropdown menu → **Generate a sphere**
2. Chọn:
   - `Circumference (in stitches):` → Chu vi (6-1200)
   - `Scatter increases and decreases?` → ✅ (phân bố đều hơn)
3. Click Generate

#### Kết quả

```
# Ví dụ: Circumference = 36
ring
sc5inc
3sc2inc,sc3inc,sc2inc
sc,2*[sc2inc,sc],sc2inc,2sc,sc2inc,sc,sc2inc
sc2inc,4*[2sc,sc2inc],3sc
3sc,2*[sc2inc,4sc],sc2inc,5sc,sc2inc,sc
2sc,2*[sc2inc,5sc],sc2inc,6sc,sc2inc,3sc
3sc,2*[sc2inc,9sc],sc2inc,5sc
sc2inc,15sc,sc2inc,15sc
28sc,sc2inc,5sc
23sc,sc2inc,11sc
17sc,sc2tog,17sc
sc2tog,33sc
13sc,sc2tog,15sc,sc2tog,2sc
5sc,2*[sc2tog,9sc],sc2tog,3sc
sc2tog,2*[5sc,sc2tog],6sc,sc2tog,5sc
sc2tog,3*[4sc,sc2tog],5sc
2sc,3*[sc2tog,2sc],sc2tog,3sc,sc2tog
sc2tog,3*[sc,sc2tog],2sc,sc2tog,sc
sc2tog,sc3tog,3sc2tog
sc5tog
```

→ Hình cầu hoàn hảo!

### 4.2. Generate Axially Symmetric Shape

**Mục đích:** Tạo hình trụ/mũ/amigurumi body bằng cách vẽ profile.

#### Cách sử dụng

1. Dropdown menu → **Generate an axially symmetric shape**
2. **Vẽ profile curve:**
   - Drag control points
   - Right-click → Add/Delete points
3. Chọn options:
   - `Scatter increases/decreases?` → ✅
   - `Number of stitches between green grid lines:` → Điều chỉnh scale
   - `Adjust thickness curve?` → ✅ (nếu cần)
4. Click Generate

#### Ví dụ applications

**Mũ beanie:**
- Profile: Nửa hình cầu trên, hình trụ dưới

**Thân amigurumi:**
- Profile: Hình giọt nước hoặc oval

**Túi:**
- Profile: Hình trụ với đáy tròn

### Export/Import curve

- **Export:** Lưu curve definition (JSON)
- **Import:** Load curve đã lưu

→ Tái sử dụng shapes!

## 5. Object Transform

### Mục đích

Di chuyển và xoay **các mảnh rời** (disjoint objects) để xem trước khi ráp.

**Ví dụ:** Amigurumi với tay, chân, đầu, thân rời nhau.

### Cách sử dụng

1. **Tools → Object Transform**
2. Chọn **Object number**
3. Điều chỉnh:
   - **Translation (x,y,z):** Di chuyển
   - **Rotation (alpha,beta,gamma):** Xoay
4. **Write to instructions:** Lưu vào code

### Kết quả trong code

```
TRANSFORM_OBJECT: 1,5.2,3.1,-2.0,0.5,1.2,0.0
```

**Giải thích:**
- Object 1
- Translation: (5.2, 3.1, -2.0)
- Rotation: (0.5, 1.2, 0.0) radians

### Khi nào dùng?

✅ **Dùng khi:**

- Amigurumi nhiều mảnh
- Appliqués
- Irish crochet (ráp motifs)

## 6. Các Tools khác

### DOT: command

Điều chỉnh physics engine:

```
DOT: iterations=1000       # Số lần tính toán
DOT: start=10              # Random seed
DOT: separate=1.5          # Khoảng cách giữa objects
DOT: inflate=2.0           # "Phồng" project
DOT: learning_rate=0.1     # Tốc độ hội tụ
```

### COLOR và BACKGROUND

```
COLOR: Blue               # Màu len
COLOR: rgb(126,8,80)      # RGB custom
BACKGROUND: White         # Màu nền
```

## Bài tập thực hành

### Bài tập 1: Expand và Simplify

**Yêu cầu:**

1. Viết pattern: `[3sc,2dc]*5`
2. Expand (run twice)
3. Chỉnh sửa: Thay dc thứ 3 thành hdc
4. Simplify lại

<details>
<summary>Đáp án</summary>

**Bước 1:**
```
[3sc,2dc]*5
```

**Bước 2 (Expand):**
```
3sc,2dc,3sc,2dc,3sc,2dc,3sc,2dc,3sc,2dc
```

**Bước 3 (Chỉnh sửa):**
```
3sc,2dc,3sc,hdc,dc,3sc,2dc,3sc,2dc,3sc,2dc
```

**Bước 4 (Simplify):**
```
3sc,2dc,3sc,hdc,dc,[3sc,2dc]*3
```

</details>

### Bài tập 2: Find Periphery (Lý thuyết)

**Yêu cầu:** Giải thích khi nào cần Find Periphery?

<details>
<summary>Đáp án</summary>

**Cần khi:**

1. Móc biên/viền cho khăn, chăn
2. Ráp mảnh (granny squares, motifs)
3. Lace có thứ tự móc phức tạp
4. Pick up stitches dọc cạnh hàng

**Không cần khi:**

- Pattern đơn giản, móc theo thứ tự
- Móc vòng tròn đơn giản
- Không cần labels biên

</details>

### Bài tập 3: Generate Sphere

**Yêu cầu:** Tạo hình cầu circumference 30, explain structure.

<details>
<summary>Đáp án</summary>

**Generate → Circumference: 30**

**Kết quả (approximate):**
```
ring
sc5inc
3sc2inc,sc3inc,sc2inc
sc,2*[sc2inc,sc],sc2inc,2sc,sc2inc,sc,sc2inc
sc2inc,4*[2sc,sc2inc],3sc
5sc,2*[sc2inc,6sc],sc2inc,sc
4sc,2*[sc2inc,7sc],sc2inc,3sc
4sc,sc2inc,13sc,sc2inc,8sc
sc2inc,28sc
24sc,sc2tog,4sc
7sc,sc2tog,13sc,sc2tog,5sc
2sc,2*[sc2tog,7sc],sc2tog,5sc
sc2tog,2*[6sc,sc2tog],6sc
2sc,3*[sc2tog,2sc],sc2tog,3sc,sc2tog
sc2tog,3*[sc,sc2tog],2sc,sc2tog,sc
sc2tog,sc3tog,3sc2tog
sc5tog
```

</details>

## Tổng kết bài học

Trong bài 9, bạn đã học:

✅ **Expand Instructions:** Bung pattern để debug  
✅ **Simplify Instructions:** Nén pattern sau chỉnh sửa  
✅ **Find Project Periphery:** Tìm biên tự động ⭐  
✅ **Sphere Generator:** Tạo hình cầu  
✅ **Axial Shape Generator:** Tạo hình trụ/mũ/body  
✅ **Object Transform:** Di chuyển/xoay objects  

### Workflow điển hình

**1. Thiết kế pattern:**
- Viết pattern compact (dùng `*`, counters)

**2. Debug:**
- Expand (run twice)
- Cross-highlight (Ctrl+Click)
- Chỉnh sửa từng mũi

**3. Chia sẻ:**
- Simplify
- Lưu backup

**4. Móc biên:**
- Find Periphery
- Apply labels
- Móc viền

### Best practices

✅ **Nên:**
- **Lưu backup** trước khi Expand/Simplify
- Dùng Find Periphery cho bất kỳ project nào cần biên
- Dùng Generators cho shapes chuẩn (sphere, cylinder)
- Export/Import curves để tái sử dụng

❌ **Không nên:**
- Expand pattern đơn giản (không cần)
- Quên lưu trước khi dùng tools (ghi đè!)
- Lạm dụng Simplify (có thể tạo code không tối ưu)

## Bài tiếp theo

Trong **Bài 10 (cuối khóa)**, chúng ta sẽ:
- Viết pattern amigurumi hoàn chỉnh
- Filet crochet
- Irish crochet và lace
- Troubleshooting và debugging
- Best practices tổng hợp

---

**Lưu ý cho giảng viên:**
- Demo live các tools (quan trọng nhất!)
- Nhấn mạnh: **Lưu backup trước khi dùng tools**
- Find Periphery là tool **hữu ích nhất** cho patterns phức tạp
- Generators tiết kiệm thời gian cho shapes chuẩn
- Khuyến khích học viên thử nghiệm tools trên patterns mẫu
