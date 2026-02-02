# Định nghĩa các kiểu mũi khâu mới

Các mũi khâu mới được xác định bằng cách sử dụng `DEF: definition`, nên đặt trên một dòng mới.

## Tạo alias

Nếu bạn sử dụng một chuỗi mũi khâu lặp đi lặp lại, bạn có thể muốn tạo bí danh (alias) cho chúng:

```js
DEF: new_stitch_sequence_alias=stitch1,stitch2,...
#Example:
DEF: p=3ch,ss@5[%,-4] 
```

> Bạn có thể sử dụng bí danh trong một pattern theo cách tương tự như sử dụng bất kỳ mũi khâu nào. Với một ngoại lệ đáng chú ý: Bí danh sẽ tăng số mũi khâu trong một hàng không phải tăng thêm 1 mà tăng bằng số mũi khâu có trong chuỗi. Cách xử lý bí danh là bằng cách thay thế chuỗi đơn giản, vì vậy kết quả tính toán sẽ không tham chiếu đến tên của bí danh theo bất kỳ cách nào.

> Tên gọi khác của mũi khâu `p` trong ví dụ trên là mũi `picot-3`: móc 3 mũi bính, sau đó móc mũi trượt vào mũi trước mũi `picot`.

Việc thay thế bí danh được thực hiện trước khi tính bộ đếm.

Ví dụ:

```js
$k=0$
DEF: scA=sc@A[k]
5ch,ch.A[0],ch.A[1],ch,turn
$k=1$,sk,3ch,scA
```

Mũi khâu `scA` được thay thế trước bằng ký tự cố định `sc@A[k]` và chỉ sau đó `k` mới được tính là 1 (do `$k=1$`), dẫn đến kết quả là `sc@A[1]`. Do đó, `sc` gắn vào `ch` được đánh dấu thứ hai `ch.A[1]` và `$k=0$` không có tác dụng.

## Sao chép một mũi khâu (cho phép chỉnh sửa)

Giả sử một pattern yêu cầu bạn sử dụng mũi móc đơn ngược (`rsc`). Mũi móc này có hình dạng tổng thể (chiều cao và chiều rộng) và cấu trúc (độ kết nối) gần giống với mũi móc đơn, vì vậy bạn chỉ cần sử dụng mũi `sc`. Tuy nhiên, giả sử bạn muốn sử dụng tên `rsc` trong pattern. Sử dụng `DEF: rsc=sc` là một lựa chọn, nhưng tên `rsc` sẽ không xuất hiện trong màn hình render. Nếu bạn muốn tên đó cũng hiển thị trong màn hình render, thì bạn có thể sử dụng `Copy()`:

```js
DEF: new_stitch=Copy(old_stitch_name)
# Example:
DEF: scbl = Copy(sc) 
```

Nếu bạn muốn điều chỉnh độ cao của mũi khâu mới tạo hoặc mũi khâu đã có, bạn có thể làm như sau:

```js
DEF: new_stitch=Copy(old_stitch_name,new_height) 
# Example:
DEF: dc=Copy(dc,3)
```

Ví dụ trên ghi đè lên mũi khâu `dc` hiện tại với chiều cao mới là 3 đơn vị.

Bạn cũng có thể thay đổi độ rộng của mũi khâu: 

```js
DEF: new_stitch=Copy(old_stitch_name, new_height, new_width) 
# Example: 
DEF: narrow_sc=Copy(sc,1,0.8)
```

> Lưu ý: Bạn phải chỉ định thêm chiều cao nếu bạn đang chỉ định cho chiều rộng, vì đó tham số thứ nhất là chiề u cao.

## Định nghĩa và ngữ pháp của các mũi khâu thô.

Có thể sử dụng ngữ pháp "mũi khâu thô" để định nghĩa các mũi khâu mới một cách ngắn gọn. Bên trong code, định nghĩa các mũi khâu cơ bản bằng cách sử dụng ký hiệu viết tắt đó. Sau đó được dịch sang định dạng JSON. Ngữ pháp để định nghĩa một mũi khâu mới như sau:

```js
DEF: new_stitch=&comment^top_nodes:bottom_nodes~attachments:other_nodes:connections
```

