# Bài 10: Dự án Thực tế và Tổng kết

## Mục tiêu bài học

Sau bài học này, bạn sẽ:
- Viết pattern amigurumi hoàn chỉnh (đầu, thân, tay, chân, ráp)
- Hiểu filet crochet và cách tạo chart
- Hiểu Irish crochet và cách ráp motifs
- Biết cách debug và troubleshoot
- Áp dụng tất cả kiến thức từ Bài 1-9

## Dự án 1: Amigurumi - Thỏ đơn giản

### Phân tích requirement

**Yêu cầu:**
- Đầu: Hình cầu
- Thân: Hình oval
- Tay: 2 cái, hình trụ nhỏ
- Chân: 2 cái, hình trụ lớn hơn
- Tai: 2 cái, hình dài

### Bước 1: Đầu (Sphere)

```
# Đầu thỏ
COLOR: White

# Dùng Sphere Generator (Circumference: 36)
# Hoặc viết tay:
ring
6sc                    # V1: 6
[sc2inc]*6             # V2: 12
[sc,sc2inc]*6          # V3: 18
[2sc,sc2inc]*6         # V4: 24
[3sc,sc2inc]*6         # V5: 30
[4sc,sc2inc]*6         # V6: 36
[6sc]*8                # V7-14: Giữ 36
[4sc,sc2tog]*6         # V15: 30
[3sc,sc2tog]*6         # V16: 24
[2sc,sc2tog]*6         # V17: 18
[sc,sc2tog]*6          # V18: 12
[sc2tog]*6             # V19: 6
```

### Bước 2: Thân (Axial Generator hoặc viết tay)

```
# Thân thỏ
start_anew    # Bắt đầu object mới
COLOR: White

ring
6sc                    # V1: 6
[sc2inc]*6             # V2: 12
[sc,sc2inc]*6          # V3: 18
[2sc,sc2inc]*6         # V4: 24
[3sc,sc2inc]*6         # V5: 30
[5sc]*12               # V6-17: Giữ 30 (thân dài)
[3sc,sc2tog]*6         # V18: 24
[2sc,sc2tog]*6         # V19: 18
[sc,sc2tog]*6          # V20: 12
[sc2tog]*6             # V21: 6
```

### Bước 3: Tay (x2)

```
# Tay phải
start_anew
COLOR: White

ring
6sc                    # V1: 6
[6sc]*10               # V2-11: Giữ 6 (tay nhỏ)

# Tay trái
start_anew
COLOR: White

ring
6sc
[6sc]*10
```

### Bước 4: Chân (x2)

```
# Chân phải
start_anew
COLOR: White

ring
6sc                    # V1: 6
[sc2inc]*6             # V2: 12
[2sc]*5                # V3-7: Giữ 12 (chân to hơn)
[sc,sc2tog]*4          # V8: 8
[8sc]*3                # V9-11: Giữ 8

# Chân trái
start_anew
COLOR: White

ring
6sc
[sc2inc]*6
[2sc]*5
[sc,sc2tog]*4
[8sc]*3
```

### Bước 5: Tai (x2)

```
# Tai phải
start_anew
COLOR: White

5ch
4sc
[4sc]*8                # Tai dài

# Tai trái
start_anew
COLOR: White

5ch
4sc
[4sc]*8
```

### Bước 6: Ráp lại bằng Object Transform

```
# Đầu: Object 0 (giữ nguyên vị trí)
# Thân: Object 1
TRANSFORM_OBJECT: 1,0,0,-5,0,0,0

# Tay phải: Object 2
TRANSFORM_OBJECT: 2,3,0,-3,0,0,0.5

# Tay trái: Object 3
TRANSFORM_OBJECT: 3,-3,0,-3,0,0,-0.5

# Chân phải: Object 4
TRANSFORM_OBJECT: 4,2,0,-8,0,0,0

# Chân trái: Object 5
TRANSFORM_OBJECT: 5,-2,0,-8,0,0,0

# Tai phải: Object 6
TRANSFORM_OBJECT: 6,2,0,4,0.3,0,0

# Tai trái: Object 7
TRANSFORM_OBJECT: 7,-2,0,4,-0.3,0,0
```

