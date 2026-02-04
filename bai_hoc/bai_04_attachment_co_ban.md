# Bài 4: Attachment Cơ bản

## Mục tiêu bài học

Sau bài học này, bạn sẽ:
- Hiểu khái niệm "attachment point" (điểm gắn kết)
- Sử dụng attachment tuyệt đối: `@[row,stitch]`
- Sử dụng attachment tương đối: `@[@+n]`
- Sử dụng attachment theo loại mũi: `@[sc:row,stitch]`
- Hiểu current position với `%`
- Sử dụng multiple attachment heads: `@0`, `@1`, `@2`

## 1. Attachment là gì?

### Khái niệm

Trong móc len, mỗi mũi mới **móc vào** (attach to) mũi cũ ở hàng trước. **Attachment point** = vị trí mà mũi mới gắn vào.

### Mặc định: Attachment tự động

CrochetPARADE tự động gắn mũi theo **thứ tự liên tiếp**:

```
10ch
9sc
```

**Kết quả:**
- Mũi sc thứ 1 gắn vào chain thứ 1
- Mũi sc thứ 2 gắn vào chain thứ 2
- ...
- Mũi sc thứ 9 gắn vào chain thứ 9

→ **Tự động, không cần chỉ định!**

### Khi nào cần chỉ định attachment?

Khi bạn muốn móc **không theo thứ tự**:
- Móc vào mũi ở hàng xa hơn (long stitch)
- Móc nhiều mũi vào cùng 1 chân (cluster)
- Móc vào khoảng chain space
- Tạo hình lace, filet, motif phức tạp

## 2. Đếm hàng và mũi (Indexing)

⚠️ **QUY TẮC QUAN TRỌNG:** CrochetPARADE đếm từ **0**, không phải từ 1!

### Ví dụ minh họa

```
10ch        # Hàng 0 (row 0)
9sc         # Hàng 1 (row 1)
9dc         # Hàng 2 (row 2)
```

**Đánh số mũi trong hàng:**

Hàng 0 (`10ch`):
- Mũi 0: chain đầu tiên
- Mũi 1: chain thứ 2
- ...
- Mũi 9: chain cuối cùng

Hàng 1 (`9sc`):
- Mũi 0: sc đầu tiên
- Mũi 1: sc thứ 2
- ...
- Mũi 8: sc cuối cùng

### Đếm ngược (Negative indexing)

Dùng số âm để đếm từ cuối:
- `-1`: Hàng/mũi cuối cùng
- `-2`: Hàng/mũi áp cuối
- `-3`: Hàng/mũi thứ 3 từ cuối

## 3. Attachment tuyệt đối: `@[row,stitch]`

### Cú pháp

```
mũi@[hàng,mũi]
```

**Ví dụ:**
```
dc@[0,3]
```
→ Móc dc vào mũi thứ 3 (thứ 4 tính từ 1) của hàng 0

### Ví dụ 1: Long stitch

```
10ch
9sc
dc@[0,4]    # Móc dc vào chain thứ 4 của hàng 0
```

**Giải thích:**
- Hàng 2 có 2 mũi: 1 dc tự động (vào hàng 1) + 1 dc vào hàng 0

### Ví dụ 2: Móc ngược về hàng trước

```
15ch
5sc,5dc,4sc
2sc,dc@[0,7],3sc
```

**Giải thích:**
- Hàng 2: Móc 2 sc bình thường, rồi 1 dc móc vào chain thứ 7 của hàng 0

### Ví dụ 3: Đếm ngược

```
10ch
9sc
dc@[-1,0]    # Móc vào mũi đầu tiên của hàng trước (-1)
```

→ `[-1,0]` = hàng trước (row 1), mũi đầu tiên (stitch 0)

## 4. Attachment tương đối: `@[@+n]`

### Khái niệm

`@` lưu **vị trí gắn cuối cùng** (last attachment point). Bạn có thể cộng/trừ để di chuyển.

### Cú pháp