Các thuật ngữ “top_nodes” và “bottom_nodes” ở đây đề cập đến các phần cụ thể của một mũi móc. 

- Nút trên (top_nodes) tương ứng với đỉnh của một mũi móc, thường được nhận biết bởi hình chữ 'V' được tạo thành ở đỉnh của mũi móc. Đây là nơi kim móc được đưa vào khi thực hiện một mũi móc truyền thống. 
- Mặt khác, nút dưới (bottom_nodes) đề cập đến các điểm nối của các mũi móc, đó là các nút trên của các mũi móc khác đã được thực hiện trước đó.

Dưới đây là phân tích chi tiết các thành phần khác nhau của một kiểu mũi khâu mới được định nghĩa theo cách này:

### comment

Trường chú thích (comment) là tùy chọn và được định nghĩa ở đầu phần định nghĩa mũi khâu, sau ký hiệu `&` và trước ký hiệu `^`. Chúng có thể là một mô tả ngắn gọn về mũi khâu, nhưng không được sử dụng trong code. Chú thích không được chứa bất kỳ ký tự nào ở đây: `^`, `:`, `~`. 

Ví dụ, trong phần định nghĩa mũi khâu 

```js
&a sc cluster of 3 stitches^A(sc):B~A-B:C;D;E;F;G;H:!-1-A;B-1/3-C;C-1/3-D;D-1/3-A;B-1/3-E;E-1/3-F;F-1/3-A;B-1/3-G;G-1/3-H;H-1/3-A
```

Chuỗi "a sc cluster of 3 stitches" là một comment.

### top_nodes

Các nút trên (top_nodes) được định nghĩa sau ký hiệu `^` và được phân tách bằng dấu chấm phẩy (;). Mỗi nút trên phải có loại đường khâu được chỉ định trong ngoặc đơn sau tên đường khâu. 

Ví dụ, trong định nghĩa đường khâu 

```js
&sc2inc^A(sc);B(sc):C~::!-1-A;A-1-B;C-1-A;C-1-B
```

`A(sc)` là một nút trên trong đó: `A` là tên đường khâu và `sc` là loại đường khâu. 

Thứ tự viết các nút trên quy định thứ tự chúng được xâu chuỗi với nhau.

### bottom_nodes

Các nút dưới (bottom_nodes) được định nghĩa sau ký hiệu `:` đầu tiên và được phân tách bằng dấu chấm phẩy (;). Không giống như các nút trên, các nút dưới không có loại mũi khâu được chỉ định trong ngoặc đơn. Thay vào đó, chúng có thể có một tiền tố số tùy chọn cho biết độ sâu gắn kết. 

Ví dụ, trong định nghĩa mũi khâu 

```js
&funky^A(funky):B;2C;D~A-D::!-1-A;B-1-A;C-1-A;D-1-A
```

`B` là một nút dưới với độ sâu gắn kết là 1 (mặc định khi không có số nào được chỉ định), trong đó `C` có độ sâu gắn kết là 2, có nghĩa là: Mũi khâu `A` gắn vào điểm gắn kết của `C`, chứ không phải trực tiếp vào `C`.

Một nút dưới theo sau bởi `[front]` hoặc `[back]` chỉ định rằng mũi khâu được thực hiện ở vòng trước/vòng sau/chân mũi. Ví dụ, định nghĩa mặc định của mũi kép vòng sau là `&dcbl^A(dcbl):B[back]~A-B::!-1-A;B-2-A`. Khoảng cách "dính" mặc định ở phía trước/phía sau là 0,2 lần chiều dài chuỗi. Bạn có thể thay đổi điều đó bằng cách thêm một số sau phía trước/phía sau. Vì vậy, ví dụ, định nghĩa của mũi kép chân trước là: `&fpdc^A(fpdc):B[front0.6]~A-B::!-1-A;B-1.5-A`.

Thứ tự viết các nút dưới xác định thứ tự gắn kết của mũi khâu hiện tại với các nút phía trên của các mũi khâu trước đó.

### attachments

Các phần đính kèm (attachments) được định nghĩa sau ký hiệu `~` và được phân tách bằng dấu chấm phẩy (;). Mỗi phần đính kèm là một cặp tên nút trên và nút dưới được phân tách bằng `-`. Tên nút trên phải đứng trước, theo sau là tên nút dưới. 

