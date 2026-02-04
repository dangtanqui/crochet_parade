# Bài 2: Làm việc với Hàng và Vòng

## Mục tiêu bài học

Sau bài học này, bạn sẽ:
- Hiểu lệnh `turn` để lật hàng móc
- Biết cách móc vòng tròn với `ring`
- Hiểu khái niệm "hướng móc" (direction of sequential attachment)
- Sử dụng lệnh `...` để wrap dòng dài
- Biết thêm các mũi móc đặc biệt: `sk`, `ss`

## 1. Lệnh `turn` - Lật hàng móc

### Tại sao cần `turn`?

Khi móc hình chữ nhật/vuông, bạn móc qua lại giữa các hàng:
- Hàng 1: móc từ **phải → trái**
- Hàng 2: lật ngược, móc từ **trái → phải**
- Hàng 3: lật lại, móc từ **phải → trái**

Lệnh `turn` báo cho CrochetPARADE biết bạn đã lật hàng.

### Cú pháp

```
10ch,turn
9sc,turn
9sc
```

⚠️ **Quy tắc quan trọng:**
- `turn` phải là lệnh **cuối cùng** trên hàng
- Sau `turn` phải xuống dòng mới

**SAI:**
```
10ch,turn,9sc  # ❌ Không được viết liền sau turn
```

**ĐÚNG:**
```
10ch,turn
9sc
```

### Ví dụ: Khăn hình chữ nhật có turn

```
# Khăn hình chữ nhật 10x5
10ch,turn
sk,ch,9sc,turn
sk,ch,9sc,turn
sk,ch,9sc,turn
sk,ch,9sc
```

**Giải thích:**
- `10ch,turn`: Móc nền 10 chain, rồi lật
- `sk,ch`: Bỏ qua 1 mũi, móc 1 chain để tăng chiều cao
- `9sc`: Móc 9 mũi sc
- `turn`: Lật hàng để móc hàng tiếp

## 2. Skip stitch (`sk`) - Bỏ mũi

`sk` = **skip**, bỏ qua mũi không móc vào.

### Ví dụ đơn giản

```
10ch
sk,8sc
```

**Kết quả:**
- Hàng 0: 10 chain
- Hàng 1: Bỏ mũi chain đầu tiên, móc 8 sc vào 8 chain còn lại

### Tại sao cần `sk`?

1. **Bỏ mũi chain đầu** khi bắt đầu hàng mới
2. **Tạo lỗ hổng** trong pattern (filet crochet, lace)
3. **Giảm số mũi** để tạo hình dáng

### Ví dụ: Tạo khoảng trống

```
15ch
3sc,2sk,5sc,2sk,3sc
```

→ Tạo 2 khoảng trống (mỗi khoảng 2 mũi)

## 3. Slip stitch (`ss`) - Mũi trượt

`ss` là mũi móc ngắn nhất, dùng để:
- **Nối đầu và cuối vòng** khi móc tròn
- **Di chuyển** đến vị trí khác mà không tăng chiều cao

### Ví dụ: Nối vòng

```
ring
6sc
ss@[0,0]  # Nối với mũi đầu tiên
```

## 4. Móc vòng tròn với `ring`

### Magic ring

`ring` = **magic ring**, vòng tròn ma thuật để bắt đầu móc tròn (amigurumi, hoa, mũ...)

```
ring
6sc
```

**Kết quả:** 6 mũi sc móc vào vòng tròn ma thuật

### Ví dụ: Móc hình tròn đơn giản (flat circle)

```
# Vòng tròn phẳng 3 hàng
ring
6sc
12sc
18sc
```

**Giải thích:**
- Vòng 0 (round 0): magic ring
- Vòng 1: 6 sc vào ring
- Vòng 2: 12 sc (tăng đều, mỗi mũi cũ móc 2 mũi mới)
- Vòng 3: 18 sc (tăng đều)

⚠️ **Lưu ý:** Đây chỉ là ví dụ số lượng mũi. Để tạo vòng tròn phẳng đều, cần dùng kỹ thuật increase chính xác (sẽ học ở Bài 3).

## 5. Hướng móc (Direction of Sequential Attachment)

### Khái niệm cốt lõi

CrochetPARADE **tự động suy luận hướng móc** dựa trên số lần `turn`:

| Số lần turn (giữa 2 hàng) | Hướng móc |
|---------------------------|-----------|
| 0 (hoặc chẵn) | **Xuôi** (cùng hướng viết) |
| 1 (hoặc lẻ) | **Ngược** (ngược hướng viết) |

### Ví dụ minh họa

```
10ch,turn          # Hàng 0
9sc,turn           # Hàng 1
9sc                # Hàng 2
```

**Phân tích:**
- **Hàng 1:** Có 1 lệnh `turn` trước nó (ở cuối hàng 0) → móc **ngược**
- **Hàng 2:** Có 2 lệnh `turn` trước nó (cuối hàng 0 và hàng 1) → móc **xuôi**

### Tại sao cần hiểu hướng móc?

Hướng móc ảnh hưởng đến:
1. **Attachment tự động** - mũi móc vào đâu theo mặc định
2. **Đếm mũi** - thứ tự các mũi
3. **Labels** (sẽ học ở Bài 5-7)

💡 **Mẹo:** Khi móc thật, bạn tự nhiên biết hướng móc. CrochetPARADE dùng `turn` để hiểu giống bạn!

## 6. Wrap dòng dài với `...`

Khi hàng móc quá dài, dùng `...` ở đầu dòng mới để nối tiếp:

```
5ch,3sc,2dc,4hdc,3tr
... 2dc,5sc
```

**Tương đương với:**
```
5ch,3sc,2dc,4hdc,3tr,2dc,5sc
```

→ Giúp code dễ đọc hơn!

## Ví dụ tổng hợp 1: Khăn đơn giản với turn

```
# Pattern: Khăn hình chữ nhật 15x10
COLOR: Violet
15ch,turn
[sk,ch,14sc,turn
]*9
sk,ch,14sc
```

**Giải thích từng bước:**

1. `15ch,turn`: Móc nền 15 chain, lật
2. `sk,ch,14sc,turn`: 
   - `sk`: Bỏ mũi chain cuối (đã dùng để lật)
   - `ch`: Chain để tăng chiều cao
   - `14sc`: Móc 14 mũi sc
   - `turn`: Lật hàng
3. Lặp bước 2 tổng cộng 9 lần
4. Hàng cuối không có `turn`

## Ví dụ tổng hợp 2: Móc vòng tròn cơ bản

```
# Pattern: Vòng tròn phẳng
COLOR: Pink
ring
6sc
12sc
18sc
24sc
30sc
36sc
```

**Giải thích:**
- Mỗi vòng tăng 6 mũi để giữ phẳng
- Vòng 1: 6 sc
- Vòng 2: 12 sc (tăng gấp đôi)
- Vòng 3: 18 sc (tăng 6 mũi)
- ...

## Bài tập thực hành

### Bài tập 1: Khăn có turn

**Yêu cầu:** Viết pattern cho khăn vuông 12x12 mũi, có turn ở mỗi hàng.

<details>
<summary>Đáp án</summary>

```
# Pattern: Khăn vuông 12x12
12ch,turn
[sk,ch,11sc,turn
]*10
sk,ch,11sc
```

**Giải thích:**
- Hàng móc nền: 12 chain
- 11 hàng móc (mỗi hàng 11 sc + 1 ch tăng chiều cao)
- Mỗi hàng có `turn` trừ hàng cuối

</details>

### Bài tập 2: Móc vòng tròn

**Yêu cầu:** Viết pattern móc vòng tròn có 5 vòng, mỗi vòng tăng 6 mũi.

<details>
<summary>Đáp án</summary>

```
# Pattern: Vòng tròn 5 vòng
ring
6sc
12sc
18sc
24sc
30sc
```

</details>

### Bài tập 3: Skip và wrap

**Yêu cầu:** Viết pattern:
- Hàng nền: 20 chain
- Hàng 1: Bỏ 2 mũi đầu, móc 10 sc, bỏ 2 mũi, móc 6 sc
- Hàng 2: 15 sc (không skip)

<details>
<summary>Đáp án</summary>

**Cách 1 (không wrap):**
```
20ch
2sk,10sc,2sk,6sc
15sc
```

**Cách 2 (có wrap cho dễ đọc):**
```
20ch
2sk,10sc
... 2sk,6sc
15sc
```

</details>

### Bài tập 4: Đọc hiểu turn

