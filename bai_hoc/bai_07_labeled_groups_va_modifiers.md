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

## 1. Labeled groups

### Khái niệm

Khi nhiều mũi có cùng nhãn, ta gọi đó là một nhóm có nhãn. Có thể gắn vào toàn bộ nhóm hoặc các mũi cụ thể trong nhóm.

```
5ch.A        # Label group A có 5 mũi chain
3sc@A        # Móc 3 sc vào group A
```

→ 3 sc phân bố đều vào 5 chain

### Quy tắc phân bố 

Ta có thể hình dung việc gắn vào khoảng trống của nhóm đó bằng cách thực hiện: 

```
5ch.A,ch,turn
dc,2sc@A
```

Trong trường hợp này, cả hai mũi `sc` sẽ được gắn vào khoảng trống 5 `ch` và được phân bố đều trên khoảng trống đó.

Nếu các vị trí phân bố đều không trùng khớp với các nút mũi hiện có trong nhóm có nhãn, thì các nút ẩn sẽ được tạo ra ở giữa và các mũi sẽ được gắn vào các nút đó. Sự phân bố các nút ẩn là đồng đều dọc theo chiều dài của nhóm có nhãn với giả định rằng tất cả các mũi trong một nhóm có nhãn đều có cùng chiều rộng (chiều cao mũi có thể khác nhau).

CrochetPARADE tự động:

1. Chia không gian group thành các đoạn đều
2. Tạo hidden nodes nếu cần
3. Gắn mũi mới vào các nodes này

**Ví dụ:**

```
2ch,turn
sk,9ch.A,sc,turn
sk,5sc@A,sc
```

→ 5 dc gắn vào chain 1, 3, 5, 7, 9

### Lưu ý

Một nhóm được gắn nhãn phải là một dãy các mũi liền kề. Việc sử dụng cùng một nhãn cho các mũi không liền kề/rời rạc là một lỗi. 

Trong trường hợp sau, hãy sử dụng các nhãn khác nhau hoặc sử dụng nhãn được đánh chỉ mục (nhãn có bộ đếm) để đánh dấu các nhóm riêng biệt, ví dụ: `.A[0]`, `.A[1]` (hoặc `.A[k++]`). 

Tính liền kề được kiểm tra trên biểu đồ mũi. "Liền kề" bao gồm các kết nối trực tiếp từ trên xuống dưới trong cùng một mũi và các kết nối trực tiếp từ dưới lên trên; các kết nối đi qua các nút ẩn không được tính. 

Nếu bạn sử dụng `SORT_LABEL:`, việc kiểm tra tính liền kề này được áp dụng sau khi sắp xếp. Sau khi sắp xếp, các mũi cho nhãn đó vẫn phải liền kề nhau trong biểu đồ mũi. Nếu chúng không liền kề, trình phân tích cú pháp "Cannot use same labels over non-adjacent stitches" sẽ báo lỗi.

Các mũi nối với nhóm được đánh dấu phải nối với các mũi đã được xác định (= đã được móc/thực hiện) tại điểm đó.

Đây là một ví dụ cực kỳ gượng ép, thoạt nhìn có vẻ vi phạm cả quy tắc liền kề và quy tắc tương lai ở trên nhưng thực tế lại không: 

```
9ch,(ch.B).A,ch,dc@A,tr.A@B,2hdc@A
```

Giải thích: Mũi `ch` và mũi `tr` được gắn nhãn cùng là `A` và liền kề nhau (mũi `tr` nối với `B`, là nhãn được mang bởi mũi `ch`; do đó hai mũi này có chung kết nối nút dưới-trên). Nhóm được gắn nhãn `A` có hai mũi: 1 mũi `ch`, 1 mũi `tr`. Có ba mũi được móc vào `A`: 1 mũi `dc`, 2 mũi `hdc`. Sau đó, code sẽ xác định rằng mũi `dc` nối với mũi đầu tiên trong nhóm được gắn nhãn (mũi `ch`), đây không phải là mũi tương lai so với mũi `dc`; mũi `hdc` cuối cùng nối với mũi `tr` (đây không phải là mũi tương lai so với các mũi `hdc`); và mũi `hdc` đầu tiên nối vào một mũi ẩn nằm giữa mũi `ch` và mũi `tr`.