Ví dụ, trong định nghĩa đường khâu 

```js
&ss^A(ss):B~A-B::!-1-A;B-0.4-A
```

`A-B` là một phần đính kèm cho biết nút trên `A` được đính kèm với nút dưới `B`. Điều này chỉ được sử dụng để tìm điểm đính kèm của một đường khâu có độ sâu đính kèm lớn hơn 1.

### other_nodes

Các nút khác (other_nodes) được định nghĩa sau ký hiệu `:` thứ 2 trong chuỗi và được phân tách bằng dấu chấm phẩy (;). Mỗi nút khác phải có loại đường khâu được chỉ định trong ngoặc đơn sau tên đường khâu. Nếu không có loại đường khâu nào được chỉ định, nó sẽ mặc định là 'hidden'. 

Ví dụ, trong định nghĩa đường khâu 

```js
&a sc cluster of 3 stitches^A(sc):B~A-B:C;D;E;F;G;H:!-1-A;B-1/3-C;C-1/3-D;D-1/3-A;B-1/3-E;E-1/3-F;F-1/3-A;B-1/3-G;G-1/3-H;H-1/3-A
```

Các nút `C` từ đến `H` đều là các nút khác, với loại được đặt thành hidden.

### connections

Các kết nối (connections) được định nghĩa sau ký hiệu `:` thứ ba và được phân tách bằng dấu chấm phẩy (;). Mỗi kết nối là một cặp tên nút được phân tách bằng `-`, với giá trị độ dài nằm giữa các dấu gạch ngang. Tên nút đầu tiên (phần đuôi của kết nối) phải đứng trước, tiếp theo là giá trị độ dài, và sau đó là tên nút thứ hai (phần đầu của kết nối). 

Ví dụ, trong định nghĩa mũi khâu 

```js
&ss^A(ss):B~A-B::!-1-A;B-0.4-A
```

`!-1-A` và `B-0.4-A` là các kết nối cho biết nút `!` được kết nối với nút `A` có độ dài là 1, và nút `B` được kết nối với nút `A` có độ dài là 0.4. Lưu ý rằng nút `!` đại diện cho mũi khâu trước đó, mà mũi khâu hiện tại được kết nối đến.

Các kết nối có thể được ẩn đi bằng cách thêm dấu `*` phía trước kết nối. Ví dụ, kết nối `*Z-3-F` được ẩn đi và chỉ hiển thị dưới dạng các sợi màu xám mỏng.

Nếu muốn thêm một nút trên không giao nhau với nút trên trước đó, thì có thể sử dụng độ dài `skip` cho kết nối đó. 

Ví dụ, "mũi khâu" `start_anew` được định nghĩa nội bộ là 

```js
&start_anew^A(hidden):~::!-skip-A
```

Như vậy, không có kết nối giữa mũi khâu tiếp theo và mũi khâu trước đó, tương tự như việc bắt đầu một phần mới của dự án.

> Khuyến nghị: Nếu sử dụng "Transform objects" để di chuyển/xoay các đối tượng rời rạc (như các chi của amigurumi), bạn cần đảm bảo rằng việc phát hiện đối tượng hoạt động chính xác. Để làm được điều đó, hãy đảm bảo rằng các kết nối cho các mũi khâu không được phép làm tách rời một đối tượng khỏi đối tượng khác (tức là tất cả các mũi khâu ngoại trừ "start_anew" hoặc "start_a_new_chain") đều có tất cả các nút ẩn và nút trên được kết nối với các nút trước đó. 

> Do đó, khi viết ra các kết nối, hãy đảm bảo rằng có ít nhất một kết nối đến mỗi nút ẩn/trên (gọi là "A") chạy về phía nút đó (ví dụ: "!-0.5-A"). Ngoài ra, khi viết ra các kết nối, tôi khuyên bạn nên liệt kê các kết nối "blue" (cấp cao nhất) trước. Điều này đảm bảo vị trí nút chính xác khi xuất biểu đồ móc sang SVG. Tất cả các mũi khâu tiêu chuẩn đều tuân theo các hướng dẫn này.