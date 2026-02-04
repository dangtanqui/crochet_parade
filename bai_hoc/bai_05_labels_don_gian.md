# Bài 5: Labels Đơn giản

## Mục tiêu bài học

Sau bài học này, bạn sẽ:
- Hiểu khái niệm label (nhãn) trong CrochetPARADE
- Gắn label cho mũi: `.A`, `.B`
- Móc vào label: `@A`, `@B`
- Hiểu label distribution (phân phối nhãn)
- Làm việc với label groups (nhóm nhãn)
- Sử dụng indexed labels: `.A[0]`, `.A[1]`

## 1. Label là gì?

### Khái niệm

**Label** (nhãn) = **stitch marker ảo** để đánh dấu mũi, dễ tham chiếu sau.

**So sánh với móc thật:**
- Móc thật: Dùng **stitch marker** (vòng nhựa/kim băng) đánh dấu mũi quan trọng
- CrochetPARADE: Dùng **label** (ký tự) đánh dấu trong code

### Tại sao cần labels?

1. **Dễ đọc hơn số:** `@A` vs `@[1,7]`
2. **Linh hoạt:** Thay đổi pattern không cần đếm lại mũi
3. **Chain spaces:** Móc vào khoảng chain dễ dàng
4. **Motifs phức tạp:** Nối các mảnh, ráp hình

## 2. Gắn label đơn: `.A`, `.B`

### Cú pháp

```
stitch.label
```

**Ví dụ:**
```
sc.A        # Single crochet được gắn label A
dc.B        # Double crochet được gắn label B
ch.Start    # Chain được gắn label Start
```

### Ví dụ 1: Đánh dấu mũi đầu/cuối

```
10ch
sc.Start,7sc,sc.End
```

**Giải thích:**
- `sc.Start`: Mũi sc đầu tiên, gắn label "Start"
- `7sc`: 7 mũi sc giữa, không có label
- `sc.End`: Mũi sc cuối, gắn label "End"

## 3. Móc vào label: `@A`

### Cú pháp

```
stitch@label
```

**Ví dụ:**
```
sc@A        # Móc sc vào mũi có label A
dc@Start    # Móc dc vào mũi có label Start
```

### Ví dụ 1: Móc về mũi đã đánh dấu

```
10ch
sc.A,8sc
5sc,dc@A,3sc
```

**Giải thích:**
- Hàng 1: Mũi sc đầu gắn label A
- Hàng 2: Móc 5 sc, rồi 1 dc móc vào mũi A (hàng 1)

**So sánh với attachment tuyệt đối:**
```
# Không dùng label
10ch
sc,8sc
5sc,dc@[1,0],3sc    # Phải nhớ vị trí [1,0]
```

→ Label dễ đọc hơn!

### Ví dụ 2: Nối đầu cuối vòng

```
ring
6sc.Start
ss@Start    # Nối với mũi đầu
```

**Tương đương với:**
```
ring
6sc
ss@[1,0]    # Phải tính index
```

## 4. Label distribution (Phân phối nhãn)

### Khái niệm

Gắn label cho **cả nhóm mũi** bằng cách dùng ngoặc `()` hoặc `[]`.

### Cú pháp

```
(stitch1,stitch2).A        # Cả 2 mũi đều có label A
[3sc,2dc].B                # Cả 5 mũi đều có label B
```

### Ví dụ 1: Gắn label cho nhiều mũi

```
(sc,dc,sc).A
```

**Tương đương với:**
```
sc.A,dc.A,sc.A
```

### Ví dụ 2: Gắn label cho block lặp

```
[2sc,dc].A*3
```

**Phân tích thành:**
```
[2sc,dc].A,[2sc,dc].A,[2sc,dc].A
```

→ Cả 3 block đều có label A!

## 5. Multiple labels (Nhiều nhãn)

Một mũi có thể có **nhiều labels**:

```
sc.A.B.C    # Mũi sc có 3 labels: A, B, C
```

### Ví dụ: Nested labels

```
(3ch.A,sc).B
```

**Kết quả:**
- 3 chain: có label A và B
- 1 sc: chỉ có label B

## 6. Label groups (Nhóm nhãn)

### Khái niệm

Khi **nhiều mũi có cùng label**, gọi là **labeled group**.

Móc vào labeled group → CrochetPARADE **phân bố đều** các mũi mới vào nhóm đó.

### Ví dụ 1: Móc vào chain space

```
5ch.A
3sc@A
```

**Giải thích:**
- `5ch.A`: 5 chain có cùng label A (tạo label group)
- `3sc@A`: Móc 3 sc vào nhóm A → phân bố đều vào 5 chain