## 2. Modifier `^` - Gắn vào chân mũi (Post)

### Khái niệm

Để gắn vào chân của một mũi, hãy đặt dấu mũ `^` sau định nghĩa của nhãn. Có thể thêm một số nguyên theo sau `^` để chỉ định chân nào của mũi cần gắn vào nếu có nhiều hơn một chân. 

### Cú pháp

```
.A^        # Gắn vào post, không chỉ định post cụ thể
.A^0       # Gắn vào post thứ 0
.A^1       # Gắn vào post thứ 1
```

### Ví dụ 1: Gắn vào post đơn

```
2ch,turn
sc,dc.B^,turn
ch,4sc@B
```

**Giải thích:**

- `dc.B^`: dc được đánh dấu post
- `4sc@B`: Móc 4 sc vào post của dc

### Ví dụ 2: Nhiều posts (khi có mũi giảm)

```
3ch,turn
sc,dc2tog.B^0,turn
4sc@B
```

vs

```
3ch,turn
sc,dc2tog.B^1,turn
4sc@B
```

## 3. Modifier `!` - Bỏ mũi biên

### Khái niệm

Nếu muốn gắn một tập hợp các mũi vào một nhóm mũi, thì mặc định hai mũi biên (đầu tiên và cuối cùng) của nhóm là các điểm gắn hợp lệ của tập hợp đó. Tuy nhiên, người dùng có thể muốn bỏ qua hai mũi đó và thay vào đó gắn vào các khoảng trống và các mũi nằm giữa hai mũi biên đó. Khi đó, bằng cách thêm nhãn `!`, người dùng có thể chỉ định xem có muốn bỏ qua cả hai mũi biên, `!0` bỏ qua mũi đầu tiên hay `!1` bỏ qua mũi cuối cùng hay không.

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
4ch,5sc@A,4ch,sk,sc
```

**Giải thích:**

- `4ch.A!`: 4 chain, bỏ đầu cuối
- `5sc@A`: Móc 5 sc vào khoảng giữa (không vào chain đầu và cuối)

> Lưu ý rằng tham chiếu `@A` không nên chứa `!`

### Ví dụ 2: Bỏ chỉ đầu

```
10ch,turn
sk,9sc,turn
ch,2sc,4ch.A!0,4sk,3sc,turn
4ch,5sc@A,4ch,sk,sc
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
2ch,turn
sc,dc.B^!,turn
4sc@B
```

→ Gắn vào post, bỏ biên

```
2ch,turn
sc,dc.B^!0,turn
4sc@B
```

→ Gắn vào post, bỏ biên dưới

```
2ch,turn
sc,dc.B^!1,turn
4sc@B
```

→ Gắn vào post, bỏ biên trên

Đây là một cấu trúc phức tạp hơn một chút:

```
9ch,turn
8sc,dc.A^,turn
4ch,[sc,sc.B^!,sc]@A
4ch,3sc@B
```

## 4. Modifier `+` - Thêm mũi biên

### Khái niệm

**Mở rộng** labeled group bằng cách thêm mũi trước/sau.

Giả sử bạn muốn thêm các mũi vào một khoảng trống trong chuỗi. Nếu bạn muốn các mũi lấp đầy khoảng trống một cách đều đặn cho đến các mũi biên quanh khoảng trống đó, bạn sẽ phải thêm các mũi trước hoặc sau khoảng trống đó vào nhóm khoảng trống chuỗi đã được gắn nhãn. Điều đó có thể khá rắc rối. Vì vậy, để làm điều đó tự động, hãy thêm dấu `+` sau định nghĩa nhãn khoảng trống chuỗi để thêm cả hai mũi biên, hoặc dấu `+0` hoặc `+1` để thêm mũi biên trước hoặc sau.

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
sk,ch,2sc,3ch.C,3sk,2sc,turn
ch,5sc@C,sc@[-1,0]
```