### Pattern hoàn chỉnh (file riêng)

Xem file: `rabbit_amigurumi_complete.txt`

## Dự án 2: Filet Crochet - Chart đơn giản

### Khái niệm Filet Crochet

**Filet = Lưới**
- **Filled square (ô đặc):** 3dc hoặc 4dc
- **Empty square (ô trống):** dc, 2ch, sk, dc

### Ví dụ: Heart chart (5x5)

```
Chart (1 = filled, 0 = empty):
  0 1 0
1 1 1 1
1 1 1 1
  1 1
  0 1
```

### Pattern

```
# Filet Heart
COLOR: Red

# Row 0: Foundation
15ch

# Row 1:   0 1 0
dc,2ch,sk,4dc,2ch,sk,dc,turn

# Row 2: 1 1 1 1
dc,4dc,4dc,4dc,turn

# Row 3: 1 1 1 1
dc,4dc,4dc,4dc,turn

# Row 4:   1 1
3ch,sk,4dc,4dc,turn

# Row 5:   0 1
3ch,sk,dc,2ch,sk,dc
```

### Pattern tổng quát hơn

Dùng labels để dễ chỉnh sửa:

```
# Filet với labels
15ch
$k=0$
dc.Row[k],2ch,sk,4dc.Row[k],2ch,sk,dc.Row[k++],turn
dc.Row[k],4dc.Row[k],4dc.Row[k],4dc.Row[k++],turn
# ...
```

## Dự án 3: Irish Crochet - Motif và nối

### Motif hoa đơn giản

```
# Irish crochet flower
COLOR: White

ring
# Petal 1
5ch,ss@[0,0]
# Petal 2
5ch,ss@[0,0]
# Petal 3
5ch,ss@[0,0]
# Petal 4
5ch,ss@[0,0]
# Petal 5
5ch,ss@[0,0]

# Móc vào petals
$k=0$
[sc@[k,0],4sc,sc@[k++,0]]*5
```

### Motif lá

```
# Irish crochet leaf
start_anew
COLOR: Green

10ch
ss,sc,hdc,dc,tr,tr,dc,hdc,sc,3sc@[@]
# Móc cạnh còn lại
sc,hdc,dc,tr,tr,dc,hdc,sc,ss
```

### Nối motifs

**Phương pháp 1: Dùng labels**

```
# Flower 1
ring
$k=0$
[5ch.Flower1[k++],ss@[0,0]]*5

# Flower 2
start_anew
ring
$m=0$
[5ch.Flower2[m++],ss@[1,0]]*5

# Nối 2 hoa
sc@Flower1[0]
ss@Flower2[0]
```

**Phương pháp 2: Dùng Find Periphery**

(Sau khi móc xong cả 2 hoa)

## Dự án 4: Granny Square - Hoàn chỉnh

### Pattern đầy đủ

```
# Granny Square - Traditional
COLOR: Blue

# Round 1: Center
ring
3ch
$k=0$
[3dc,3ch.Corner[k++]]*4
ss@[1,0]

# Round 2: Corners + sides
$k=0$
[3dc@Corner[k],3ch.Corner[k],3dc@Corner[k++],3ch]*4
ss@Corner[0]

# Round 3
$k=0$
[3dc@Corner[k],3ch.Corner[k],3dc@Corner[k++],3dc,3ch]*4
ss@Corner[0]

# Round 4
$k=0$
[3dc@Corner[k],3ch.Corner[k],3dc@Corner[k++],3dc,3dc,3ch]*4
ss@Corner[0]

# Round 5
$k=0$
[3dc@Corner[k],3ch.Corner[k],3dc@Corner[k++],[3dc]*3,3ch]*4
ss@Corner[0]
```

## Troubleshooting và Debugging

### Vấn đề 1: Pattern bị lộn ngược (inside-out)

**Triệu chứng:** Project nhìn như left-handed hoặc inside-out.

**Nguyên nhân:** Random seed của physics engine.

**Giải pháp:**
```
DOT: start=2     # Thử các giá trị: 0,1,2,3,4...
```

