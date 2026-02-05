# Bài 3: Tăng, Giảm và Biến thể Mũi

## Mục tiêu bài học

Sau bài học này, bạn sẽ:
- Sử dụng `inc` để tăng mũi (increase)
- Sử dụng `tog` để giảm mũi (decrease). “tog” là viết tắt của together
- Hiểu mũi móc front loop/back loop (`fl`/`bl`)
- Hiểu mũi móc front post/back post (`fp`/`bp`)
- Viết được pattern amigurumi và texture đơn giản

## 1. Tăng mũi với `inc` (Increase)

### Khái niệm

**Tăng mũi** = móc **nhiều mũi vào cùng 1 chân** của mũi trước đó.

### Cú pháp

```
sc2inc    # 2 mũi sc vào cùng 1 chân
sc3inc    # 3 mũi sc vào cùng 1 chân
dc4inc    # 4 mũi dc vào cùng 1 chân
```

**Công thức chung:**

```
[tên_mũi][số_mũi]inc
```

### Ví dụ đơn giản

```
ring
sc6inc
6sc2inc
```

**Kết quả:**
- Vòng 1: 6 sc vào ring
- Vòng 2: Mỗi mũi sc cũ móc 2 mũi mới → 12 sc

### Increase phân bố đều

Để tăng **k mũi** trên vòng có **n mũi**, thường dùng công thức:

**"Móc (n/k - 1) mũi bình thường, rồi increase, lặp lại k lần"**

```
[(n/k − 1) sc, sc2inc] * k
```

**Ví dụ:** Tăng 6 mũi trên vòng có 12 mũi:
```
[sc,sc2inc]*6
```
→ Móc 1 sc, rồi 1 increase, lặp 6 lần = 18 mũi

## 2. Giảm mũi với `tog` (Together/Decrease)

### Khái niệm

**Giảm mũi** = móc **nhiều mũi cũ thành 1 mũi mới**.

### Cú pháp

```
sc2tog    # Giảm 2 sc thành 1
sc3tog    # Giảm 3 sc thành 1
dc4tog    # Giảm 4 dc thành 1
```

**Công thức chung:**

```
[tên_mũi][số_mũi]tog
```

### Ví dụ đơn giản

```
ring
sc6inc        # 6 mũi
6sc2inc       # 12 mũi
[sc2tog]*6    # Giảm từ 12 → 6 mũi
sc6tog        # Giảm từ 6 → 1 mũi
```

### Decrease phân bố đều

Để giảm **k mũi** trên vòng có **n mũi**:

**"Móc (n/k - 1) mũi bình thường, rồi decrease, lặp lại"**

**Ví dụ:** Giảm 6 mũi trên vòng có 18 mũi:
```
[sc,sc2tog]*6
```
→ Móc 1 sc, rồi 1 decrease, lặp 6 lần = 12 mũi

## 3. Ví dụ tổng hợp: Hình cầu đơn giản (Sphere)

```
# Pattern: Hình cầu amigurumi
ring
sc6inc                 # Vòng 1: 6 mũi
[sc2inc]*6             # Vòng 2: 12 mũi
[sc,sc2inc]*6          # Vòng 3: 18 mũi
[sc,sc2inc,sc]*6       # Vòng 4: 24 mũi
[3sc,sc2inc]*6         # Vòng 5: 30 mũi
[2sc,sc2inc,2sc]*6     # Vòng 6: 36 mũi
[6sc]*6                # Vòng 7: giữ 36 mũi
[2sc,sc2tog,2sc]*6     # Vòng 8: 30 mũi
[3sc,sc2tog]*6         # Vòng 9: 24 mũi
[sc,sc2tog,sc]*6       # Vòng 10: 18 mũi
[sc,sc2tog]*6          # Vòng 11: 12 mũi
[sc2tog]*6             # Vòng 12: 6 mũi
```

**Giải thích:**
- Vòng 1-6: **Tăng** để tạo bán cầu dưới
- Vòng 7: **Giữ** số mũi (phần thân)
- Vòng 8-12: **Giảm** để đóng bán cầu trên

## 4. Front Loop / Back Loop (`fl` / `bl`)

### Khái niệm

Loop: vòng móc

Mỗi mũi móc có hình chữ V ở trên cùng, gồm 2 vòng:

- **Front loop (vòng trước)** - gần về phía bạn
- **Back loop (vòng sau)** - xa về phía sau

### Cú pháp

```
scfl    # Single crochet front loop only
scbl    # Single crochet back loop only
dcfl    # Double crochet front loop only
dcbl    # Double crochet back loop only
```

**Quy tắc:** Thêm `fl` hoặc `bl` vào cuối tên mũi.

### Tác dụng

- Tạo **texture** (gân nổi/gân lõm)
- Tạo **đường viền** nổi
- Amigurumi: tạo khớp, đường gấp

### Ví dụ: Khăn có gân nổi

```
# Khăn có texture gân nổi
20ch,turn
[sk,ch,19scbl,turn
]*9
sk,ch,19scbl
```

**Kết quả:** Mỗi hàng móc vào back loop → tạo gân nằm ngang rõ nét.

## 5. Front Post / Back Post (`fp` / `bp`)

### Khái niệm

Post: trụ/thân mũi

Móc **quanh thân mũi** (post) thay vì móc vào đỉnh mũi:

- **Front post (fp)** - kim móc đi từ phía trước ra sau
- **Back post (bp)** - kim móc đi từ phía sau ra trước

### Cú pháp

```
fpsc    # Front post single crochet
bpsc    # Back post single crochet
fpdc    # Front post double crochet
bpdc    # Back post double crochet
```

**Quy tắc:** Thêm `fp` hoặc `bp` vào **đầu** tên mũi.

### Tác dụng