→ 5 sc chỉ vào 3 chain

**Có `+`:**

```
8ch,turn
sk,ch,2sc,3ch.C+,3sk,2sc,turn
ch,5sc@C,sc@[-1,0]
```

→ 5 sc vào 3 chain + 2 sc biên = 5 mũi

### Kết hợp `+` và `!`

```
8ch,turn
sk,ch,2sc,3ch.C+!,3sk,2sc,turn
ch,5sc@C,sc@[-1,0]
```

→ Thêm biên (`+`), nhưng không móc vào biên (`!`)

> Lưu ý: C+! khác với C, vì khi +! nó thêm biên và không móc vào biên, nhưng có thể móc vào cạnh làm cho sự phân bổ móc nó khác

## 5. Modifier `~` - Đảo chiều gắn

### Khái niệm

Đảo ngược **thứ tự gắn** mũi vào labeled group.

### Cú pháp

```
@A~        # Đảo chiều attachment
```

### Ví dụ: So sánh có/không `~`

**Không đảo chiều:**

Khi gắn một tập hợp các mũi vào một nhóm các mũi khác, code cố gắng sắp xếp các mối nối theo cách ít gây xáo trộn nhất (ví dụ: xoắn) cho dự án, nhưng đôi khi nó thất bại.

```
10ch,turn
sk,8sc,sc.A!,turn
4ch.A!,sk,9tr,turn
1ch,sk,8sc,7sc@A
```

**Có đảo chiều:**

Nếu bạn muốn 7 mũi `sc` nối với nhóm 4 mũi ch được nối theo thứ tự ngược lại, thì hãy thêm dấu `~` vào cuối nhãn nối.

```
10ch,turn
sk,8sc,sc.A!,turn
4ch.A!,sk,9tr,turn
1ch,sk,8sc,7sc@A~
```

→ 7 sc gắn theo thứ tự ngược lại

> Note: vẫn chưa hiểu tại sao k có ~ nó móc vào sc trước ch

Lưu ý rằng cú pháp của CrochetPARADE phân phối nhãn trên các tập hợp mũi. Vì vậy, `(3sc).A~` tương đương với `sc.A~`,`sc.A~`,`sc.A~`. Do đó, trong ví dụ bên dưới, hai tập hợp `(3sc).A~` được coi là một tập hợp `(6sc).A~`. Vì vậy, code sẽ đảo ngược tất cả 6 mũi và sau đó gắn chúng vào nhóm `A`.

```
9ch,turn
sk,(ch,5sc).A,3sc,turn
sk,2sc,3sc@A~,3sc@A~
```

Tương đương với:

```
9ch,turn
sk,(ch,5sc).A,3sc,turn
sk,2sc,6sc@A~
```

### Quy tắc phân nhóm tự động

Nếu muốn gắn mũi `3sc` đầu tiên theo chiều ngược lại, rồi mới đảo chiều mũi `3sc` tiếp theo và gắn chúng lần lượt, thì phải sử dụng các bộ mũi:

```
9ch,turn
sk,(ch,5sc).A[],3sc,turn
sk,2sc,3sc@A[;0]~,3sc@A[;1]~
```

Tuy nhiên, nếu ta kết hợp kiểu gắn kết bình thường (thuận) và kiểu gắn kết ngược (lùi) như trong trường hợp sau:

```
9ch,turn
sk,(ch,5sc).A,3sc,turn
sk,2sc,3sc@A~,3sc@A
```

Khi đó, phần tử `3sc` thứ nhất và phần tử `3sc` thứ hai được coi là các tập hợp riêng biệt. Đoạn code sẽ ghép 3 phần tử đầu tiên theo thứ tự ngược lại, sau đó ghép 3 phần tử tiếp theo theo thứ tự bình thường. Nói cách khác, ví dụ trên tương đương với:

```
9ch,turn
sk,(ch,5sc).A[],3sc,turn
sk,2sc,3sc@A[;0]~,3sc@A[;1]
```