### Vấn đề 2: Mũi không gắn đúng vị trí

**Triệu chứng:** 3D render sai, mũi gắn không đúng.

**Debug:**
1. Expand instructions (run twice)
2. Ctrl+Click mũi trong editor → Xem highlight trong 3D
3. Kiểm tra `@` syntax

**Ví dụ lỗi thường gặp:**
```
# SAI
5ch.A
3sc@B    # ❌ Label B không tồn tại!

# ĐÚNG
5ch.A
3sc@A
```

### Vấn đề 3: Labeled group lỗi "non-adjacent"

**Triệu chứng:** `Cannot use same labels over non-adjacent stitches`

**Nguyên nhân:** Các mũi có cùng label không liền kề.

**Giải pháp:**
```
# SAI
sc.A,5sc,dc.A    # ❌ A không liền kề
3sc@A

# ĐÚNG
sc.A[0],5sc,dc.A[1]    # ✅ Dùng indexed labels
3sc@A[0]
3sc@A[1]
```

### Vấn đề 4: Counter không tăng

**Triệu chứng:** `sc.A[0],sc.A[0],sc.A[0]` thay vì `sc.A[0],sc.A[1],sc.A[2]`

**Nguyên nhân:** Dùng `3sc` thay vì `3*sc`

**Giải pháp:**
```
# SAI
$k=0$
3sc.A[k++]    # ❌ Counter đánh giá trước phân tích

# ĐÚNG
$k=0$
3*sc.A[k++]   # ✅ Counter tăng từng mũi
```

### Vấn đề 5: Project không hội tụ (không render đúng)

**Triệu chứng:** Mũi bị kéo dài, không đều.

**Giải pháp:**
```
DOT: iterations=2000      # Tăng số iterations
DOT: inflate=1.5          # Thêm inflation
DOT: learning_rate=0.05   # Giảm learning rate
```

## Best Practices - Tổng hợp

### 1. Cấu trúc code

✅ **Nên:**
```
# === METADATA ===
# Pattern: Rabbit Amigurumi
# Author: Your Name
# Date: 2026-02-04

# === COLOR ===
COLOR: White
BACKGROUND: LightGray

# === BODY ===
ring
6sc
# ...

# === PHYSICS ===
DOT: iterations=1000
DOT: start=5
```

❌ **Không nên:**
```
ring 6sc 12sc ...    # ❌ Khó đọc
```

### 2. Labels

✅ **Nên:**
- Dùng tên có ý nghĩa: `Corner`, `Edge`, `Petal`
- Dùng counters cho labels lặp: `$k=0$; .A[k++]`
- Comment các labels quan trọng

❌ **Không nên:**
- Tên ngắn vô nghĩa: `A`, `B`, `C`
- Dùng quá nhiều labels không cần thiết

### 3. Counters

✅ **Nên:**
```
$k=0$           # Khởi tạo rõ ràng
[sc.A[k++]]*10  # Dùng * để tăng
```

❌ **Không nên:**
```
$k=0$
10sc.A[k++]     # ❌ Không tăng counter!
```

### 4. Comments

✅ **Nên:**
```
# Round 1: Create center ring
ring
6sc    # 6 sc into magic ring
```

❌ **Không nên:**
```
ring 6sc    # ❌ Không comment, khó hiểu sau
```

### 5. Testing

✅ **Workflow:**
1. Viết pattern nhỏ test trước
2. Render 3D → Kiểm tra
3. Expand → Debug từng mũi
4. Simplify → Chia sẻ

## Bài tập cuối khóa

### Bài tập 1: Amigurumi đơn giản

**Yêu cầu:** Viết pattern cho **bóng tennis** (sphere):
- Circumference: 24
- Màu: Yellow

<details>
<summary>Đáp án</summary>

```
# Tennis Ball
COLOR: Yellow

ring
6sc
[sc2inc]*6             # 12
[sc,sc2inc]*6          # 18
[2sc,sc2inc]*6         # 24
[4sc]*6                # Giữ 24
[2sc,sc2tog]*6         # 18
[sc,sc2tog]*6          # 12
[sc2tog]*6             # 6
```

