# Bài 8: Định nghĩa Stitches Mới

## Mục tiêu bài học

Sau bài học này, bạn sẽ:
- Tạo alias cho chuỗi mũi: `DEF: p=3ch,ss`
- Copy và modify stitches: `Copy(sc,height,width)`
- Hiểu cấu trúc của một stitch
- Sử dụng raw stitch grammar (nâng cao)
- Mở rộng thư viện stitches của riêng bạn

## 1. Tại sao cần định nghĩa stitches mới?

### Vấn đề

CrochetPARADE có sẵn các mũi cơ bản (sc, dc, ch...), nhưng:
- **Mũi đặc biệt** không có trong thư viện: picot, solomon's knot, bullion...
- **Chuỗi mũi lặp lại** nhiều lần: V-stitch, shell, cluster...
- **Mũi biến thể** cần chiều cao/rộng khác: dc cao hơn, sc hẹp hơn...

### Giải pháp

`DEF:` = **define** (định nghĩa) stitch mới.

## 2. Tạo alias - Đặt tên cho chuỗi mũi

### Cú pháp

```
DEF: tên_mới=chuỗi_mũi
```

**Ví dụ:**
```
DEF: p=3ch,ss@[%,%-4]
```

→ Định nghĩa `p` (picot-3) = 3 chain + slip stitch về 4 mũi trước

### Ví dụ 1: Picot-3

```
DEF: picot3=3ch,ss@[%,%-4]

# Sử dụng
15ch
5sc,picot3,4sc,picot3,4sc
```

**Giải thích:**
- `picot3` thay thế thành `3ch,ss@[%,%-4]`
- Kết quả: 5 sc, 3 chain + ss, 4 sc, 3 chain + ss, 4 sc

### Ví dụ 2: V-stitch

```
DEF: Vstitch=dc,ch,dc@[@]

# Sử dụng
10ch
sk,[Vstitch,sk]*5
```

### Ví dụ 3: Shell-5

```
DEF: shell5=dc,dc@[@],dc@[@],dc@[@],dc@[@]

# Sử dụng
15ch
2sc,[shell5,2sk,2sc]*3
```

### ⚠️ Lưu ý quan trọng

**Alias tăng số mũi trong hàng:**

```
DEF: p=3ch,ss@[%,%-4]
p,p,p    # ≠ 3 mũi, mà là 3*4 = 12 mũi!
```

**Vì sao?** Alias = **string substitution** (thay thế chuỗi):
- `p,p,p` → `3ch,ss@[%,%-4],3ch,ss@[%,%-4],3ch,ss@[%,%-4]`

## 3. Alias với counters

### Quy tắc đánh giá

**Thay thế alias trước → Đánh giá counter sau**

### Ví dụ

```
$k=0$
DEF: scA=sc@A[k]
5ch,ch.A[0],ch.A[1],ch,turn
$k=1$,sk,3ch,scA
```

**Phân tích:**
1. `scA` thay thế thành `sc@A[k]`
2. Đến dòng cuối, đánh giá `k=1`
3. Kết quả: `sc@A[1]`

→ sc móc vào chain thứ 2 (`ch.A[1]`)

### Ví dụ 2: Alias với k++ (phức tạp!)

```
DEF: scB=sc.B[k++]

$k=0$
[scB]*3
```

**Phân tích:**
1. `[scB]*3` thay thế thành `[sc.B[k++]]*3`
2. Phân tích `*`: `sc.B[k++],sc.B[k++],sc.B[k++]`
3. Đánh giá counters: `sc.B[0],sc.B[1],sc.B[2]`

## 4. Copy stitches - Sao chép và chỉnh sửa

### Cú pháp

```
DEF: tên_mới=Copy(tên_cũ)
DEF: tên_mới=Copy(tên_cũ, chiều_cao_mới)
DEF: tên_mới=Copy(tên_cũ, chiều_cao, chiều_rộng)
```

### Ví dụ 1: Đổi tên (reverse single crochet)

```
DEF: rsc=Copy(sc)

# Sử dụng
20ch
19rsc    # Tên "rsc" sẽ hiện trong render
```

**Khác biệt với alias:**
- Alias: `DEF: rsc=sc` → Render hiện "sc"
- Copy: `DEF: rsc=Copy(sc)` → Render hiện "rsc"

### Ví dụ 2: Thay đổi chiều cao

```
DEF: dc_tall=Copy(dc, 3)

# dc mặc định: chiều cao ~1.5-2
# dc_tall: chiều cao 3
```

### Ví dụ 3: Thay đổi cả chiều cao và rộng

```
DEF: sc_narrow=Copy(sc, 1, 0.8)

# sc mặc định: height=1, width=1
# sc_narrow: height=1, width=0.8
```

### Ghi đè stitch có sẵn

