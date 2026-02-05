# Bài 1: Giới thiệu và Cú pháp Cơ bản

## Mục tiêu bài học

Sau bài học này, bạn sẽ:

- Hiểu CrochetPARADE là gì và tại sao nên học
- Biết cách viết các mũi móc cơ bản: chain (ch), single crochet (sc), double crochet (dc)
- Hiểu cách nhân mũi và block
- Viết được pattern đơn giản đầu tiên

## 1. CrochetPARADE là gì?

**CrochetPARADE** (Crochet Pattern Renderer, Analyzer and Debugger) là một **ngôn ngữ lập trình chuyên dụng** để mô tả pattern móc len.

### Tại sao cần CrochetPARADE?

**Pattern móc truyền thống (bằng tiếng Anh thông thường):**

- Dễ nhầm lẫn, không rõ ràng
- Khó kiểm tra trước khi móc
- Không có cách nào xác minh đúng sai

**Pattern móc với CrochetPARADE:**

- Chính xác, không mơ hồ
- Render 2D/3D để xem trước
- Tự động phát hiện lỗi
- Có thể chia sẻ dễ dàng

### So sánh nhanh

**Pattern truyền thống:**

```
Row 1: Chain 10, turn
Row 2: Skip 1, single crochet in each chain across (9 sc), chain 1, turn
Row 3: Skip 1, single crochet in each stitch across (9 sc)
```

**Pattern CrochetPARADE:**

```
10ch,turn
sk,9sc,ch,turn
sk,9sc
```

→ **Ngắn gọn, rõ ràng, chính xác!**

## 2. Mũi móc cơ bản (Basic Stitches)

CrochetPARADE có sẵn các mũi móc thông dụng:

| Ký hiệu | Tên tiếng Anh | Tên tiếng Việt | Mô tả |
|---------|---------------|----------------|-------|
| `ch` | Chain | Mũi xích | Nền móc |
| `ss` | Slip stitch | Mũi trượt | Nối, di chuyển |
| `sc` | Single crochet | Mũi đơn | Chắc, đặc |
| `hdc` | Half double crochet | Mũi nửa kép | Vừa phải |
| `dc` | Double crochet | Mũi kép | Cao, thoáng |
| `tr` | Treble crochet | Mũi ba | Rất cao |
| `dtr` | Double treble | Mũi kép ba | Cực cao |

### Ví dụ đơn giản

```
ch
```

→ Một mũi chain

```
sc
```

→ Một mũi single crochet

```
dc
```

→ Một mũi double crochet

## 3. Nhân mũi (Multiplying Stitches)

Trong móc len, ta thường móc nhiều mũi giống nhau. CrochetPARADE có 3 cách viết:

### Cách 1: Viết liền

```
10ch
```

→ 10 mũi chain

### Cách 2: Dùng dấu `*`

```
10*ch
ch*10
```

→ 10 mũi chain

## 4. Chuỗi mũi (Stitch Sequences)

Để viết nhiều mũi khác nhau trên cùng một hàng, dùng dấu phẩy `,`:

```
ch,sc,dc
```

→ 1 chain, 1 single crochet, 1 double crochet

```
5ch,3sc,2dc
```

→ 5 chain, 3 single crochet, 2 double crochet

## 5. Hàng và dòng (Rows)

**Mỗi dòng code = 1 hàng (row) hoặc 1 vòng (round)**

```
10ch
9sc
```

- Dòng 1: 10 chain (hàng móc nền - hàng 1)
- Dòng 2: 9 single crochet (hàng 2)

## 6. Nhân block (Block Multiplication)

Để lặp lại một chuỗi mũi, dùng dấu ngoặc `[]` hoặc `()`:

```
[sc,dc]*3
```

→ Được phân tích thành: `sc,dc,sc,dc,sc,dc`

```
(2ch,sc)*4
```

→ Được phân tích thành: `2ch,sc,2ch,sc,2ch,sc,2ch,sc`

### So sánh với nhân mũi đơn

```
3sc          → sc,sc,sc
3*sc         → sc,sc,sc
[sc]*3       → sc,sc,sc
```

→ Ba cách này cho kết quả giống nhau!

## 7. Comment (Chú thích)

Để giải thích code, dùng `#` cho comment 1 dòng:

```
10ch,turn  # Hàng 1: Móc nền foundation chain
sk,9sc     # Hàng 2: toàn mũi sc
```

> Lưu ý: `turn` và `sk` sẽ được giải thích ở bài sau