</details>

### Bài tập 2: Granny Square 3 rounds

**Yêu cầu:** Viết pattern Granny Square với counters

<details>
<summary>Đáp án</summary>

```
# Granny Square - 3 rounds
COLOR: Pink

ring
3ch
$k=0$
[3dc,3ch.Corner[k++]]*4
ss@[1,0]

$k=0$
[3dc@Corner[k],3ch.Corner[k],3dc@Corner[k++],3ch]*4
ss@Corner[0]

$k=0$
[3dc@Corner[k],3ch.Corner[k],3dc@Corner[k++],3dc,3ch]*4
ss@Corner[0]
```

</details>

### Bài tập 3: Dự án cuối khóa

**Yêu cầu:** Thiết kế và viết pattern cho **1 trong các dự án sau:**

1. **Amigurumi:** Con vật đơn giản (bạn chọn)
2. **Túi nhỏ:** Hình trụ có dây đeo
3. **Mũ beanie:** Dùng Axial Generator
4. **Khăn texture:** Kết hợp fl/bl/fp/bp

**Yêu cầu kỹ thuật:**
- Có comments rõ ràng
- Dùng ít nhất 1 DEF (alias)
- Dùng ít nhất 1 counter
- Dùng labels nếu cần
- Render 3D và chụp ảnh

## Tổng kết khóa học

### Những gì bạn đã học

**Bài 1-3: Nền tảng**
- Cú pháp cơ bản, mũi móc
- Hàng, vòng, turn
- Tăng, giảm, biến thể mũi

**Bài 4-5: Attachment và Labels**
- Attachment tuyệt đối/tương đối
- Labels đơn giản
- Label groups

**Bài 6-7: Nâng cao**
- Counters và arithmetic
- Modifiers (^, !, +, ~)
- SORT_LABEL, INDEX_ARRAY

**Bài 8-9: Công cụ**
- Định nghĩa stitches
- Tools (Expand, Simplify, Periphery)
- Generators

**Bài 10: Thực hành**
- Dự án hoàn chỉnh
- Troubleshooting
- Best practices

### Bước tiếp theo

**Cấp độ sau khóa học:**

1. **Thực hành nhiều hơn:**
   - Viết 10+ patterns khác nhau
   - Móc thật để verify

2. **Đọc manual gốc:**
   - Chi tiết hơn về grammar
   - Raw stitch definitions nâng cao

3. **Tham gia cộng đồng:**
   - Forum trên CrochetPARADE.org
   - Chia sẻ patterns

4. **Đóng góp:**
   - Tạo thư viện stitches
   - Dịch patterns sang tiếng Việt
   - Hướng dẫn người khác

### Lời kết

Chúc mừng bạn đã hoàn thành khóa học **CrochetPARADE từ cơ bản đến nâng cao**! 🎉

CrochetPARADE không chỉ là công cụ, mà là **cách suy nghĩ mới** về móc len:
- Chính xác, không mơ hồ
- Có thể kiểm chứng trước khi móc
- Dễ chia sẻ, dễ học

Bây giờ, bạn có thể:
✅ Viết pattern chuyên nghiệp  
✅ Debug pattern phức tạp  
✅ Thiết kế từ ý tưởng đến code  
✅ Dạy người khác sử dụng CrochetPARADE  

**Hãy tiếp tục thực hành và sáng tạo!** 🧶✨

---

## Tài nguyên bổ sung

### Websites
- **CrochetPARADE:** https://crochetparade.org
- **Manual gốc:** Xem trên website

### Files tham khảo
- `manual.md` - Manual đầy đủ (tiếng Anh)
- `Specifying attachment points.md` - Chi tiết về attachment
- `defining_new_stitches.md` - Chi tiết về DEF

### Community
- Forum trên CrochetPARADE.org
- Facebook groups (nếu có)

---

**Tác giả khóa học:** Biên soạn từ manual gốc của Svetlin Tassev  
**Giấy phép:** CC BY-NC-SA 4.0  
**Cập nhật:** Tháng 2, 2026  

**Cảm ơn bạn đã học!** 🙏