- Tạo **texture 3D** nổi bật (ribbing)
- Móc gân cho mũ, áo, tất
- Tạo hiệu ứng "cable" (dây thừng)

### Ví dụ: Ribbing (gân dọc)

```
# Ribbing pattern
21ch,turn
sk,ch,20dc,turn
[sk,ch,[fpdc,bpdc]*10,turn
]*9
sk,ch,[fpdc,bpdc]*10
```

## 6. Tổng hợp: Các loại biến thể mũi

| Loại | Ký hiệu | Tên | Dùng để |
|------|---------|-----|---------|
| **Tăng** | `sc2inc`, `sc3inc` | Increase | Tăng số mũi, tạo hình tròn |
| **Giảm** | `sc2tog`, `sc3tog` | Decrease | Giảm số mũi, đóng hình |
| **Front loop** | `scfl`, `dcfl` | Front loop only | Texture, gân ngang |
| **Back loop** | `scbl`, `dcbl` | Back loop only | Texture, gân ngang |
| **Front post** | `fpsc`, `fpdc` | Front post | Texture 3D, gân dọc |
| **Back post** | `bpsc`, `bpdc` | Back post | Texture 3D, gân dọc |

## Bài tập thực hành

### Bài tập 1: Vòng tròn phẳng hoàn hảo

**Yêu cầu:** Viết pattern vòng tròn phẳng 6 vòng, mỗi vòng tăng 6 mũi đều.

<details>
<summary>Đáp án</summary>

```
# Vòng tròn phẳng 6 vòng
ring
sc6inc                 # V2: 6
[sc2inc]*6             # V3: 12
[sc,sc2inc]*6          # V4: 18
[sc,sc2inc,sc]*6       # V5: 24
[3sc,sc2inc]*6         # V6: 30
[2sc,sc2inc,2sc]*6     # V7: 36
```

</details>

### Bài tập 2: Hình trụ (Cylinder)

**Yêu cầu:** Viết pattern hình trụ (móc tròn không tăng giảm):
- Vòng 1-2-3: Tạo đáy (tăng từ 6 → 12 → 18)
- Vòng 4-9: Giữ 18 mũi (thân)

<details>
<summary>Đáp án</summary>

```
# Hình trụ
ring
sc6inc                 # V1: 6
[sc2inc]*6             # V2: 12
[sc,sc2inc]*6          # V3: 18
18scbl                 # V4: giữ 18
[18sc                  # V5-9: giữ 18
]*5
```

</details>

### Bài tập 3: Khăn texture

**Yêu cầu:** Viết pattern khăn có gân ngang (dùng back loop):
- 25 chain móc nền
- 20 hàng móc back loop only

<details>
<summary>Đáp án</summary>

```
# Khăn texture gân ngang
25ch,turn
[sk,ch,24scbl,turn
]*19
sk,ch,24scbl
```

</details>

### Bài tập 4: Đọc hiểu pattern

**Yêu cầu:** Tính số mũi mỗi vòng.

```
ring
sc6inc
6sc2inc
12sc
6sc2tog
```

<details>
<summary>Đáp án</summary>

**Số mũi:**
- Vòng 1: 1 ring
- Vòng 2: 6 sc
- Vòng 3: 12 sc (tăng)
- Vòng 4: 12 sc (giữ)
- Vòng 5: 12 sc (giảm)

</details>

## Pattern thực tế

### Pattern 2: Túi nhỏ (pouch)

```
# Túi nhỏ hình trụ
COLOR: Pink
ring
sc6inc
[sc2inc]*6             # 12
[sc,sc2inc]*6          # 18
[2sc,sc2inc]*6         # 24
24scbl                 # Back loop → tạo đường viền
[24sc                  # Thân túi
]*10
```

### Pattern 3: Khăn texture

```
# Khăn texture với gân nổi
COLOR: Beige
30ch,turn
sk,ch,29sc,turn
[sk,ch,29scbl,turn
]*25
```

## Tổng kết bài học

Trong bài 3, bạn đã học:

✅ **Tăng mũi:** `sc2inc`, `sc3inc`, `dc2inc`  
✅ **Giảm mũi:** `sc2tog`, `sc3tog`, `dc2tog`  
✅ **Front/Back loop:** `scfl`, `scbl`, `dcfl`, `dcbl`  
✅ **Front/Back post:** `fpsc`, `bpsc`, `fpdc`, `bpdc`  
✅ Công thức tăng/giảm đều trong vòng tròn  
✅ Tạo texture và 3D với fl/bl/fp/bp  

### Bảng tra cứu nhanh: Inc/Tog pattern

| Từ | Đến | Pattern |
|---|---|---|
| 6 | 12 | `[sc2inc]*6` |
| 12 | 18 | `[sc,sc2inc]*6` |
| 18 | 24 | `[2sc,sc2inc]*6` |
| 24 | 30 | `[3sc,sc2inc]*6` |
| 30 | 24 | `[3sc,sc2tog]*6` |
| 24 | 18 | `[2sc,sc2tog]*6` |
| 18 | 12 | `[sc,sc2tog]*6` |
| 12 | 6 | `[sc2tog]*6` |

## Bài tiếp theo

Trong **Bài 4**, chúng ta sẽ học:
- Attachment cơ bản với `@[row,stitch]`
- Attachment tương đối với `@[@+n]`
- Attachment theo loại mũi với `@[sc:row,stitch]`

---

**Lưu ý cho giảng viên:**
- Thực hành móc hình cầu hoàn chỉnh để học viên thấy tăng/giảm
- So sánh fl/bl/fp/bp bằng mẫu móc thực tế
- Nhấn mạnh: inc/tog ảnh hưởng đến **số top nodes** (quan trọng cho attachment!)
