# Bài 7: Labeled Groups và Modifiers

## Mục tiêu bài học

Sau bài học này, bạn sẽ:
- Hiểu sâu về labeled groups (nhóm nhãn)
- Sử dụng `^` để gắn vào thân mũi (post)
- Sử dụng `!` để bỏ mũi biên
- Sử dụng `+` để thêm mũi biên
- Sử dụng `~` để đảo chiều attachment
- Làm việc với multiple stitch sets: `@A[;0]`, `@A[;1]`
- Gắn vào mũi cụ thể: `@A[][2]`
- Sử dụng `SORT_LABEL`

## 1. Labeled groups - Ôn tập nâng cao

### Khái niệm (từ Bài 5)

**Labeled group** = nhiều mũi liền kề có cùng label.

```
5ch.A        # Label group A có 5 mũi chain
3sc@A        # Móc 3 sc vào group A
```

→ 3 sc phân bố đều vào 5 chain

### Quy tắc phân bố

CrochetPARADE tự động:
1. Chia không gian group thành các đoạn đều
2. Tạo hidden nodes nếu cần
3. Gắn mũi mới vào các nodes này

**Ví dụ:**
```
10ch.A
5dc@A
```

→ 5 dc gắn vào chain 1, 3, 5, 7, 9 (hoặc tương tự)

## 2. Modifier `^` - Gắn vào thân mũi (Post)

### Khái niệm

Gắn vào **thân mũi** (post) thay vì đỉnh mũi (top).

### Cú pháp

```
.A^        # Gắn vào post, không chỉ định post cụ thể
.A^0       # Gắn vào post thứ 0
.A^1       # Gắn vào post thứ 1
```

### Ví dụ 1: Gắn vào post đơn

```
8ch,turn
7sc,dc.B^,turn
5ch,4sc@B
```

**Giải thích:**
- `dc.B^`: dc được đánh dấu post
- `4sc@B`: Móc 4 sc vào post của dc

### Ví dụ 2: Nhiều posts (decrease)

```
8ch,turn
6sc,dc2tog.B^0,turn
5ch,4sc@B
```

vs

```
8ch,turn
6sc,dc2tog.B^1,turn
5ch,4sc@B
```

→ Chọn post thứ 0 hay thứ 1 của `dc2tog`

### Khi nào dùng `^`?

✅ **Dùng khi:**
- Móc vào khoảng giữa các mũi
- Tạo hình 3D (amigurumi limbs)
- Irish crochet motifs

## 3. Modifier `!` - Bỏ mũi biên

### Khái niệm

Khi móc vào labeled group, **bỏ qua** mũi đầu và/hoặc mũi cuối.

### Cú pháp

```
.A!        # Bỏ cả đầu và cuối
.A!0       # Bỏ mũi đầu (index 0)
.A!1       # Bỏ mũi cuối (index -1)
```

### Ví dụ 1: Bỏ cả 2 biên

```
10ch,turn
sk,9sc,turn
ch,2sc,4ch.A!,4sk,3sc,turn
4ch,5sc@A,4ch,sc
```

**Giải thích:**
- `4ch.A!`: 4 chain, bỏ đầu cuối
- `5sc@A`: Móc 5 sc vào khoảng giữa (không vào chain đầu và cuối)

### Ví dụ 2: Bỏ chỉ đầu

```
10ch,turn
sk,9sc,turn
ch,2sc,4ch.A!0,4sk,3sc,turn
4ch,5sc@A,4ch,sc
```

→ Bỏ chain đầu, giữ chain cuối

### Ví dụ 3: Bỏ chỉ cuối

```
10ch,turn
sk,9sc,turn
ch,2sc,4ch.A!1,4sk,3sc,turn
4ch,5sc@A,4ch,sc
```

→ Giữ chain đầu, bỏ chain cuối

### Kết hợp `^` và `!`

```
8*ch,turn
7*sc,dc.B^!,turn
5ch,4*sc@B
```