**Kết quả:** 3 sc được móc vào chain 1, 3, 5 (hoặc vị trí tương tự)

### Ví dụ 2: Shell stitch với labels

```
10ch,turn
3sc,5ch.A,3sc,turn
3sc,5dc@A,3sc
```

**Giải thích:**
- Hàng 1: 3 sc, 5 chain (label A), 3 sc
- Hàng 2: 3 sc, 5 dc vào nhóm A (5-chain space), 3 sc

### ⚠️ Quy tắc quan trọng của labeled group

1. **Phải liền kề:** Các mũi trong group phải nối tiếp nhau
2. **Không tương lai:** Không móc vào label chưa định nghĩa

**SAI:**
```
sc.A,5sc,dc.A    # ❌ 2 mũi .A không liền kề
3sc@A            # ❌ Lỗi!
```

**ĐÚNG:**
```
sc.A[0],5sc,dc.A[1]    # ✅ Dùng indexed labels (Bài 6)
3sc@A[0]
3sc@A[1]
```

## 7. Indexed labels: `.A[0]`, `.A[1]`

### Khái niệm

Khi cần **nhiều labels giống nhau** (nhưng khác nhóm), dùng **index** để phân biệt.

### Cú pháp

```
.A[0]    # Label A, index 0
.A[1]    # Label A, index 1
.A[2]    # Label A, index 2
```

### Ví dụ 1: Nhiều chain spaces

```
15ch,turn
3sc,3ch.A[0],3sc,3ch.A[1],3sc,turn
2sc,3dc@A[0],2sc,3dc@A[1],2sc
```

**Giải thích:**
- Hàng 1: 2 nhóm chain, gắn label A[0] và A[1]
- Hàng 2: Móc dc vào từng nhóm riêng biệt

### Ví dụ 2: Granny square góc

```
ring
[3dc,3ch.Corner[0]]*4
ss@Corner[0]
```

**Giải thích:**
- 4 góc, mỗi góc có 3 chain gắn label `Corner[0]`, `Corner[1]`, `Corner[2]`, `Corner[3]`
- Nối về góc đầu tiên

**Lưu ý:** Ở đây chỉ ví dụ index, thực tế pattern sẽ khác.

## 8. Label inheritance (Kế thừa nhãn)

### Quy tắc

Labels **gần nhất** được ưu tiên.

### Ví dụ

```
(sc@A)@B
```

**Kết quả:** `sc` móc vào `A`, không phải `B`.

```
(sc,dc@B,sc)@A
```

**Kết quả:**
- `sc` thứ 1: móc vào A
- `dc`: móc vào B (ưu tiên gần hơn)
- `sc` thứ 2: móc vào A

## Bài tập thực hành

### Bài tập 1: Gắn label cơ bản

**Yêu cầu:** Viết pattern:
- 10 chain
- Hàng 1: Gắn label "First" cho mũi sc đầu, label "Last" cho mũi sc cuối
- Hàng 2: Móc dc vào mũi "First"

<details>
<summary>Đáp án</summary>

```
10ch
sc.First,7sc,sc.Last
dc@First,8dc
```

</details>

### Bài tập 2: Chain space

**Yêu cầu:** Viết pattern:
- 15 chain
- Hàng 1: 3 sc, 5 chain (label "Space"), 3 sc
- Hàng 2: 3 sc, 5 dc vào "Space", 3 sc

<details>
<summary>Đáp án</summary>

```
15ch,turn
3sc,5ch.Space,3sc,turn
sk,3sc,5dc@Space,3sc
```

</details>

### Bài tập 3: Indexed labels

**Yêu cầu:** Viết pattern có 2 chain spaces:
- 20 chain
- Hàng 1: 3 sc, 3 chain (Space[0]), 3 sc, 3 chain (Space[1]), 3 sc
- Hàng 2: Móc 3 dc vào mỗi space

<details>
<summary>Đáp án</summary>

```
20ch,turn
3sc,3ch.Space[0],3sc,3ch.Space[1],3sc,turn
sk,2sc,3dc@Space[0],2sc,3dc@Space[1],2sc
```

</details>

### Bài tập 4: Nối vòng

**Yêu cầu:** Viết pattern móc vòng, nối đầu cuối:
- Magic ring
- 12 sc, gắn label "Start" cho mũi đầu
- Slip stitch nối về "Start"

<details>
<summary>Đáp án</summary>

```
ring
sc.Start,11sc
ss@Start
```

</details>

## Bài tập nâng cao

### Challenge 1: V-stitch với labels

**Yêu cầu:** Viết pattern V-stitch sử dụng labels:
- Định nghĩa V-stitch: dc, ch, dc vào cùng 1 mũi
- Pattern: 15 chain, 5 V-stitches