Và tương tự đối với bất kỳ sự kết hợp nào giữa các phần gắn phía trước và phía sau. Do đó, hai ví dụ sau đây là tương đương:

```
9ch,turn
sk,(ch,5sc).A,3sc,turn
sk,2sc,2sc@A~,2sc@A,2sc@A~
```

Cũng giống như

```
9ch,turn
sk,(ch,5sc).A[],3sc,turn
sk,2sc,2sc@A[;0]~,2sc@A[;1],2sc@A[;2]~
```

## 6. Nhiều bộ mũi gắn vào một nhóm được đánh dấu

### Khái niệm

Khi **nhiều nhóm mũi** móc vào cùng labeled group, dùng `;` để chỉ định thứ tự.

### Cú pháp

```
@A[label;set_index]
```

Nếu cần nối nhiều nhóm mũi vào một nhóm mũi có nhãn, thì thứ tự nối các nhóm đó có thể được chỉ định bằng dấu chấm phẩy như sau:

**Ví dụ:**
```
6dc.A[12]
3sc@A[12;1],3sc@A[12;0]
```

Trong ví dụ này, nhóm 3 mũi `sc` thứ hai sẽ được nối với 3 mũi `dc` đầu tiên, và 3 mũi `sc` đầu tiên sẽ được nối với 3 mũi `sc` thứ hai. 

Lưu ý rằng để sử dụng chức năng này, cần phải có nhãn trong dấu ngoặc vuông, chẳng hạn như `A[12]`. Nếu không chỉ định thứ tự, thì các nhóm mũi sẽ được nối theo thứ tự như đã viết.

Ví dụ:

```
6dc.A[12]
3sc@A[12],3sc@A[12] # 6 mũi `sc` được nối liên tiếp trong 6 dc mũi.
```

### Ví dụ với đảo chiều

Lưu ý rằng mỗi bộ có thể được đảo ngược nếu bạn thêm chữ `~` vào cuối nhãn tệp đính kèm.

```
10ch,turn
sk,8sc,sc.A[]!,turn
4ch.A[]!,sk,9tr,turn
1ch,sk,8sc,3sc@A[;1]~,4sc@A[;0]
```

Và:

```
10ch,turn
sk,8sc,sc.A[]!,turn
4ch.A[]!,sk,9tr,turn
1ch,sk,8sc,3sc@A[;1],4sc@A[;0]
```

## 7. Gắn vào mũi cụ thể: `@A[][k]`

### Khái niệm

Nếu muốn gắn vào mũi thứ `k` mang cùng nhãn, thì cũng giống như trên, cần có nhãn trong ngoặc vuông, chẳng hạn như `A[0]` và vị trí mũi sẽ theo sau trong một cặp ngoặc vuông khác: ví dụ `@A[0][k]` gắn vào mũi `k` của nhóm mũi có nhãn `A[0]`. Việc đếm được thực hiện theo cùng hướng với hướng mặc định.

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

Đối với các nhãn đơn giản (nhãn không có bộ đếm như `.A`, `.A[]`, `.A[2,3]`), bạn có thể kiểm soát thứ tự nhóm nhãn bằng cách sử dụng `SORT_LABEL:` thay vì thêm bộ đếm nhãn. Điều này đặc biệt hữu ích khi nhãn được tạo bởi công cụ `Tools → Find project periphery` hoặc bất cứ khi nào bạn gắn nhãn cho các mũi liền kề (một yêu cầu đối với bất kỳ nhóm nhãn nào!) nhưng KHÔNG được sắp xếp theo vị trí liền kề và cần sắp xếp lại.

### Cú pháp

```
SORT_LABEL: A = {thứ_tự_mũi}
```

Điều này có nghĩa là: thu thập các mũi được đánh dấu theo thứ tự chúng xuất hiện trong `thứ_tự_mũi` của bạn (theo thứ tự chúng được móc); tức là `turn` không ảnh hưởng đến thứ tự.