```
@[@]        # Gắn vào cùng vị trí mũi trước
@[@+1]      # Tiến 1 mũi
@[@+2]      # Tiến 2 mũi
@[@-1]      # Lùi 1 mũi
```

### Ví dụ 1: Móc 2 mũi vào cùng 1 chân

```
10ch
sc@[@],sc@[@]    # 2 sc móc vào cùng 1 chain
```

**Giải thích:**
- Mũi sc đầu tiên móc vào chain 0 (tự động)
- `@[@]`: Móc vào cùng vị trí → chain 0
- Kết quả: 2 sc vào chain 0

**So sánh với increase:**
```
sc2inc    # Cũng là 2 sc vào cùng 1 chân
```
→ `sc2inc` ngắn gọn hơn!

### Ví dụ 2: Bỏ mũi (skip) bằng attachment

```
10ch
sc,sc@[@+2],sc
```

**Giải thích:**
- Mũi sc thứ 1: móc vào chain 0
- `@[@+2]`: Tiến 2 mũi → móc vào chain 2 (bỏ chain 1)
- Mũi sc thứ 3: móc tiếp vào chain 3

**Tương đương với:**
```
10ch
sc,sk,sc,sc
```

### Ví dụ 3: Cluster stitch (móc 3 vào 1)

```
10ch
3sc@[@],@[@],@[@]    # 3 sc vào cùng 1 chain
```

## 5. Current position với `%`

### Khái niệm

`%` = **hàng hiện tại** (current row)  
`%-n` = **mũi hiện tại trừ n**

### Ví dụ 1: Gắn vào hàng hiện tại

```
10ch
sc,dc@[%,%-3],sc
```

**Giải thích:**
- `[%,%-3]`: Hàng hiện tại, mũi cách 3 vị trí về trước
- Mũi dc móc vào chính hàng 1, cách 3 mũi về trước

### Ví dụ 2: Picot stitch

```
3ch,ss@[%,%-4]
```

**Giải thích:**
- Móc 3 chain
- Móc slip stitch vào 4 mũi về trước (tạo vòng picot)

**Pattern thực tế:**
```
DEF: picot3=3ch,ss@[%,%-4]
10ch
5sc,picot3,4sc
```

## 6. Attachment theo loại mũi: `@[type:row,stitch]`

### Khái niệm

Đếm **chỉ mũi thuộc loại chỉ định**, bỏ qua các mũi khác.

### Cú pháp

```
@[sc:row,stitch]    # Đếm chỉ sc
@[dc:row,stitch]    # Đếm chỉ dc
@[ch:row,stitch]    # Đếm chỉ chain
```

### Ví dụ 1: Móc vào sc thứ 3 của hàng trước

```
10ch
3sc,4dc,2sc
dc@[sc:-1,2]    # Móc vào sc thứ 3 (index 2) của hàng trước
```

**Giải thích:**
- Hàng 1 có: 3 sc + 4 dc + 2 sc
- `[sc:-1,2]`: Chỉ đếm sc → sc thứ 3 = mũi sc cuối cùng (index 2 trong danh sách sc)

### Ví dụ 2: Kết hợp với attachment tương đối

```
@[sc:@+1]    # Móc vào sc tiếp theo sau vị trí hiện tại
```

**Quy trình:**
1. Từ vị trí `@`, tiến 1 mũi
2. Tìm mũi sc đầu tiên từ vị trí đó trở đi
3. Gắn vào mũi sc đó

## 7. Multiple Attachment Heads: `@0`, `@1`, `@2`

### Khái niệm

Khi móc qua lại giữa nhiều hàng/vị trí, dùng **nhiều đầu gắn** để theo dõi.

- `@` hoặc `@0`: Đầu gắn mặc định
- `@1`, `@2`, ...: Các đầu gắn phụ

### Ví dụ: Móc xen kẽ 2 hàng

```
10ch        # Hàng 0
9sc         # Hàng 1
sc@[-1,0],dc@1[-2,0],sc,dc@1[@1+1]
```