```
DEF: dc=Copy(dc, 3)

# Tất cả dc sau này đều có chiều cao 3
```

## 5. Cấu trúc của một stitch

Trước khi học raw grammar, cần hiểu cấu trúc:

### Top nodes (Nút trên)

**= Đỉnh mũi** (hình chữ V ở trên), nơi mũi tiếp theo móc vào.

**Ví dụ:**
- `sc`: 1 top node
- `sc2inc`: 2 top nodes (2 đỉnh V)
- `dc2tog`: 1 top node (2 mũi gộp thành 1)

### Bottom nodes (Nút dưới)

**= Điểm gắn** của mũi này vào mũi trước.

**Ví dụ:**
- `sc`: 1 bottom node (móc vào 1 mũi)
- `dc2tog`: 2 bottom nodes (móc vào 2 mũi)

### Connections (Kết nối)

**= Dây len** nối giữa các nodes.

## 6. Raw stitch grammar - Cú pháp thô (Nâng cao)

### Cú pháp đầy đủ

```
DEF: tên=&comment^top_nodes:bottom_nodes~attachments:other_nodes:connections
```

### Các thành phần

| Phần | Ký hiệu | Mô tả |
|------|---------|-------|
| **Comment** | `&...` | Ghi chú (tùy chọn) |
| **Top nodes** | `^A(type);B(type)` | Các nút trên |
| **Bottom nodes** | `:C;D` | Các nút dưới |
| **Attachments** | `~A-C;B-D` | Gắn top vào bottom |
| **Other nodes** | `:E;F` | Các nút khác (hidden) |
| **Connections** | `:!-1-A;C-1-A` | Độ dài kết nối |

### Ví dụ 1: Single crochet (đơn giản hóa)

```
DEF: mysc=^A(sc):B~A-B::!-1-A;B-1-A
```

**Giải thích:**
- `^A(sc)`: 1 top node A, kiểu sc
- `:B`: 1 bottom node B
- `~A-B`: A gắn vào B
- `::`: Không có other nodes
- `!-1-A`: Nút trước (!) nối với A, độ dài 1
- `B-1-A`: B nối với A, độ dài 1

### Ví dụ 2: Single crochet increase (sc2inc)

```
DEF: mysc2inc=^A(sc);B(sc):C~A-C;B-C::!-1-A;A-1-B;C-1-A;C-1-B
```

**Giải thích:**
- `^A(sc);B(sc)`: 2 top nodes (2 đỉnh)
- `:C`: 1 bottom node (móc vào 1 chân)
- `~A-C;B-C`: Cả A và B đều gắn vào C

### Ví dụ 3: Front loop variant

```
DEF: scfl=^A(scfl):B[front]~A-B::!-1-A;B-1-A
```

**Giải thích:**
- `B[front]`: Bottom node B ở phía trước
- Số sau `[front]`: khoảng cách (mặc định 0.2)
- `B[front0.5]`: Cách 0.5 chain lengths

### Ví dụ 4: Hidden connections

```
DEF: mystitch=^A(sc):B~A-B:C:!-1-A;B-1-A;*C-0.5-A
```

**Giải thích:**
- `:C`: Other node (hidden)
- `*C-0.5-A`: Hidden connection (không render đậm)

## Bài tập thực hành

### Bài tập 1: Tạo alias đơn giản

**Yêu cầu:** Định nghĩa picot-5 (5 chain, ss về)

<details>
<summary>Đáp án</summary>

```
DEF: picot5=5ch,ss@[%,%-6]

# Sử dụng
20ch
4sc,picot5,4sc,picot5,4sc,picot5,4sc
```

</details>

### Bài tập 2: V-stitch với chain space

**Yêu cầu:** Định nghĩa V-stitch = dc, 2 chain, dc vào cùng 1 mũi

<details>
<summary>Đáp án</summary>

```
DEF: Vstitch=dc,2ch,dc@[@]

# Sử dụng
10ch
sk,[Vstitch,sk]*5
```

</details>

### Bài tập 3: Shell với attachment tương đối

**Yêu cầu:** Định nghĩa shell7 = 7 dc vào cùng 1 mũi

<details>
<summary>Đáp án</summary>

```
DEF: shell7=dc,dc@[@],dc@[@],dc@[@],dc@[@],dc@[@],dc@[@]

# Hoặc ngắn gọn hơn (dùng block)
DEF: shell7=dc,[dc@[@]]*6

# Sử dụng
20ch
3sc,[shell7,3sk,3sc]*3
```

</details>

### Bài tập 4: Copy và modify

**Yêu cầu:** Tạo `dc_short` = double crochet với chiều cao 1.5 (thay vì 2)

<details>
<summary>Đáp án</summary>

```
DEF: dc_short=Copy(dc, 1.5)

# Sử dụng
15ch
14dc_short
```