Hoặc dùng `\...\` cho comment nhiều dòng:

```
\
Đây là pattern cho khăn vuông đơn giản
Kích thước: 10cm x 10cm
\
```

## Ví dụ 1: Móc vuông đơn giản

```
# Pattern: Vuông đơn giản 10x10
10ch,turn
sk,ch,9sc,turn
sk,ch,9sc,turn
sk,ch,9sc,turn
sk,ch,9sc,turn
sk,ch,9sc,turn
sk,ch,9sc,turn
sk,ch,9sc,turn
sk,ch,9sc,turn
sk,ch,9sc
```

**Cải thiện bằng block:**

```
# Pattern: Vuông đơn giản 10x10
10ch,turn
[sk,ch,9sc,turn
]*8
sk,ch,9sc
```

→ Ngắn gọn hơn nhiều!

## Ví dụ 2: Móc với nhiều loại mũi

```
# Pattern: Mẫu móc kết hợp
20ch,turn
sk,ch,3sc,4hdc,5dc,4hdc,3sc
```

## Bài tập thực hành

### Bài tập 1: Viết pattern cơ bản

**Yêu cầu:** Viết pattern cho khăn hình chữ nhật:
- Hàng móc nền: 15 chain
- 10 hàng single crochet

<details>
<summary>Đáp án</summary>

```
# Pattern: Khăn hình chữ nhật đơn giản
15ch,turn
[sk,ch,14sc,turn
]*9
sk,ch,14sc
```

</details>

### Bài tập 2: Pattern kết hợp mũi

**Yêu cầu:** Viết pattern cho mẫu móc có cấu trúc:
- Hàng nền: 13 chain
- Hàng 1: 2 sc, 4 hdc, 4 dc, 2 sc

<details>
<summary>Đáp án</summary>

```
# Pattern: Mẫu móc kết hợp nhiều mũi
13ch,turn
sk,ch,2sc,4hdc,4dc,2sc
```

</details>

### Bài tập 3: Block multiplication

**Yêu cầu:** Viết pattern cho mẫu móc lặp:
- Hàng nền: 21 chain
- 5 hàng, mỗi hàng lặp lại: 1 sc, 1 dc

<details>
<summary>Đáp án</summary>

**Cách 1:**
```
21ch,turn
[sk,ch,[sc,dc]*10,turn
]*4
sk,ch,[sc,dc]*10
```

</details>

### Bài tập 4: Đọc hiểu pattern

**Yêu cầu:** Pattern sau tạo ra bao nhiêu mũi trên mỗi hàng?

```
8ch,turn
sk,ch,[2sc,2dc]*3,turn
sk,ch,[sc,hdc,dc]*4
```

<details>
<summary>Đáp án</summary>

- **Hàng 0 (móc nền):** 8 chain
- **Hàng 1:** `sk,ch,[2sc,2dc]*3` = `sk,ch,2sc,2dc,2sc,2dc,2sc,2dc` = **13 mũi** (1 ch + 6 sc + 6 dc và sk không tính vào số mũi)
- **Hàng 2:** `sk,ch,[sc,hdc,dc]*4` = `sk,ch,sc,hdc,dc,sc,hdc,dc,sc,hdc,dc,sc,hdc,dc` = **13 mũi** (1 ch + 4 sc + 4 hdc + 4 dc và sk không tính vào số mũi)

</details>

### Bài tập 5: Viết ngắn gọn hơn

Viết lại pattern sau cho ngắn gọn hơn bằng block multiplication:

```
11ch,turn
sk,ch,5sc,5dc,turn
sk,ch,5sc,5dc,turn
sk,ch,5sc,5dc,turn
5sc,5dc
```

<details>
<summary>Đáp án</summary>

```
11ch,turn
[sk,ch,5sc,5dc,turn
]*3
sk,ch,5sc,5dc
```

</details>

## Tổng kết bài học

Trong bài 1, bạn đã học:

✅ CrochetPARADE là gì và lợi ích của nó  
✅ Các mũi móc cơ bản: `ch`, `sc`, `hdc`, `dc`, `tr`  
✅ Nhân mũi: `10ch` hoặc `10*ch`  
✅ Chuỗi mũi: dùng dấu phẩy `,`  
✅ Hàng móc: mỗi dòng = 1 hàng  
✅ Nhân block: `[sc,dc]*3`  
✅ Comment: `#` hoặc `\...\`  

## Bài tiếp theo

Trong **Bài 2**, chúng ta sẽ học:
- Lệnh `turn` để lật hàng
- Móc vòng tròn với `ring`
- Hiểu về hướng móc và thứ tự attachment

---

**Lưu ý cho giảng viên:**
- Khuyến khích học viên thử nghiệm trên https://crochetparade.org
- Mỗi ví dụ nên được render để học viên thấy kết quả 3D
- Nhấn mạnh sự khác biệt giữa "viết pattern" và "móc thật"