**Giải thích:**
- `@[-1,0]`: Đầu gắn 0 → hàng 1, mũi 0
- `@1[-2,0]`: Đầu gắn 1 → hàng 0, mũi 0
- `sc`: Tiếp tục trên đầu gắn 0 → hàng 1, mũi 1
- `@1[@1+1]`: Tiếp tục trên đầu gắn 1 → hàng 0, mũi 1

→ Móc xen kẽ giữa 2 hàng!

## 8. Empty stitch để reset attachment

### Khái niệm

Dùng `@[...]` **không có mũi** để chỉ di chuyển attachment point.

### Ví dụ

```
10ch
sc,dc,@[@-1],tr
```

**Tương đương với:**
```
10ch
sc,dc,tr@[@]
```

**Giải thích:**
- Sau dc, attachment point ở chain 2
- `@[@-1]`: Lùi về chain 1
- `tr`: Móc vào chain 1

## Bài tập thực hành

### Bài tập 1: Long stitch cơ bản

**Yêu cầu:** Viết pattern:
- Hàng 0: 10 chain
- Hàng 1: 9 sc
- Hàng 2: 3 sc, 1 dc móc vào chain thứ 4 của hàng 0, 5 sc

<details>
<summary>Đáp án</summary>

```
10ch
9sc
3sc,dc@[0,4],5sc
```

</details>

### Bài tập 2: Cluster với attachment tương đối

**Yêu cầu:** Viết pattern móc 3 dc vào cùng 1 chain:
- Hàng 0: 10 chain
- Hàng 1: 2 sc, 3 dc vào chain thứ 3, 5 sc

<details>
<summary>Đáp án</summary>

```
10ch
2sc,dc,dc@[@],dc@[@],5sc
```

**Giải thích:**
- `dc`: Móc dc đầu tiên (vào chain 2)
- `dc@[@]`: Móc dc thứ 2 vào cùng vị trí
- `dc@[@]`: Móc dc thứ 3 vào cùng vị trí
- `5sc`: Tiếp tục móc bình thường

</details>

### Bài tập 3: Picot với current position

**Yêu cầu:** Tạo picot-3 (3 chain nối lại thành vòng):
- Định nghĩa stitch `picot3`
- Sử dụng trong pattern

<details>
<summary>Đáp án</summary>

```
DEF: picot3=3ch,ss@[%,%-4]

# Sử dụng
15ch
3sc,picot3,3sc,picot3,3sc,picot3,3sc
```

**Giải thích:**
- `3ch`: Móc 3 chain
- `ss@[%,%-4]`: Móc slip stitch vào 4 mũi về trước (tạo vòng)

</details>

### Bài tập 4: Attachment theo loại mũi

**Yêu cầu:** Viết pattern:
- Hàng 0: 15 chain
- Hàng 1: 3 sc, 5 dc, 3 sc, 3 hdc
- Hàng 2: 2 sc, 1 dc móc vào dc thứ 3 của hàng 1

<details>
<summary>Đáp án</summary>

```
15ch
3sc,5dc,3sc,3hdc
2sc,dc@[dc:-1,2]
```

**Giải thích:**
- `[dc:-1,2]`: Hàng trước (-1), dc thứ 3 (index 2)
- Chỉ đếm dc, bỏ qua sc và hdc

</details>

## Bài tập nâng cao

### Challenge 1: V-stitch pattern

**Yêu cầu:** Tạo V-stitch (móc dc, chain, dc vào cùng 1 mũi):
- Định nghĩa `Vstitch`
- Pattern: 10 chain, 5 V-stitches

<details>
<summary>Đáp án</summary>

```
DEF: Vstitch=dc,ch,dc@[@]

# Pattern
10ch
sk,[Vstitch,sk]*5
```

**Giải thích:**
- `dc,ch,dc@[@]`: dc, chain, dc vào cùng vị trí
- `sk`: Bỏ 1 mũi giữa các V-stitch

</details>