</details>

## Bài tập nâng cao

### Challenge 1: Solomon's knot (alias phức tạp)

**Yêu cầu:** Định nghĩa Solomon's knot:
- 5 chain (kéo dài)
- Single crochet vào vòng sau của chain thứ 2

<details>
<summary>Đáp án</summary>

```
DEF: solomon=5ch,sc@[%,%-4]

# Sử dụng
10ch
[solomon]*10
```

**Lưu ý:** Đây chỉ là approximation, thực tế solomon's knot phức tạp hơn.

</details>

### Challenge 2: Cluster với counters

**Yêu cầu:** Định nghĩa cluster = 3 dc vào 3 mũi khác nhau, gộp đỉnh lại
- Sử dụng labels để đánh dấu 3 mũi

<details>
<summary>Đáp án (đơn giản hóa)</summary>

```
DEF: cluster3=dc,dc@[@+1],dc@[@+1]

# Thực tế: cluster cần gộp đỉnh, không thể làm đơn giản bằng alias
# Nên dùng dc3tog (có sẵn trong CrochetPARADE)
```

</details>

### Challenge 3: Raw grammar - Custom increase

**Yêu cầu:** Định nghĩa `mydc3inc` = 3 dc vào cùng 1 mũi (raw grammar)

<details>
<summary>Đáp án</summary>

```
DEF: mydc3inc=^A(dc);B(dc);C(dc):D~A-D;B-D;C-D::!-2-A;A-2-B;B-2-C;D-2-A;D-2-B;D-2-C

# Giải thích:
# - 3 top nodes: A, B, C (kiểu dc)
# - 1 bottom node: D
# - A, B, C đều gắn vào D
# - Connections: nối các nodes với độ dài ~2 (chiều cao dc)
```

**Lưu ý:** Có sẵn `dc3inc` trong CrochetPARADE, không cần tự định nghĩa!

</details>

## Pattern thực tế

### Pattern 1: Picot edging

```
# Viền picot
DEF: picot3=3ch,ss@[%,%-4]

COLOR: White
30ch
[3sc,picot3]*10
```

### Pattern 2: V-stitch blanket

```
# Chăn V-stitch
DEF: Vstitch=dc,ch,dc@[@]

COLOR: Blue
40ch
[sk,Vstitch]*20
[sk,[Vstitch@[@+1]]*20
]*30
```

### Pattern 3: Shell border

```
# Viền shell
DEF: shell5=dc,[dc@[@]]*4

COLOR: Pink
50ch
[2sc,shell5,2sk]*10
```

### Pattern 4: Custom height dc

```
# Double crochet cao hơn cho chăn dày
DEF: dc=Copy(dc, 2.5)

COLOR: Gray
30ch
[29dc
]*40
```

## Tổng kết bài học

Trong bài 8, bạn đã học:

✅ **Tạo alias:** `DEF: p=3ch,ss`  
✅ **Copy stitch:** `Copy(sc)`, `Copy(dc,3)`, `Copy(sc,1,0.8)`  
✅ **Alias với counters:** Thay thế trước, đánh giá sau  
✅ **Cấu trúc stitch:** Top nodes, bottom nodes, connections  
✅ **Raw grammar (nâng cao):** `^top:bottom~attachments:other:connections`  

### So sánh Alias vs Copy

| | Alias | Copy |
|---|---|---|
| **Cú pháp** | `DEF: p=3ch,ss` | `DEF: rsc=Copy(sc)` |
| **Thay thế** | String substitution | Tạo stitch mới |
| **Tên render** | Tên gốc (3ch,ss) | Tên mới (rsc) |
| **Modify** | Không thể | Có thể (height, width) |

### Best practices

✅ **Nên:**
- Tạo alias cho chuỗi mũi lặp >3 lần
- Copy khi cần thay đổi height/width
- Dùng tên có ý nghĩa: `picot3`, `Vstitch`, `shell5`

❌ **Không nên:**
- Tạo alias quá phức tạp (khó debug)
- Ghi đè stitches có sẵn trừ khi cần thiết
- Dùng raw grammar trừ khi thật sự cần

## Bài tiếp theo

Trong **Bài 9**, chúng ta sẽ học:
- Tools → Expand Instructions
- Tools → Simplify Instructions
- Tools → Find Project Periphery
- Pattern Generators (Sphere, Axial Shape)
- Object Transform

---

**Lưu ý cho giảng viên:**
- Alias và Copy dễ, raw grammar khó → ưu tiên phần đầu
- Raw grammar có thể bỏ qua nếu học viên chỉ cần dùng, không cần tạo stitch phức tạp
- Nhấn mạnh: CrochetPARADE đã có sẵn hầu hết stitches phổ biến
- Thực hành render để thấy sự khác biệt giữa alias và copy