**Yêu cầu:** Phân tích pattern sau, cho biết hàng nào móc xuôi, hàng nào móc ngược:

```
8ch,turn      # Hàng 0
7sc,turn      # Hàng 1
7sc,turn      # Hàng 2
7sc           # Hàng 3
```

<details>
<summary>Đáp án</summary>

| Hàng | Số `turn` trước nó | Hướng móc |
|------|-------------------|-----------|
| Hàng 0 | 0 | Xuôi (mặc định) |
| Hàng 1 | 1 (từ hàng 0) | **Ngược** |
| Hàng 2 | 2 (từ hàng 0 và 1) | **Xuôi** |
| Hàng 3 | 3 (từ hàng 0, 1, 2) | **Ngược** |

**Quy luật:**
- Số `turn` chẵn → móc xuôi
- Số `turn` lẻ → móc ngược

</details>

## Bài tập nâng cao

### Challenge 1: Zigzag pattern

**Yêu cầu:** Tạo pattern móc hình zigzag đơn giản:
- Hàng nền: 15 chain
- Hàng 1: 3 sc, bỏ 2, 3 sc, bỏ 2, 3 sc
- Hàng 2: 3 sc, bỏ 2, 3 sc, bỏ 2, 3 sc
- Hàng 3: Giống hàng 1

<details>
<summary>Đáp án</summary>

```
# Pattern: Zigzag đơn giản
15ch,turn
sk,3sc,2sk,3sc,2sk,3sc,turn
3sc,2sk,3sc,2sk,3sc,turn
3sc,2sk,3sc,2sk,3sc
```

**Lưu ý:** Đây là pattern đơn giản hóa. Thực tế zigzag cần điều chỉnh vị trí tăng/giảm mũi chính xác hơn.

</details>

### Challenge 2: Móc spiral (xoắn ốc)

**Yêu cầu:** Móc vòng tròn xoắn ốc (không nối cuối vòng):
- Ring
- 6 vòng, mỗi vòng 12 mũi sc

<details>
<summary>Đáp án</summary>

```
# Pattern: Spiral đơn giản
ring
[12sc
]*6
```

**Giải thích:**
- Không có `ss` để nối vòng
- Móc liên tục không ngắt → tạo hình xoắn ốc
- Thực tế: cần marker để đánh dấu đầu vòng

</details>

## Các mẫu pattern thực tế

### Pattern 1: Khăn mặt (Washcloth)

```
# Washcloth 25x25
COLOR: Blue
25ch,turn
[sk,ch,24sc,turn
]*24
sk,ch,24sc
```

### Pattern 2: Đĩa lót ly (Coaster) - Vòng tròn

```
# Coaster - Vòng tròn phẳng
COLOR: Green
ring
6sc
12sc
18sc
24sc
30sc
36sc
```

### Pattern 3: Móc dải viền (Border strip)

```
# Border strip 50 mũi
50ch
49sc
49sc
49sc
```

## Tổng kết bài học

Trong bài 2, bạn đã học:

✅ Lệnh `turn` để lật hàng móc  
✅ `sk` (skip) để bỏ mũi  
✅ `ss` (slip stitch) để nối vòng  
✅ `ring` (magic ring) để móc tròn  
✅ Hướng móc: chẵn `turn` = xuôi, lẻ `turn` = ngược  
✅ `...` để wrap dòng dài  

### So sánh: Móc phẳng vs Móc tròn

| | Móc phẳng (Flat) | Móc tròn (Round) |
|---|---|---|
| **Bắt đầu** | Chain dài | `ring` |
| **Lật hàng** | Có `turn` | Không có `turn` |
| **Nối vòng** | Không cần | Có thể dùng `ss` |
| **Ví dụ** | Khăn, chăn | Mũ, túi, amigurumi |

## Bài tiếp theo

Trong **Bài 3**, chúng ta sẽ học:
- Tăng mũi với `inc` (increase)
- Giảm mũi với `tog` (together)
- Mũi móc biến thể: front loop (fl), back loop (bl), front post (fp), back post (bp)

---

**Lưu ý cho giảng viên:**
- Render từng ví dụ để học viên thấy sự khác biệt giữa có/không có `turn`
- Nhấn mạnh: `turn` phải ở cuối hàng
- Thực hành móc tròn và móc phẳng song song để so sánh
