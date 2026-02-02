# Hướng dẫn CrochetPARADE (Crochet Pattern Renderer, Analyzer & Debugger)

---

## 0. CrochetPARADE là gì?

**CrochetPARADE** là một **nền tảng mô phỏng crochet bằng ngôn ngữ hình thức** (formal grammar). Bạn **viết pattern như code**, hệ thống sẽ:

* Phân tích cú pháp (parse)
* Kiểm tra logic mũi móc
* Dựng mô hình **2D / 3D**
* Cho phép debug hình dáng *trước khi móc thật*

👉 Mục tiêu không phải thay thế người móc, mà là:

* Giảm lỗi pattern
* Hiểu chính xác hình học của crochet
* Viết pattern phức tạp (lace, amigurumi, ráp mảnh) một cách **có kiểm soát**

---

## 1. Tư duy cốt lõi khi dùng CrochetPARADE

Nếu bạn quen móc truyền thống:

* Bạn *móc → nhìn → sửa*

Với CrochetPARADE:

* Bạn *mô tả logic → render → debug → móc*

Ba khái niệm nền tảng:

1. **Stitch graph** – các mũi là node, dây len là edge
2. **Attachment order** – thứ tự mũi móc quyết định hình dạng
3. **Deterministic pattern** – cùng input → luôn ra cùng hình

---

## 2. Cấu trúc pattern cơ bản

### 2.1 Dòng = hàng / vòng

* Mỗi dòng là **1 row hoặc 1 round**
* Hệ thống **đếm từ 0**, không phải từ 1

```
10ch
9sc
```

* Hàng 0: 10 chain
* Hàng 1: 9 single crochet

---

### 2.2 Mũi cơ bản (Built-in stitches)

| Ký hiệu | Tên            | Ghi chú hình học     |
| ------- | -------------- | -------------------- |
| ch      | Chain          | tạo node nền         |
| ss      | Slip stitch    | không tăng chiều cao |
| sc      | Single crochet | chắc, đặc            |
| hdc     | Half double    | cao vừa              |
| dc      | Double crochet | cao, thoáng          |
| tr      | Treble         | rất cao              |
| dtr     | Double treble  | lace                 |
| trtr    | Triple treble  | cực cao              |

---

### 2.3 Mũi đặc biệt

| Ký hiệu    | Ý nghĩa                   |
| ---------- | ------------------------- |
| ring       | vòng tròn ma thuật        |
| sk         | bỏ mũi                    |
| turn       | lật hàng                  |
| tie_up     | khóa sợi                  |
| start_at   | bắt đầu tại vị trí bất kỳ |
| start_anew | bắt đầu mảnh rời          |

---

## 3. Móc tăng – giảm (Inc / Tog)

CrochetPARADE xử lý **tăng giảm hình học tự động**.

### 3.1 Tăng mũi

```
sc2inc   # 2 sc vào cùng 1 chân
sc3inc
```

### 3.2 Giảm mũi

```
sc2tog   # giảm 2 sc
sc3tog
```

⚠️ Những mũi này tạo **nhiều top node**, ảnh hưởng đến đánh số mũi.

---

## 4. Nhân mũi & block (Tư duy lập trình)

### 4.1 Nhân mũi đơn

```
10sc
10*sc
```

### 4.2 Nhân block

```
[sc,dc]*3
```

→ sc,dc, sc,dc, sc,dc

### 4.3 Cắt vòng lặp với < >

```
[2sc,<,dc]*3
```

→ dc,2sc, dc,2sc, dc

---

## 5. Turn & hướng móc (RẤT QUAN TRỌNG)

CrochetPARADE **tự suy luận hướng móc** dựa vào số lần `turn`.

* Số turn chẵn → móc xuôi
* Số turn lẻ → móc ngược

Ví dụ:

```
10ch,turn
9sc,turn
```

Hướng móc ảnh hưởng trực tiếp đến:

* Attach mũi
* Đếm mũi
* Lace & filet

---

## 6. Attachment – gắn mũi nâng cao

### 6.1 Gắn theo vị trí tuyệt đối

```
dc@[2,4]
```

→ hàng 3, mũi số 5

Âm nghĩa là đếm ngược:

```
dc@[-1,0]
```

→ Mũi thứ nhất của hàng trước

---

### 6.2 Gắn theo loại mũi

```
dc@[sc:-1,3]
```

→ mũi sc thứ 4 của hàng trước

---

### 6.3 Gắn tương đối (@)

```
dc@[@]
```

→ gắn vào cùng vị trí mũi trước

```
dc@[@+2]
```

→ tiến 2 mũi theo hướng móc

---

## 7. Label – trái tim của CrochetPARADE

### 7.1 Label đơn

```
sc.A
```

Gắn vào label:

```
sc@A
```

---

### 7.2 Label nhóm (group)

```
5ch.A
3sc@A
```

→ 3 sc phân bố đều vào khoảng chain

⚠️ Label **phải liên tiếp**, nếu không sẽ lỗi.

---

### 7.3 Label có index

```
sc.A[0]
sc.A[1]
```

Hoặc dùng biến:

```
$k=0$
sc.A[k++]
```

---

## 8. INDEX_ARRAY & SORT_LABEL (nâng cao thật sự)

### 8.1 INDEX_ARRAY

Dùng khi **thứ tự biên ≠ thứ tự móc**.

```
INDEX_ARRAY: k={4,3,1,2,0}
```

Rất quan trọng cho:

* Viền
* Ráp mảnh
* Panel

---

### 8.2 SORT_LABEL

```
SORT_LABEL: A={3,4,2,1,0}
```

→ kiểm soát thứ tự xử lý label **không cần counter**.

---

## 9. Gắn vào thân mũi (^), bỏ biên (!), mở rộng (+)

### 9.1 Gắn vào thân mũi

```
dc.B^
sc@B
```

### 9.2 Bỏ mũi biên

```
4ch.A!
```

### 9.3 Thêm mũi biên

```
3ch.A+
```

---

## 10. Đảo chiều gắn (~) & nhiều tập gắn

```
5sc@A~
```

→ gắn ngược thứ tự

```
3sc@A[;1]
3sc@A[;0]
```

→ kiểm soát thứ tự nhiều nhóm

---

## 11. Tools – công cụ không thể thiếu

### 11.1 Expand Instructions

* Bung toàn bộ mũi
* Dùng để debug

### 11.2 Simplify Instructions (Experimental)

* Nén pattern sau chỉnh sửa

### 11.3 Find Project Periphery ⭐⭐⭐

* Tìm đường biên
* Gắn label viền
* Sinh INDEX_ARRAY / SORT_LABEL

---

## 12. Pattern Generator

### 12.1 Sphere Generator

* Tạo đầu thú / thân tròn

### 12.2 Axial Shape Generator

* Tạo mũ, ống, thân amigurumi
* Vẽ profile bằng chuột

---

## 13. Xuất file (Export)

* Text pattern
* SVG chart chuẩn crochet
* SVG + topology
* GLTF cho Blender

---

## 14. Khi nào nên dùng CrochetPARADE?

* Amigurumi phức tạp
* Lace / filet
* Ráp nhiều mảnh
* Viết pattern để bán / chia sẻ

---

## 15. Tổng kết tư duy học

CrochetPARADE **không dành cho học vẹt**.

Muốn dùng tốt, bạn cần:

* Hiểu hình học crochet
* Hiểu thứ tự móc
* Nghĩ pattern như một **đồ thị**

Khi đã quen, bạn sẽ:

* Ít lỗi hơn
* Viết pattern nhanh hơn
* Nhìn mẫu → suy ra chart

---

*Hết – tài liệu nền tảng đầy đủ để học nghiêm túc CrochetPARADE* 🧶🔥
