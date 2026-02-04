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
sc2inc,sc2inc,sc2inc,sc2inc,sc2inc,sc2inc
```

**Kết quả:**
- Vòng 1: 6 sc vào ring
- Vòng 2: Mỗi mũi sc cũ móc 2 mũi mới → 12 sc

**Viết ngắn gọn hơn:**
```
ring
sc6inc
[sc2inc]*6    # hoặc 6sc2inc
```

### Increase phân bố đều

Để tăng **k mũi** trên vòng có **n mũi**, thường dùng công thức:

**"Móc (n/k - 1) mũi bình thường, rồi increase, lặp lại k lần"**

```
[(n/k − 1) sc, inc] * k
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
sc6inc
6sc2inc
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
[2sc,sc2inc]*6         # Vòng 4: 24 mũi
[3sc,sc2inc]*6         # Vòng 5: 30 mũi
[4sc,sc2inc]*6         # Vòng 6: 36 mũi
[5sc]*6                # Vòng 7-12: giữ 36 mũi
[5sc]*6
[5sc]*6
[5sc]*6
[5sc]*6
[5sc]*6
[4sc,sc2tog]*6         # Vòng 13: 30 mũi
[3sc,sc2tog]*6         # Vòng 14: 24 mũi
[2sc,sc2tog]*6         # Vòng 15: 18 mũi
[sc,sc2tog]*6          # Vòng 16: 12 mũi
[sc2tog]*6             # Vòng 17: 6 mũi
```

**Giải thích:**
- Vòng 1-6: **Tăng** để tạo bán cầu dưới
- Vòng 7-12: **Giữ** số mũi (phần thân)
- Vòng 13-17: **Giảm** để đóng bán cầu trên

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
]*10
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
20ch,turn
sk,ch,19dc,turn
[sk,ch,fpdc,bpdc,fpdc,bpdc,fpdc,bpdc,fpdc,bpdc,fpdc,bpdc,turn
]*10
```

**Giải thích:**
- Hàng đầu: dc bình thường
- Các hàng sau: xen kẽ fpdc và bpdc → tạo gân dọc

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
6sc                    # V1: 6
[sc2inc]*6             # V2: 12
[sc,sc2inc]*6          # V3: 18
[2sc,sc2inc]*6         # V4: 24
[3sc,sc2inc]*6         # V5: 30
[4sc,sc2inc]*6         # V6: 36
```

**Quy luật:**
- Vòng n: `[(n-1)sc, sc2inc]*6`
- Số mũi vòng n: `n * 6`

</details>

### Bài tập 2: Hình trụ (Cylinder)

**Yêu cầu:** Viết pattern hình trụ (móc tròn không tăng giảm):
- Vòng 1-2: Tạo đáy (tăng từ 6 → 12 → 18)
- Vòng 3-8: Giữ 18 mũi (thân)

<details>
<summary>Đáp án</summary>

```
# Hình trụ
ring
6sc                    # V1: 6
[sc2inc]*6             # V2: 12
[sc,sc2inc]*6          # V3: 18
[18sc                  # V4-8: giữ 18
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

**Yêu cầu:** Pattern sau tạo hình gì? Tính số mũi mỗi vòng.

```
ring
6sc
[sc2inc]*6
[2sc]*12
[sc,sc2tog]*6
```

<details>
<summary>Đáp án</summary>

**Hình dạng:** Hình bán cầu (bowl/cup)

**Số mũi:**
- Vòng 1: 6 sc
- Vòng 2: 12 sc (tăng)
- Vòng 3: 24 sc (giữ, viết ngắn gọn)
- Vòng 4: 12 sc (giảm)

**Lưu ý:** Vòng 3 có `[2sc]*12` = `2sc` lặp 12 lần = 24 mũi.

</details>

## Bài tập nâng cao

### Challenge 1: Hình nón (Cone)

**Yêu cầu:** Tạo pattern hình nón bằng cách tăng dần đều:
- Vòng 1-2: Đáy tròn (6 → 12)
- Vòng 3-7: Tăng 6 mũi mỗi vòng

<details>
<summary>Đáp án</summary>

```
# Hình nón
ring
6sc                    # V1: 6
[sc2inc]*6             # V2: 12
[sc,sc2inc]*6          # V3: 18
[2sc,sc2inc]*6         # V4: 24
[3sc,sc2inc]*6         # V5: 30
[4sc,sc2inc]*6         # V6: 36
[5sc,sc2inc]*6         # V7: 42
```

</details>

### Challenge 2: Amigurumi đầu đơn giản

**Yêu cầu:** Viết pattern đầu amigurumi cơ bản:
- Tăng 6 vòng (6 → 36)
- Giữ 4 vòng (36 mũi)
- Giảm 6 vòng (36 → 6)

<details>
<summary>Đáp án</summary>

```
# Đầu amigurumi
ring
6sc                    # V1: 6
[sc2inc]*6             # V2: 12
[sc,sc2inc]*6          # V3: 18
[2sc,sc2inc]*6         # V4: 24
[3sc,sc2inc]*6         # V5: 30
[4sc,sc2inc]*6         # V6: 36
[6sc                   # V7-10: giữ 36
]*4
[4sc,sc2tog]*6         # V11: 30
[3sc,sc2tog]*6         # V12: 24
[2sc,sc2tog]*6         # V13: 18
[sc,sc2tog]*6          # V14: 12
[sc2tog]*6             # V15: 6
```

</details>

### Challenge 3: Ribbing pattern (gân dọc)

**Yêu cầu:** Viết pattern có gân dọc (xen kẽ fp và bp):
- Móc nền: 20 chain
- Hàng 1: dc bình thường
- Hàng 2-10: xen kẽ fpdc và bpdc

<details>
<summary>Đáp án</summary>

```
# Ribbing (gân dọc)
20ch,turn
sk,ch,19dc,turn
[sk,ch,[fpdc,bpdc]*9,fpdc,turn
]*9
```

**Giải thích:**
- Hàng 1: 19 dc (nền để móc post)
- Hàng 2-10: Lặp `[fpdc,bpdc]` → tạo gân dọc

</details>

## Pattern thực tế

### Pattern 1: Mũ beanie đơn giản (phần đầu)

```
# Mũ beanie - Phần đỉnh
COLOR: Gray
ring
6sc
[sc2inc]*6             # 12
[sc,sc2inc]*6          # 18
[2sc,sc2inc]*6         # 24
[3sc,sc2inc]*6         # 30
[4sc,sc2inc]*6         # 36
[5sc,sc2inc]*6         # 42
[6sc,sc2inc]*6         # 48
[8sc                   # Giữ 48 mũi cho phần thân
]*15
```

### Pattern 2: Túi nhỏ (pouch)

```
# Túi nhỏ hình trụ
COLOR: Pink
ring
6sc
[sc2inc]*6             # 12
[sc,sc2inc]*6          # 18
[2sc,sc2inc]*6         # 24
[24scbl                # Back loop → tạo đường viền
]
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