Mảng được hiểu là chỉ số dựa trên 0, mặc dù chỉ số dựa trên 1 (1..N) cũng được chấp nhận và sẽ được chuyển đổi thành chỉ số dựa trên 0.

Tên nhãn có thể là `A`, `B[]`, `C[0]`, `D[1,2]`, v.v.

Nếu nhãn của bạn sử dụng cú pháp thêm cạnh biên (ví dụ: `.A+1`), các cạnh biên sẽ được thêm vào sau sắp xếp khi `SORT_LABEL:` có mặt. Để tránh sự mơ hồ, bạn nên thêm nhãn vào các nút cạnh bằng tay.

> Lưu ý: Khi `SORT_LABEL:` có mặt, và một mũi được gắn nhãn mở rộng thành nhiều nút (ví dụ: tăng như `dc2inc`), bộ sắp xếp sẽ thử cả hai thứ tự nút trên cùng (từ trái sang phải và từ phải sang trái) cho mũi đó trước khi đánh giá tính liền kề, để tính liền kề có thể được bảo toàn sau khi sắp xếp. Không có thao tác sắp xếp lại nội bộ nào được thực hiện khi `SORT_LABEL:` không được sử dụng cho nhóm được gắn nhãn đó.

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

## Bài tập thực hành

### Bài tập 1: Gắn vào post

**Yêu cầu:** Viết pattern:

- Hàng 1: 10 chain
- Hàng 2: 9 dc
- Hàng 3: Đánh dấu dc giữa (B^), móc 5 sc vào post

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

- Hàng 1: 15 chain
- Hàng 2: 5 chain space (A!), móc 7 sc vào space (không vào biên)

<details>
<summary>Đáp án</summary>

```
15ch,turn
5sc,5ch.A!,5sk,5sc,turn
4sc,7sc@A,sk,4sc
```

</details>

### Bài tập 3: Thêm mũi biên

**Yêu cầu:** Viết pattern:

- Hàng 1: 12 chain
- Hàng 2: 3 chain (C+), móc 5 dc vào space (bao gồm biên)

<details>
<summary>Đáp án</summary>

```
11ch,turn
4sc,3ch.C+,3sk,4sc,turn
3sc,5dc@C,sk,3sc
```

</details>

### Bài tập 4: Đảo chiều

**Yêu cầu:** Viết pattern:

- Hàng 1: 10 chain
- Hàng 2: 5 chain (A)
- Hàng 3: Móc 5 sc vào A theo chiều ngược

<details>
<summary>Đáp án</summary>

```
9ch,turn
2sc,5ch.A,5sk,2sc,turn
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
10ch,turn
10dc.A[],turn
5dc@A[;1],5dc@A[;0]
```

</details>

## Bài tập nâng cao

### Challenge 1: Họa tiết móc len Ireland

**Yêu cầu:** Viết họa tiết hoa có thân:

- Ring
- 5 cánh, mỗi cánh 5 chain, ss về ring
- Móc 5 sc vào post của ss (dùng `^`)

<details>
<summary>Đáp án</summary>

```
ring
$k=0$
[5ch.Petal[k++],ss@[0,0]]*5
$m=0$
[5sc@Petal[m++]]*5
```

</details>

### Challenge 2: Lace pattern phức tạp

**Yêu cầu:** Viết pattern lace:

- Hàng 1: 20 chain
- Hàng 2: 3 nhóm chain space (A[0-2]), mỗi nhóm 3 chain
- Hàng 3: Móc vào các space, bỏ biên, đảo chiều space thứ 2

<details>
<summary>Đáp án</summary>

```
16ch,turn
$k=0$
[2sc,3ch.A[k++]!,3sk]*3,sc,turn
[sc,3dc@A[2]],[sc,3dc@A[1]~],[sc,3dc@A[0]],2sc
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
6ch,turn
6sc.A,turn
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
21ch,turn
$k=0$
[3sc,5ch.Shell[k++]+]*6,3sc,turn
$m=5$
sc,[sc,5dc@Shell[m--],sk]*6,2sc
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