→ Gắn vào post, bỏ biên

## 4. Modifier `+` - Thêm mũi biên

### Khái niệm

**Mở rộng** labeled group bằng cách thêm mũi trước/sau.

### Cú pháp

```
.A+        # Thêm cả đầu và cuối
.A+0       # Thêm mũi trước (previous stitch)
.A+1       # Thêm mũi sau (next stitch)
```

### Ví dụ: So sánh có/không `+`

**Không có `+`:**
```
8ch,turn
2sc,3ch.C,2sc,turn
3ch,5sc@C,sc@[-1,0]
```

→ 5 sc chỉ vào 3 chain

**Có `+`:**
```
8ch,turn
2sc,3ch.C+,2sc,turn
3ch,5sc@C,sc@[-1,0]
```

→ 5 sc vào 3 chain + 2 sc biên = 5 mũi

### Kết hợp `+` và `!`

```
8ch,turn
2sc,3ch.C+!,2sc,turn
3ch,5sc@C,sc@[-1,0]
```

→ Thêm biên (`+`), nhưng không móc vào biên (`!`)

## 5. Modifier `~` - Đảo chiều gắn

### Khái niệm

Đảo ngược **thứ tự gắn** mũi vào labeled group.

### Cú pháp

```
@A~        # Đảo chiều
```

### Ví dụ: So sánh có/không `~`

**Không đảo:**
```
10ch,turn
sk,8sc,sc.A!,turn
4ch.A!,sk,9tr,turn
1ch,sk,8sc,7sc@A
```

**Có đảo:**
```
10ch,turn
sk,8sc,sc.A!,turn
4ch.A!,sk,9tr,turn
1ch,sk,8sc,7sc@A~
```

→ 7 sc gắn theo thứ tự ngược lại

### Quy tắc phân nhóm tự động

CrochetPARADE tự động chia thành **stitch sets** khi có `~` xen kẽ:

```
9ch,turn
sk,(ch,5sc).A,3sc,turn
sk,2sc,3sc@A~,3sc@A
```

**Tương đương với:**
```
9ch,turn
sk,(ch,5sc).A[],3sc,turn
sk,2sc,3sc@A[;0]~,3sc@A[;1]
```

## 6. Multiple stitch sets: `@A[;0]`, `@A[;1]`

### Khái niệm

Khi **nhiều nhóm mũi** móc vào cùng labeled group, dùng `;` để chỉ định thứ tự.

### Cú pháp

```
@A[label;set_index]
```

**Ví dụ:**
```
6dc.A[12]
3sc@A[12;1]      # Set thứ 1 (móc sau)
3sc@A[12;0]      # Set thứ 0 (móc trước)
```

**Kết quả:** Set thứ 1 móc vào 3 dc đầu, set thứ 0 móc vào 3 dc sau

### Ví dụ với đảo chiều

```
10ch,turn
sk,8sc,sc.A[]!,turn
4ch.A[]!,sk,9tr,turn
1ch,sk,8sc,3sc@A[;1]~,4sc@A[;0]
```

## 7. Gắn vào mũi cụ thể: `@A[][k]`

### Khái niệm

Gắn vào mũi thứ **k** trong labeled group.

### Cú pháp

```
@A[][k]        # Mũi thứ k trong group A
@A[0][k]       # Mũi thứ k trong group A[0]
```

### Ví dụ

```
10ch.A[]
sc@A[][0]      # Móc vào chain đầu tiên
sc@A[][5]      # Móc vào chain thứ 6
sc@A[][9]      # Móc vào chain cuối
```

## 8. SORT_LABEL - Sắp xếp thứ tự

### Khái niệm

Định nghĩa **thứ tự xử lý** cho labeled group khi thứ tự móc ≠ thứ tự cần thiết.

### Cú pháp

```
SORT_LABEL: A = {thứ_tự_mũi}
```