<details>
<summary>Đáp án</summary>

**Cách 1: Không dùng label trong DEF**
```
DEF: Vstitch=dc,ch,dc@[@]

15ch
sk,[Vstitch,sk]*5
```

**Cách 2: Dùng label để rõ ràng hơn**
```
15ch
2sc,5ch.V[0],2sc,5ch.V[1],2sc,turn
dc,ch,dc@V[0],dc,ch,dc@V[1]
```

</details>

### Challenge 2: Granny square góc phần 1

**Yêu cầu:** Viết vòng đầu tiên của granny square:
- Magic ring
- 4 nhóm: mỗi nhóm 3 dc, 3 chain (góc)
- Nối về góc đầu tiên

<details>
<summary>Đáp án</summary>

```
ring
3dc,3ch.Corner[0],3dc,3ch.Corner[1],3dc,3ch.Corner[2],3dc,3ch.Corner[3]
ss@Corner[0]
```

**Lưu ý:** Có thể viết ngắn gọn hơn bằng block (nhưng phức tạp với labels):

```
ring
[3dc,3ch.Corner[0]]*4    # Sai! Index không tự tăng
ss@Corner[0]
```

→ Sẽ học cách tự động tăng index ở Bài 6 (counters)!

</details>

### Challenge 3: Irish crochet motif đơn giản

**Yêu cầu:** Viết motif hoa 4 cánh:
- Ring
- Mỗi cánh: 5 chain (label Petal[0-3]), ss về ring
- Móc 5 sc vào mỗi cánh

<details>
<summary>Đáp án</summary>

```
ring
5ch.Petal[0],ss@[0,0]
5ch.Petal[1],ss@[0,0]
5ch.Petal[2],ss@[0,0]
5ch.Petal[3],ss@[0,0]
5sc@Petal[0]
5sc@Petal[1]
5sc@Petal[2]
5sc@Petal[3]
```

**Lưu ý:** Pattern thực tế sẽ phức tạp hơn, đây chỉ là minh họa labels.

</details>

## Pattern thực tế

### Pattern 1: Mesh với labels

```
# Mesh pattern - dễ đọc với labels
20ch
[dc,2ch.Space]*10
[[dc@Space,2ch.Space]*10
]*5
```

### Pattern 2: Shell border

```
# Viền shell
30ch
[3sc,5ch.Shell]*6
[2sc,5dc@Shell,2sc]*6
```

### Pattern 3: Picot edging

```
# Viền picot với labels
DEF: picot=3ch,ss@[%,%-4]

20ch
19sc
[3sc,picot]*6,sc
```

## Tổng kết bài học

Trong bài 5, bạn đã học:

✅ **Gắn label:** `.A`, `.B`, `.Start`  
✅ **Móc vào label:** `@A`, `@Start`  
✅ **Label distribution:** `(sc,dc).A`  
✅ **Label groups:** `5ch.A`, `3sc@A`  
✅ **Indexed labels:** `.A[0]`, `.A[1]`  
✅ **Multiple labels:** `.A.B.C`  

### So sánh: Attachment vs Labels

| | Attachment | Labels |
|---|---|---|
| **Syntax** | `@[row,stitch]` | `@A` |
| **Ưu điểm** | Chính xác tuyệt đối | Dễ đọc, linh hoạt |
| **Nhược điểm** | Khó đọc, phải đếm mũi | Phải định nghĩa trước |
| **Dùng khi** | Biết chính xác vị trí | Pattern phức tạp, nhiều tham chiếu |

### Best practices

✅ **Nên:**
- Dùng labels có ý nghĩa: `Corner`, `Space`, `Start`
- Dùng indexed labels khi có nhiều nhóm giống nhau
- Kiểm tra labeled group có liền kề không

❌ **Không nên:**
- Dùng label quá ngắn: `A`, `B` (trừ khi ví dụ đơn giản)
- Dùng cùng label cho nhóm không liền kề (phải dùng index)

## Bài tiếp theo

Trong **Bài 6**, chúng ta sẽ học:
- Counters: `$k=0$`, `k++`, `++k`
- Indexed labels tự động
- `INDEX_ARRAY`: định nghĩa thứ tự tùy chỉnh
- Counter arithmetic

---

**Lưu ý cho giảng viên:**
- Labels là **khái niệm quan trọng nhất** của CrochetPARADE
- Nên so sánh với stitch marker thực tế để học viên dễ hình dung
- Render 3D để thấy labels attachment có đúng không
- Nhấn mạnh quy tắc: labeled group phải liền kề!
