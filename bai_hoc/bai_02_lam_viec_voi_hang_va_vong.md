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
sk,ch,9sc,turn
sk,ch,9sc
```

⚠️ **Quy tắc quan trọng:**
- `turn` phải là lệnh **cuối cùng** trên hàng
- Sau `turn` phải xuống dòng mới

**SAI:**

```
10ch,turn,sk,ch,9sc,turn,sk,ch,9sc  # ❌ Không được viết liền sau turn
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
10ch,turn
sk,9sc
```

**Kết quả:**

- Hàng 0: 10 chain
- Hàng 1: Bỏ mũi chain đầu tiên, móc 9 sc vào 9 chain còn lại

### Tại sao cần `sk`?

1. **Bỏ mũi chain đầu** khi bắt đầu hàng mới
2. **Tạo lỗ hổng** trong pattern (filet crochet, lace)
3. **Giảm số mũi** để tạo hình dáng

### Ví dụ: Tạo khoảng trống

```
16ch,turn
sk,ch,3sc,2sk,5sc,2sk,3sc
```

→ Tạo 2 khoảng trống (mỗi khoảng 2 mũi)

## 3. Slip stitch (`ss`) - Mũi trượt

`ss` là mũi móc ngắn nhất, dùng để:
- **Nối đầu và cuối vòng** khi móc tròn
- **Di chuyển** đến vị trí khác mà không tăng chiều cao

> Lưu ý: Mũi trượt ở ngoài thật và trong mô phỏng khác nhau, cần custom lại mũi này. Nó nên là nối 2 đầu mũi với 0 chiều cao, 0 chiều rộng và không tính là 1 mũi

### Ví dụ: Nối vòng

```
ring
sc6inc,ss@[1,0]  # Nối với mũi đầu tiên
```

## 4. Móc vòng tròn với `ring`

### Magic ring

`ring` = **magic ring**, vòng tròn ma thuật để bắt đầu móc tròn (amigurumi, hoa, mũ...)

```
ring
sc6inc,ss@[1,0]
```

**Kết quả:** 6 mũi sc móc vào vòng tròn ma thuật

> Lưu ý: Vòng tròn ma thuật ở ngoài thật và trong mô phỏng tính số hàng khác nhau, cần custom lại mũi này. Nó nên là sc6ring và gồm 2 hàng trên, nhưng kết quả tính nên là 1 hàng

### Ví dụ: Móc hình tròn đơn giản (flat circle)

```
# Vòng tròn phẳng 4 hàng
ring
sc6inc
6sc2inc
[sc,sc2inc]*6
```

## 5. Hướng móc (Direction of Sequential Attachment)

### Khái niệm cốt lõi

CrochetPARADE **tự động suy luận hướng móc** dựa trên số lần `turn`:

| Số lần turn (giữa 2 hàng) | Hướng móc |
|---------------------------|-----------|
| 0 (hoặc chẵn) | **Xuôi** (cùng hướng viết) |
| 1 (hoặc lẻ) | **Ngược** (ngược hướng viết) |

### Ví dụ minh họa

```
10ch,turn          # Hàng 1
9sc,turn           # Hàng 2
9sc                # Hàng 3
```

**Phân tích:**
- **Hàng 1:** Có 1 lệnh `turn` trước nó (ở cuối hàng 1) → móc **ngược**
- **Hàng 2:** Có 2 lệnh `turn` trước nó (ở cuối hàng 2) → móc **xuôi**

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
   - `sk`: Bỏ mũi chain cuối
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
sc6inc
6sc2inc
[sc,sc2inc]*6
[sc,sc2inc,sc]*6
[3sc,sc2inc]*6
[2sc,sc2inc,2sc]*6
```

**Giải thích:**
- Mỗi vòng tăng 6 mũi để giữ phẳng
- Vòng 1: vòng tròn ma thuật
- Vòng 2: Móc 6 mũi đơn vào vòng tròn ma thuật
- Vòng 3: Móc tăng ở tất cả các mũi
- Vòng 4: Lặp lại 6 lần:
  - móc 1 sc
  - rồi móc tăng 1 lần (inc)
- Vòng 5: Lặp lại 6 lần:
  - móc 1 sc
  - rồi móc tăng 1 lần
  - rồi móc 1 sc
- Vòng 6: Lặp lại 6 lần:
  - móc 3 sc
  - rồi móc tăng 1 lần
- Vòng 7: Lặp lại 6 lần:
  - móc 2 sc
  - rồi móc tăng 1 lần
  - rồi móc 2 sc

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

### Bài tập 2: Đọc hiểu turn

**Yêu cầu:** Phân tích pattern sau, cho biết hàng nào móc xuôi, hàng nào móc ngược:

```
8ch,turn      # Hàng 1
7sc,turn      # Hàng 2
7sc,turn      # Hàng 3
7sc           # Hàng 4
```

<details>
<summary>Đáp án</summary>

| Hàng | Số `turn` trước nó | Hướng móc |
|------|-------------------|-----------|
| Hàng 1 | 0 | Xuôi (mặc định) |
| Hàng 2 | 1 (từ hàng 1) | **Ngược** |
| Hàng 3 | 2 (từ hàng 1 và 2) | **Xuôi** |
| Hàng 4 | 3 (từ hàng 1, 2, 3) | **Ngược** |

**Quy luật:**

- Số `turn` chẵn → móc xuôi
- Số `turn` lẻ → móc ngược

</details>

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