**Ví dụ:**
```
SORT_LABEL: A = {3,4,2,1,0}

# 5 mũi được móc theo thứ tự: 0,1,2,3,4
# Nhưng gắn nhãn theo thứ tự: 3,4,2,1,0
```

### Ví dụ thực tế

```
# Móc 5 mũi theo thứ tự bình thường
5sc.A

# Định nghĩa thứ tự mới cho A
SORT_LABEL: A = {2,4,1,3,0}

# Móc vào A sẽ theo thứ tự mới
5dc@A
```

**Giải thích:**
- dc thứ 1 móc vào sc thứ 3 (index 2)
- dc thứ 2 móc vào sc thứ 5 (index 4)
- dc thứ 3 móc vào sc thứ 2 (index 1)
- ...

### Khi nào dùng SORT_LABEL?

✅ **Dùng khi:**
- Tools → Find Project Periphery tự động tạo
- Biên (border/edging) phức tạp
- Thứ tự móc không phải là thứ tự liền kề

## Bài tập thực hành

### Bài tập 1: Gắn vào post

**Yêu cầu:** Viết pattern:
- 10 chain
- Hàng 1: 9 dc
- Hàng 2: Đánh dấu dc giữa (B^), móc 5 sc vào post

<details>
<summary>Đáp án</summary>

```
10ch,turn
3dc,dc.B^,5dc,turn
2sc,5sc@B,2sc
```

</details>

### Bài tập 2: Bỏ mũi biên

**Yêu cầu:** Viết pattern:
- 15 chain
- Hàng 1: 5 chain space (A!), móc 7 sc vào space (không vào biên)

<details>
<summary>Đáp án</summary>

```
15ch,turn
5sc,5ch.A!,5sc,turn
4sc,7sc@A,4sc
```

</details>

### Bài tập 3: Thêm mũi biên

**Yêu cầu:** Viết pattern:
- 12 chain
- Hàng 1: 3 chain (C+), móc 5 dc vào space (bao gồm biên)

<details>
<summary>Đáp án</summary>

```
12ch,turn
4sc,3ch.C+,4sc,turn
3sc,5dc@C,3sc
```

</details>

### Bài tập 4: Đảo chiều

**Yêu cầu:** Viết pattern:
- 10 chain
- Hàng 1: 5 chain (A)
- Hàng 2: Móc 5 sc vào A theo chiều ngược

<details>
<summary>Đáp án</summary>

```
10ch,turn
2sc,5ch.A,2sc,turn
2sc,5sc@A~,2sc
```

</details>

### Bài tập 5: Multiple stitch sets

**Yêu cầu:** Viết pattern:
- 10 dc gắn label A[]
- Set 1 (5 dc) móc vào 5 dc cuối
- Set 0 (5 dc) móc vào 5 dc đầu

<details>
<summary>Đáp án</summary>

```
ring
10dc.A[]
5dc@A[;1],5dc@A[;0]
```

</details>

## Bài tập nâng cao

### Challenge 1: Irish crochet motif

**Yêu cầu:** Viết motif hoa có thân:
- Ring
- 5 cánh, mỗi cánh 5 chain, ss về ring
- Móc 5 sc vào post của ss (dùng `^`)

<details>
<summary>Đáp án</summary>

```
ring
$k=0$
[5ch.Petal[k],ss.Post[k++]^@[0,0]]*5
$m=0$
[5sc@Post[m++]]*5
```

</details>

### Challenge 2: Lace pattern phức tạp

**Yêu cầu:** Viết pattern lace:
- 20 chain
- Hàng 1: 3 nhóm chain space (A[0-2]), mỗi nhóm 3 chain
- Hàng 2: Móc vào các space, bỏ biên, đảo chiều space thứ 2

<details>
<summary>Đáp án</summary>

```
20ch,turn
$k=0$
[2sc,3ch.A[k++]!]*3,2sc,turn
$m=0$
[sc,3dc@A[m++]]*2,[sc,3dc@A[2]~],sc
```

</details>