### Challenge 2: Shell stitch

**Yêu cầu:** Tạo shell (5 dc vào cùng 1 mũi):
- Định nghĩa `shell`
- Pattern: 15 chain, 3 shells

<details>
<summary>Đáp án</summary>

```
DEF: shell=5dc@[@],@[@],@[@],@[@],@[@]

# Pattern (sai, sửa lại)
15ch
2sc,[shell,2sk,2sc]*3
```

**Sửa lại đúng:**
```
DEF: shell=dc,dc@[@],dc@[@],dc@[@],dc@[@]

15ch
2sc,[shell,2sk,2sc]*3
```

**Giải thích:**
- Mũi dc đầu gắn tự động
- 4 mũi dc sau gắn vào cùng vị trí với `@[@]`

</details>

### Challenge 3: Bobble với attachment

**Yêu cầu:** Tạo bobble-4 (4 dc incomplete, nối đỉnh lại):
- Sử dụng attachment để mô phỏng

<details>
<summary>Gợi ý</summary>

**Lưu ý:** CrochetPARADE có sẵn `dc4bobble`. Bài này chỉ để luyện tập attachment logic.

**Mô phỏng đơn giản:**
```
DEF: bobble4=dc,dc@[@],dc@[@],dc@[@]

10ch
5sc,bobble4,4sc
```

**Thực tế:** Nên dùng `dc4bobble` có sẵn để có kết quả chính xác hơn.

</details>

## Pattern thực tế

### Pattern 1: Mesh/Net stitch

```
# Mesh pattern - Mắt lưới
20ch
[dc,ch,sk]*10
[[dc@[@+1],ch,sk]*10
]*5
```

**Giải thích:**
- Hàng 1: dc, chain, skip → tạo khoảng trống
- Hàng 2+: dc móc vào chain space của hàng trước (`@[@+1]`)

### Pattern 2: Long single crochet texture

```
# Texture với long sc
15ch
14sc
[sc,sc,longsc@[0,0],sc,sc,longsc@[0,5],sc,sc,longsc@[0,10]
]*5
```

**Giải thích:**
- Móc sc bình thường xen kẽ long sc móc vào hàng móc nền (hàng 0)

### Pattern 3: Granny square góc

```
# Granny square - 1 góc
ring
3ch,[3dc],3ch,[3dc],3ch,[3dc],3ch,ss@[0,0]
```

## Tổng kết bài học

Trong bài 4, bạn đã học:

✅ **Attachment tuyệt đối:** `@[row,stitch]`  
✅ **Attachment tương đối:** `@[@+n]`  
✅ **Current position:** `@[%,%-3]`  
✅ **Theo loại mũi:** `@[sc:row,stitch]`  
✅ **Đếm ngược:** `@[-1,0]`  
✅ **Multiple heads:** `@0`, `@1`, `@2`  
✅ **Empty stitch:** `@[@-1]` không có mũi  

### So sánh các loại attachment

| Loại | Cú pháp | Dùng khi |
|------|---------|----------|
| **Tuyệt đối** | `@[2,5]` | Biết chính xác vị trí |
| **Tương đối** | `@[@+2]` | Tiến/lùi từ vị trí hiện tại |
| **Theo loại** | `@[sc:-1,3]` | Chỉ quan tâm 1 loại mũi |
| **Current** | `@[%,%-4]` | Gắn vào chính hàng hiện tại |

## Bài tiếp theo

Trong **Bài 5**, chúng ta sẽ học:
- Labels đơn giản: `.A`, `@A`
- Label groups: `5ch.A`, `3sc@A`
- Label distribution
- Attachment vào labels

---

**Lưu ý cho giảng viên:**
- Attachment là **khái niệm khó nhất** ở mức cơ bản, cần nhiều ví dụ
- Nên vẽ sơ đồ hàng/mũi để học viên dễ hình dung
- Nhấn mạnh: Đếm từ 0!
- Thực hành render 3D để thấy attachment có đúng không