### Challenge 3: SORT_LABEL

**Yêu cầu:** Viết pattern với SORT_LABEL:
- 6 sc gắn label A
- Định nghĩa thứ tự: {5,3,1,0,2,4}
- Móc 6 dc vào A theo thứ tự mới

<details>
<summary>Đáp án</summary>

```
ring
6sc.A
SORT_LABEL: A = {5,3,1,0,2,4}
6dc@A
```

**Giải thích:**
- dc[0] → sc[5]
- dc[1] → sc[3]
- dc[2] → sc[1]
- ...

</details>

## Pattern thực tế

### Pattern 1: Shell stitch với modifiers

```
# Shell stitch border
COLOR: Pink
30ch,turn
$k=0$
[3sc,5ch.Shell[k++]+]*6,turn
$m=0$
[2sc,5dc@Shell[m++],2sc]*6
```

### Pattern 2: Irish crochet flower

```
# Irish crochet flower với post
COLOR: Yellow
ring
$k=0$
[5ch.Petal[k],ss.Base[k++]^@[0,0]]*6

# Móc vào posts
$m=0$
[sc@Base[m],4sc,sc@Base[m++]]*6
```

### Pattern 3: Complex lace với SORT_LABEL

```
# Lace với thứ tự phức tạp
20ch
$k=0$
[sc.Border[k++]]*20

# Định nghĩa thứ tự biên
SORT_LABEL: Border = {0,5,10,15,19,18,17,16,14,13,12,11,9,8,7,6,4,3,2,1}

# Móc vào biên theo thứ tự mới
$m=0$
[sc@Border,ch,sk]*20
```

## Tổng kết bài học

Trong bài 7, bạn đã học:

✅ **Modifier `^`:** Gắn vào post - `.A^`, `.A^0`  
✅ **Modifier `!`:** Bỏ biên - `.A!`, `.A!0`, `.A!1`  
✅ **Modifier `+`:** Thêm biên - `.A+`, `.A+0`, `.A+1`  
✅ **Modifier `~`:** Đảo chiều - `@A~`  
✅ **Multiple sets:** `@A[;0]`, `@A[;1]`  
✅ **Mũi cụ thể:** `@A[][k]`  
✅ **SORT_LABEL:** Sắp xếp thứ tự tùy chỉnh  

### Bảng tra cứu modifiers

| Modifier | Cú pháp | Ý nghĩa |
|----------|---------|---------|
| **Post** | `.A^`, `.A^0` | Gắn vào thân mũi |
| **Skip edge** | `.A!`, `.A!0`, `.A!1` | Bỏ mũi biên |
| **Add edge** | `.A+`, `.A+0`, `.A+1` | Thêm mũi biên |
| **Reverse** | `@A~` | Đảo chiều gắn |
| **Set index** | `@A[;0]`, `@A[;1]` | Chọn stitch set |
| **Stitch index** | `@A[][2]` | Chọn mũi cụ thể |

### Best practices

✅ **Nên:**
- Dùng `!` khi móc vào chain space (bỏ biên)
- Dùng `+` khi muốn phủ đều cả space
- Dùng `~` khi CrochetPARADE gắn sai chiều
- Dùng SORT_LABEL khi thứ tự móc ≠ thứ tự attachment

❌ **Không nên:**
- Lạm dụng modifiers khi không cần thiết
- Quên kiểm tra thứ tự attachment (render 3D!)

## Bài tiếp theo

Trong **Bài 8**, chúng ta sẽ học:
- Định nghĩa stitches mới
- Alias và Copy
- Raw stitch grammar: `^top:bottom~attachments`

---

**Lưu ý cho giảng viên:**
- Bài này **khó nhất** trong khóa học, cần nhiều ví dụ minh họa
- Render 3D để so sánh có/không có modifier
- Nhấn mạnh: Modifiers giải quyết các trường hợp đặc biệt
- SORT_LABEL khó, có thể để cuối hoặc bỏ qua
