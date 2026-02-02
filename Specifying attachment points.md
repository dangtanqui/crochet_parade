# Xác định các điểm gắn kết

Các mũi khâu trên một hàng/vòng nhất định sẽ tự động được nối từng mũi một với các mũi khâu liền kề ở hàng/vòng trước đó. Nếu sản phẩm được xoay ở cuối hàng, điều đó cũng sẽ được tự động tính đến.

Tuy nhiên, trong móc len, người ta thường cần nối các mũi mới vào các mũi trước đó không liền kề. Để cho phép điều đó, chỉ định các điểm nối sau ký hiệu `@`, theo sau một mũi trong pattern. Ví dụ:

```js
3sc,dc@[-1,3],dc
```

Chỉ định rằng điểm nối của mũi kép `dc` nên được di chuyển đến mũi thứ 4 (việc đếm mũi và hàng bắt đầu từ 0) của hàng/vòng trước đó (được chỉ định bằng chỉ số âm: -1). Mũi tiếp theo `dc` được thực hiện ở mũi sau đó.

Quan trọng: Điểm gắn kết được chỉ định rõ ràng đầu tiên sẽ được ưu tiên. Ví dụ:

```js
(sc,dc@B,(tr@C)@D)@A
```

Mũi móc đơn `sc` gắn vào `A`, mũi móc kép `dc` gắn vào `B`, và mũi móc ba `tr` gắn vào `C`.

Điều này đúng ngay cả khi có nhiều điểm gắn kết được chỉ định.

Ví dụ:

```
(sc,dc@B,(tr@1C)@D)@A,hdc
```

Mũi móc ba `tr` gắn vào `C` và điểm gắn kết đó chỉ cập nhật điểm gắn kết `@1`. Do đó, mũi móc nửa kép `hdc` gắn vào mũi sau `B` (lần cập nhật cuối cùng cho điểm gắn kết 0, được chỉ định bằng `@`) theo thứ tự gắn kết mặc định.

> Các nhãn như `@A`, các điểm gắn kết như `@1` và thứ tự gắn kết đều được định nghĩa trong phần tiếp theo.

Có nhiều cách khác nhau để xác định điểm gắn mũi khâu:

Bắt đầu hàng/vòng mới: nhập một dòng mới (không có điểm nối rõ ràng)
Điểm gắn kết đầu tiên được khởi tạo mặc định ở mũi khâu đầu tiên. Vì vậy, trong ví dụ này 5ch,sc,dc, mũi móc đơn (sc) gắn vào mũi xích đầu tiên và mũi móc kép (dc) gắn vào mũi xích thứ hai (tính từ 1).

Sau khi thêm một dòng mới vào văn bản, trình tự nối mũi sẽ tự động thiết lập lại, và mũi tiếp theo sẽ được nối vào mũi đầu tiên (hay đúng hơn là mũi thứ 0) của dòng trước đó nếu không có lệnh quay mũi nào ở dòng trước đó; hoặc mũi tiếp theo sẽ được nối vào mũi cuối cùng của dòng trước đó nếu có lệnh quay mũi ở cuối dòng trước đó. Dưới đây là một ví dụ minh họa:


8ch,ch.A,ch
9sc,turn
sk,ss,8sc,ch,turn
sk,hdc,sc@A,sc,dc
2sk,2ch,tr
Dòng 2: Mũi móc đơn đầu tiên trên dòng thứ hai (tính từ 1) nối với mũi bính đầu tiên của dòng thứ nhất. Sau đó, các mũi tiếp theo được nối theo trình tự dọc theo Dòng 1.

Dòng 3: Mũi ss ở dòng thứ ba nối với mũi sc thứ 8 của dòng thứ hai. Lý do là việc nối bắt đầu từ mũi cuối cùng (do thao tác xoay ở cuối dòng 2), nhưng mũi sc cuối cùng bị bỏ qua bởi thao tác sk ở đầu dòng 3. Các mũi tiếp theo được nối theo trình tự ngược lại với các mũi ở dòng 2 do lệnh xoay ở cuối dòng 2 (xem phần Hướng nối mũi theo trình tự). Trong ví dụ này, mũi sc cuối cùng trong số 8 mũi sc bỏ qua điểm bắt đầu của dòng 2 và do đó được nối với mũi bính cuối cùng của dòng 1, là mũi đã móc trước đó (tức là điểm nối tiếp theo được tính theo thứ tự ngược lại).

Dòng 4: Có một khúc cua ở cuối Dòng 3, vì vậy điểm nối được đặt lại thành mũi cuối cùng của Dòng 3 sau dòng mới. Mũi hdc nối vào mũi sc cuối cùng của dòng trước (sau khi bỏ qua mũi bính cuối cùng bằng sk). Sau đó, mũi sc@A nối vào mũi bính ở Dòng 1 được đánh dấu bằng ch.A (xem phần về Nhãn đơn giản bên dưới). Mũi sc tiếp theo ở Dòng 4 nối vào mũi bính cuối cùng của Dòng 1 (hướng nối tuần tự là tiến về phía trước vì có số khúc cua chẵn giữa Dòng 1 và Dòng 4). Vì chúng ta đã hết mũi ở Dòng 1, mũi dc nối vào mũi sc đầu tiên ở Dòng 2 vì đó là mũi tiếp theo được thực hiện trong dự án (mặc dù nó nằm ở hàng/vòng/dòng tiếp theo).

Dòng 5: Điểm gắn kết được đặt lại do dòng mới. Không có điểm quay ở cuối Dòng 4, vì vậy điểm gắn kết tiếp theo là mũi đầu tiên của Dòng 4. Ký hiệu 2sk có nghĩa là mũi hdc và mũi sc@A bị bỏ qua ở Dòng 4. Do đó, mũi tr gắn vào mũi sc thứ hai (ngay trước mũi dc) ở Dòng 4. Các mũi bính không có điểm gắn kết nên chúng không làm tăng vị trí gắn kết.

Đính kèm trực tiếp: @[2,10]
Gắn trực tiếp vào một tọa độ mũi khâu cụ thể được chỉ định bằng một cặp số nguyên, ví dụ  @[2,10]: . Số nguyên đầu tiên chỉ định số hàng/vòng. Số nguyên thứ hai chỉ định mũi khâu trong hàng đó. Việc đếm mũi khâu/hàng/vòng bắt đầu từ 0, vì vậy trong ví dụ trên, điểm gắn nằm ở mũi khâu thứ 11 của hàng thứ 3.

Số âm biểu thị việc đếm từ cuối, bắt đầu từ -1mũi/hàng/vòng cuối cùng; -2mũi/hàng/vòng trước đó, v.v. Việc đếm hàng/vòng bắt đầu từ đầu dự án. Việc đếm mũi bắt đầu từ mũi đầu tiên của hàng như được ghi trong hướng dẫn, bất kể turnchỉ dẫn nào khác. Hàng mũi hiện tại và vị trí mũi có thể được chỉ định bằng % ký hiệu , do đó @[%,%-3]biểu thị hàng hiện tại, ba mũi trước mũi đang được thực hiện.

Đính kèm với kiểu mũi khâu đếm @[sc:-1,3]
Các ký hiệu gắn kèm kiểu mũi khâu trước dấu hai chấm chỉ định rằng việc đếm mũi khâu trong một hàng được thực hiện trên các mũi khâu thuộc loại đó. Ví dụ, @[sc:-1,3]chỉ định rằng mũi khâu hiện tại được thực hiện ở mũi móc đơn (sc) thứ 4 của hàng trước, chứ không phải là mũi thứ 4 nói chung. Hướng đếm không nhất thiết phải theo hướng các mũi khâu được viết (so sánh với ví dụ trên), mà theo hướng móc. Xem phần "Hướng gắn mũi khâu tuần tự".

Đính kèm với vị trí tương đối: @[@+1]
Điểm gắn kết cuối cùng được lưu trữ trong @ký hiệu, ký hiệu này có thể được tham chiếu trong một điểm gắn kết khác. Ví dụ, điều dc,dc@[@]này ngụ ý rằng dcmũi khâu thứ hai nên được thực hiện ở cùng một vị trí với mũi khâu trước đó dc.

Ta có thể di chuyển lên xuống hàng bằng cách cộng thêm các số nguyên vào @. Vì vậy, @[@+2]có nghĩa là nối hai mũi sau điểm nối cuối cùng . Hướng này theo hướng ta đang làm việc (xem phần "Hướng nối mũi tuần tự"), do đó các lượt quay được tính đến.

Người ta cũng có thể kết hợp mã định danh vị trí tương đối với mã định danh loại mũi khâu. Ví dụ, @[sc:@+1]có nghĩa là gắn vào scmũi khâu tiếp theo sau điểm gắn cuối cùng. Nói chung, một biểu thức gắn có dạng @[TYPE:@+k] được đánh giá qua hai bước:

1) Đầu tiên, tính vị trí cơ sở bằng cách di chuyển k mũi từ "@" theo hướng móc (cùng hướng với hướng nối tiếp; các lượt xoay được tính đến). Điều này tạo ra vị trí mũi trung gian "@+k" được xác định dựa trên tất cả các mũi trong hàng, bất kể loại mũi nào.

2) Sau đó, bắt đầu từ vị trí trung gian đó, tìm theo hướng móc mũi khâu đầu tiên có kiểu khớp với TYPE. Nối vào mũi khâu đó.
Nếu không tìm thấy mũi khâu nào thuộc LOẠI được yêu cầu tại "@+k" hoặc sau đó theo hướng móc, trình phân tích cú pháp phải báo lỗi.
Ghi chú:
- @[sc:@] gắn vào mũi sc gần nhất tại hoặc sau "@". Nếu "@" đã nằm trên một mũi sc, nó sẽ gắn vào đó. Nếu không, nó sẽ gắn vào mũi sc tiếp theo.
- Lệnh @[sc:@+1] trước tiên di chuyển một mũi từ vị trí "@", sau đó tìm kiếm mũi sc đầu tiên tại hoặc sau vị trí mới đó. Nếu "@" không nằm trên mũi sc nào, thì lệnh @[sc:@] và @[sc:@+1] sẽ cùng tìm đến một mũi sc tiếp theo.
- Trong một nhóm được gắn nhãn như (sc,dc)@[@+1], nhãn được phân bổ trước và sau đó mỗi phần gắn được đánh giá riêng biệt, vì vậy sc@[@+1],dc@[@+1] gắn vào các mũi khâu liên tiếp, chứ không phải vào cùng một mũi khâu.
Đính kèm vào nhãn
Nhãn đơn giản
Trong đan móc, người ta thường dùng kim đánh dấu mũi để theo dõi vị trí của các mũi đan cụ thể. Tương tự, bất kỳ mũi đan nào ở đây cũng có thể được gắn nhãn sau một ký hiệu .. Ví dụ, trong sc,sc.A,2chhình thứ hai , mũi đan scđược gắn nhãn A. Một mũi đan có thể có nhiều nhãn có tính chất phân phối. Vì vậy, (3ch.A,sc).Bđiều này ngụ ý rằng tất cả các mũi xích đều có cả nhãn Avà B, trong khi scmũi đan chỉ mang nhãn B.

Sau đó, người ta có thể thực hiện một mũi khâu trên nhãn đó bằng cách gắn vào Abằng cách viết sc,sc.A,2ch,ss@A. Khi cần sử dụng nhiều nhãn tương tự, người ta có thể sử dụng các nhãn khác nhau bởi các nhãn nội bộ là số nguyên, chẳng hạn như sc,sc.A[0],sc,sc,sc.A[1]. Ở đây A[0]và A[1]được coi là các nhãn khác nhau.

Như đã đề cập trước đó, một mũi khâu chỉ có thể gắn vào một nhãn duy nhất, kế thừa điểm gắn gần nhất về mặt cú pháp. Ví dụ, trong (sc@A)@Bmũi khâu sc, nó gắn vào A. Các điểm gắn cũng được phân bố. Do đó, (sc,dc,sc@A,sc)@Btương đương với sc@B,dc@B,sc@A,sc@B.

Các nhóm mũi khâu được đánh dấu
Những điều cơ bản
Khi nhiều mũi khâu có cùng nhãn, ta gọi đó là một nhóm có nhãn. Có thể gắn vào toàn bộ nhóm hoặc các mũi khâu cụ thể trong nhóm. Ví dụ 5ch.A, nhãn này A đề cập đến toàn bộ nhóm 5 mũi xích. Ta có thể hình dung việc gắn vào khoảng trống của nhóm đó bằng cách thực hiện: 5ch.A,dc,2ch,2sc@A. Trong trường hợp này, cả hai scmũi khâu sẽ được gắn vào khoảng trống 5 mũi xích và được phân bố đều trên khoảng trống đó. Nếu các vị trí phân bố đều không trùng khớp với các nút mũi khâu hiện có trong nhóm có nhãn, thì các nút ẩn sẽ được tạo ra ở giữa và các mũi khâu sẽ được gắn vào đó. Sự phân bố các nút ẩn là đồng đều dọc theo chiều dài của nhóm có nhãn với giả định rằng tất cả các mũi khâu trong một nhóm có nhãn đều có cùng chiều rộng (chiều cao mũi khâu có thể khác nhau).

Quan trọng: Một nhóm được gắn nhãn (nhiều mũi khâu có cùng nhãn, ví dụ: .A) phải là một dãy các mũi khâu liền kề. Việc sử dụng cùng một nhãn cho các mũi khâu không liền kề/rời rạc là một lỗi. Trong trường hợp sau, hãy sử dụng các nhãn khác nhau hoặc sử dụng nhãn được đánh chỉ mục (nhãn có bộ đếm) để đánh dấu các nhóm riêng biệt, ví dụ .A[0]: , .A[1](hoặc .A[k++]với $k=0$các bước tăng và ). Tính liền kề được kiểm tra trên biểu đồ mũi khâu. "Liền kề" bao gồm các kết nối trực tiếp từ trên xuống dưới trong cùng một mũi khâu và các kết nối trực tiếp từ dưới lên trên; các kết nối đi qua các nút ẩn không được tính. Nếu bạn sử dụng SORT_LABEL:, việc kiểm tra tính liền kề này được áp dụng sau khi sắp xếp.

Quan trọng: Sau khi sắp xếp, các mũi khâu cho nhãn đó vẫn phải liền kề nhau trong biểu đồ mũi khâu. Nếu chúng không liền kề, trình phân tích cú pháp Cannot use same labels over non-adjacent stitchessẽ báo lỗi. "Liền kề" bao gồm các kết nối trực tiếp từ trên xuống dưới trong cùng một mũi khâu, và các kết nối trực tiếp từ dưới lên trên. Các kết nối đi qua các nút ẩn không được tính là liền kề và sẽ gây ra lỗi.

Quan trọng: Các mũi khâu nối với nhóm được đánh dấu phải nối với các mũi khâu đã được xác định (= đã được móc/thực hiện) tại điểm đó trong hướng dẫn. Trên thực tế, điều này có nghĩa là: nối vào các mũi/hàng trước đó, chứ không phải vào các mũi khâu xuất hiện sau trong văn bản hướng dẫn.

Chỉ để cho vui, đây là một ví dụ cực kỳ gượng ép, thoạt nhìn có vẻ vi phạm cả quy tắc liền kề và quy tắc tương lai ở trên nhưng thực tế lại không: 
9ch,(ch.B).A,ch,dc@A,tr.A@B,2hdc@A
Giải thích: Mũi ch và mũi tr được gắn nhãn cùng là A và liền kề nhau (mũi tr nối với B, là nhãn được mang bởi mũi ch; do đó hai mũi khâu này có chung kết nối nút dưới-trên). Nhóm được gắn nhãn A có hai mũi khâu: 1 mũi ch, 1 mũi tr. Có ba mũi khâu được móc vào A: 1 mũi dc, 2 mũi hdc. Sau đó, mã sẽ xác định rằng mũi dc nối với mũi khâu đầu tiên trong nhóm được gắn nhãn (mũi xích), đây không phải là mũi khâu tương lai so với mũi dc; mũi hdc cuối cùng nối với mũi tr (đây không phải là mũi khâu tương lai so với các mũi hdc); và mũi hdc đầu tiên nối vào một mũi khâu ẩn nằm giữa mũi ch và mũi tr.

Gắn vào trụ của một mũi khâu: .A^ .A^1
Để gắn vào chân của một mũi khâu, hãy đặt dấu mũ (^) sau định nghĩa của nhãn ^. Có thể thêm một số nguyên theo sau ^để chỉ định chân nào của mũi khâu cần gắn vào nếu có nhiều hơn một chân. Ví dụ:

8*ch,turn
7*sc,dc.B^,turn
5ch,4*sc@B
Dưới đây là hai ví dụ với hai bài đăng khác nhau làm điểm đính kèm:

8ch,turn
6sc,dc2tog.B^0,turn
5ch,4*sc@B
có thể so sánh với:

8ch,turn
6sc,dc2tog.B^1,turn
5ch,4*sc@B
Bỏ qua các mũi viền của một nhóm: .A! .A!0 .A!1
Nếu muốn gắn một tập hợp các mũi khâu vào một nhóm mũi khâu, thì mặc định hai mũi khâu viền (đầu tiên và cuối cùng) của nhóm là các điểm gắn hợp lệ của tập hợp đó. Tuy nhiên, người dùng có thể muốn bỏ qua hai mũi khâu đó và thay vào đó gắn vào các khoảng trống và các mũi khâu nằm giữa hai mũi khâu viền đó. Khi đó, bằng cách thêm nhãn, người dùng có thể chỉ định xem !có muốn bỏ qua cả hai mũi khâu viền, !0bỏ qua mũi khâu đầu tiên hay !1bỏ qua mũi khâu cuối cùng hay không.

Đây là một ví dụ:

10ch,turn
sk,9sc,turn
ch,2sc,4ch.A!,4sk,3sc,turn
4ch,5sc@A,4ch,sc
5 scmũi khâu sẽ được nối vào khoảng trống 4 mũi bính được đánh dấu bằng A, tránh mũi đầu tiên và mũi cuối cùng ch. Hãy hiển thị cùng một bộ hướng dẫn với 4ch.A, 4ch.A!0, 4ch.A!1để thấy sự khác biệt. Lưu ý rằng tham chiếu @Akhông nên chứa !hướng dẫn .

Người ta có thể kết hợp !bổ ngữ này với ^ bổ ngữ khác:

8*ch,turn
7*sc,dc.B^!,turn
5ch,4*sc@B
Đây là một cấu trúc mạng phức tạp hơn một chút:

9ch,turn
8sc,dc.A^,turn
4ch,[sc,sc.B^!,sc]@A
4ch,3sc@B
Thêm các mũi khâu viền vào một nhóm: .A+ .A+0 .A+1 .A+! .A+!0
Giả sử bạn muốn thêm các mũi khâu vào một khoảng trống trong chuỗi. Nếu bạn muốn các mũi khâu lấp đầy khoảng trống một cách đều đặn cho đến các mũi khâu viền quanh khoảng trống đó, bạn sẽ phải thêm các mũi khâu trước và/hoặc sau khoảng trống đó vào nhóm khoảng trống chuỗi đã được gắn nhãn. Điều đó có thể khá rắc rối. Vì vậy, để làm điều đó tự động, hãy thêm dấu / +sau định nghĩa nhãn khoảng trống chuỗi để thêm cả hai mũi khâu viền, hoặc dấu +0/ +1để thêm mũi khâu viền trước/sau.

Hãy so sánh những điều sau:

8ch,turn
2sc,3ch.C+,2sc,turn
3ch,5sc@C,sc@[-1,0]
với

8ch,turn
2sc,3ch.C+!,2sc,turn 
3ch,5sc@C,sc@[-1,0]
và với

8ch,turn
2sc,3ch.C,2sc,turn
3ch,5sc@C,sc@[-1,0]
Đảo ngược thứ tự gắn một nhóm mũi khâu vào một nhóm mũi khâu khác: @A ~
Khi gắn một tập hợp các mũi khâu vào một nhóm các mũi khâu khác, mã lập trình cố gắng sắp xếp các mối nối theo cách ít gây xáo trộn nhất (ví dụ: xoắn) cho dự án, nhưng đôi khi nó thất bại. Ví dụ, hiển thị như sau:

10ch,turn
sk,8sc,sc.A!,turn
4ch.A!,sk,9tr,turn
1ch,sk,8sc,7sc@A
Nếu bạn muốn 7 scmũi khâu nối với nhóm 4 mũi bính được nối theo thứ tự ngược lại, thì hãy thêm dấu ngã, ~, vào cuối nhãn nối, như trong:

10ch,turn
sk,8sc,sc.A!,turn
4ch.A!,sk,9tr,turn
1ch,sk,8sc,7sc@A~
So sánh với kết quả thu được từ lần chạy tập lệnh trước đó.

Lưu ý rằng cú pháp của CrochetPARADE phân phối nhãn trên các tập hợp mũi khâu. Vì vậy, (3sc).A~tương đương với sc.A~,sc.A~,sc.A~. Do đó, trong ví dụ bên dưới, hai tập hợp (3sc).A~được coi là một tập hợp (6sc).A~. Vì vậy, mã sẽ đảo ngược tất cả 6 mũi khâu và sau đó gắn chúng vào nhóm A.

9ch,turn
sk,(ch,5sc).A,3sc,turn
sk,2sc,3sc@A~,3sc@A~
tương đương với:
9ch,turn
sk,(ch,5sc).A,3sc,turn
sk,2sc,6sc@A~
Nếu muốn gắn mũi khâu đầu tiên 3sctheo chiều ngược lại, rồi mới đảo chiều mũi khâu tiếp theo 3scvà gắn chúng lần lượt, thì phải sử dụng các bộ mũi khâu (xem "Gắn nhiều bộ mũi khâu vào một nhóm được đánh dấu") như sau:

9ch,turn
sk,(ch,5sc).A[],3sc,turn
sk,2sc,3sc@A[;0]~,3sc@A[;1]~
Tuy nhiên, nếu ta kết hợp kiểu gắn kết bình thường (thuận) và kiểu gắn kết ngược (lùi) như trong trường hợp sau:

9ch,turn
sk,(ch,5sc).A,3sc,turn
sk,2sc,3sc@A~,3sc@A
Khi đó, phần tử thứ nhất 3scvà phần tử thứ hai 3scđược coi là các tập hợp riêng biệt. Đoạn mã sẽ ghép 3 phần tử đầu tiên theo thứ tự ngược lại, sau đó ghép 3 phần tử tiếp theo theo thứ tự bình thường. Nói cách khác, ví dụ trên tương đương với:

9ch,turn
sk,(ch,5sc).A[],3sc,turn
sk,2sc,3sc@A[;0]~,3sc@A[;1]
và tương tự đối với bất kỳ sự kết hợp nào giữa các phần gắn phía trước và phía sau. Do đó, hai ví dụ sau đây là tương đương:

9ch,turn
sk,(ch,5sc).A,3sc,turn
sk,2sc,2sc@A~,2sc@A,2sc@A~
cũng giống như

9ch,turn
sk,(ch,5sc).A[],3sc,turn
sk,2sc,2sc@A[;0]~,2sc@A[;1],2sc@A[;2]~
Xem phần "Hướng gắn mũi khâu tuần tự" để biết cách mã chọn hướng mặc định để gắn các mũi khâu.

Nhiều bộ mũi khâu gắn vào một nhóm được đánh dấu: @A [2;1]
Nếu cần nối nhiều nhóm mũi khâu vào một nhóm mũi khâu có nhãn, thì thứ tự nối các nhóm đó có thể được chỉ định bằng dấu chấm phẩy như sau: 6dc.A[12],5ch,3sc@A[12;1],3sc@A[12;0]. Trong ví dụ này, nhóm 3 mũi sc thứ hai sẽ được nối với 3 mũi dc đầu tiên , và 3 mũi sc đầu tiên sẽ được nối với 3 mũi sc thứ hai. Lưu ý rằng để sử dụng chức năng này, cần phải có nhãn trong dấu ngoặc vuông, chẳng hạn như A[12]. Nếu không chỉ định thứ tự, thì các nhóm mũi khâu sẽ được nối theo thứ tự như đã viết, vì vậy trong 6dc.A[12],5ch,3sc@A[12],3sc@A[12], 6 scmũi khâu được nối liên tiếp trong 6 dc mũi khâu.

Lưu ý rằng mỗi bộ có thể được đảo ngược nếu bạn thêm chữ "a" ~vào cuối nhãn tệp đính kèm. So sánh:

10ch,turn
sk,8sc,sc.A[]!,turn
4ch.A[]!,sk,9tr,turn
1ch,sk,8sc,3sc@A[;1]~,4sc@A[;0]
với

10ch,turn
sk,8sc,sc.A[]!,turn
4ch.A[]!,sk,9tr,turn
1ch,sk,8sc,3sc@A[;1],4sc@A[;0]
Gắn vào một mũi khâu cụ thể trong một nhóm được gắn nhãn: @A [][2]
Nếu muốn gắn vào kmũi khâu thứ mang cùng nhãn, thì cũng giống như trên, cần có nhãn trong ngoặc vuông, chẳng hạn như A[0]và vị trí mũi khâu sẽ theo sau trong một cặp ngoặc vuông khác: ví dụ @A[0][k]gắn vào kmũi khâu của nhóm mũi khâu có nhãn A[0]. Việc đếm được thực hiện theo cùng hướng với hướng khâu mặc định (xem "Hướng gắn mũi khâu tuần tự" bên dưới).

Các nhóm được gắn nhãn bằng SORT_LABEL
Đối với các nhãn đơn giản (nhãn không có bộ đếm như .A, .A[], .A[2,3]), bạn có thể kiểm soát thứ tự nhóm nhãn bằng cách sử dụng SORT_LABEL:thay vì thêm bộ đếm nhãn. Điều này đặc biệt hữu ích khi nhãn được tạo bởi công cụ Tools → Find project periphery hoặc bất cứ khi nào bạn gắn nhãn cho các mũi khâu liền kề (một yêu cầu đối với bất kỳ nhóm nhãn nào!) nhưng KHÔNG được sắp xếp theo vị trí liền kề và cần sắp xếp lại.

SORT_LABEL:Lưu trữ thứ tự xử lý cụ thể cho các mũi khâu có cùng nhãn. Dòng này có dạng:

SORT_LABEL: A = {3,4,2,1,0}
Điều này có nghĩa là: thu thập các mũi khâu được đánh dấu theo thứ tự chúng xuất hiện trong hướng dẫn của bạn (theo thứ tự chúng được móc); tức là turnhướng dẫn không ảnh hưởng đến thứ tự. Sau đó, sắp xếp lại danh sách đó sao cho 3mũi khâu thứ 3 trở thành mũi thứ 0, 4mũi thứ 4 trở thành mũi thứ 1, 2mũi thứ 2 vẫn là mũi thứ 2, v.v. Nói cách khác, mũi khâu thứ 0 được móc vào nhóm được đánh dấu bằng A sẽ được móc vào mũi thứ 3 của nhóm đó; mũi khâu thứ 1 được móc vào A sẽ được móc vào mũi thứ 4 của nhóm được đánh dấu bằng A, và cứ thế tiếp tục. Mảng được hiểu là chỉ số dựa trên 0, mặc dù chỉ số dựa trên 1 (1..N) cũng được chấp nhận và sẽ được chuyển đổi thành chỉ số dựa trên 0.

Tên nhãn có thể là A, B[], C[0], D[1,2], v.v. SORT_LABEL:và không chỉ dành riêng cho công cụ Periphery (mặc dù công cụ đó có thể tạo ra tên nhãn cho các mũi khâu xung quanh chu vi dự án của bạn); bạn có thể tự viết tên nhãn cho bất kỳ nhãn nào.

Nếu nhãn của bạn sử dụng cú pháp mảnh cạnh (ví dụ: .A+1), các mảnh cạnh sẽ được thêm vào sau khi sắp xếp khi SORT_LABEL:có mặt. Để tránh sự mơ hồ, bạn nên thêm nhãn vào các nút cạnh bằng tay.

Quan trọng (chỉ áp dụng cho nhãn đã sắp xếp): Khi SORT_LABEL:có mặt, và một mũi khâu được gắn nhãn mở rộng thành nhiều nút (ví dụ: tăng như dc2inc), bộ sắp xếp sẽ thử cả hai thứ tự nút trên cùng (từ trái sang phải và từ phải sang trái) cho mũi khâu đó trước khi đánh giá tính liền kề, để tính liền kề có thể được bảo toàn sau khi sắp xếp. Không có thao tác sắp xếp lại nội bộ nào được thực hiện khi SORT_LABEL:không được sử dụng cho nhóm được gắn nhãn đó.

Nhãn có bộ đếm: @A [++k] và .A[++k]
Lưu ý rằng thông thường, người ta cần tạo nhiều nhãn theo cách thức thuật toán. Khi đó, người ta có thể sử dụng một bộ đếm (một biến được khởi tạo bằng một số nguyên và sau đó có thể được tăng lên). Người ta khởi tạo bộ đếm bằng cách đặt biểu thức khởi tạo giữa hai $ dấu, chẳng hạn như $k=0$ở đầu dòng. Sau đó, người ta có thể tăng giá trị đó bằng cách sử dụng toán tử++ hoặc , hoặc viết (tương tự như ) hoặc (tương tự như ). Ví dụ, được đánh giá thành .-- prev k--knext k++k$m=0$, sc.A[m],sc.A[m++],sc.A[m],sc.A[++m],sc.A[m],sc.A[prev m],sc.A[m]sc.A[0],sc.A[0],sc.A[1],sc.A[2],sc.A[2],sc.A[1],sc.A[1]

Lưu ý rằng khi phân phối nhãn với bộ đếm, bộ đếm được đánh giá trước khi phân phối khi các mũi khâu được đặt trong ngoặc đơn, hoặc khi một số nguyên đứng trước MỘT mũi khâu (không được đặt trong ngoặc đơn) mà không có *ký hiệu. Vì vậy, $k=0$,2sc.A[k++],(dc,dc).A[k] được đánh giá thành sc.A[0],sc.A[0],dc.A[1],dc.A[1]. Nếu một mũi khâu được nhân với một số nguyên bằng toán *tử , thì nhãn được phân phối trước khi đánh giá bộ đếm. Ví dụ, $k=1$, 3*dc.A[k++]được đánh giá trước thành $k=1$,dc.A[k++],dc.A[k++],dc.A[k++]và sau đó thành dc.A[1],dc.A[2],dc.A[3], trong khi $k=1$, 3dc.A[k++]sẽ đánh giá bộ đếm trước khi phân phối nhãn để cho ra dc.A[1],dc.A[1],dc.A[1].

Lưu ý rằng nếu có dấu ngoặc vuông/ngoặc đơn, thì việc bỏ qua *toán tử sẽ không làm thay đổi kết quả. Vì vậy, $c=0$,2[sc].A[c++]tương đương với $c=0$,2*[sc].A[c++]và được đánh giá là [sc].A[0],[sc].A[1], và điều tương tự cũng áp dụng cho nhiều phép toán bên trong dấu ngoặc vuông.

Cũng cần lưu ý rằng việc thay thế định nghĩa được thực hiện sau cùng, sau khi các nhãn được đánh giá. Do đó, các mũi picot bên dưới, 3p.A[k++], được xử lý tương tự như 3sc.A[k++], cho ra p.A[0],p.A[0],p.A[0]. Ba mũi picot này không tương đương với 3*p.A[k++], mà khi đó lại được đánh giá thành p.A[0],p.A[1],p.A[2]. Đây là đoạn mã hoàn chỉnh: 
DEF: p=3ch,ss@1[%,%-4]
$k=0$,3p.A[k++]
Đoạn mã trên coi plà một mũi đơn, mặc dù định nghĩa của nó là một chuỗi gồm 4 mũi. Vì vậy, nó được phân tích cú pháp trước tiên thành , 
DEF:p=3ch,ss@1[%,%-4]
$k=0$,[p,p,p].A[k++]
sau đó được đánh giá thành 
DEF:p=3ch,ss@1[%,%-4]
[p,p,p].A[0]
như đã giải thích ở trên.

Lưu ý rằng phép toán đại số đếm được cho phép trong việc lập chỉ mục. Vì vậy, ví dụ, $k=3$,sc@A[(k++)%5]*5sẽ sử dụng toán tử modulo % , và sẽ được phân tích thành sc@A[3],sc@A[4],sc@A[0],sc@A[1],sc@A[2]. Điều này đặc biệt hữu ích khi thực hiện theo vòng, và nhãn đầu tiên mà bạn gắn vào không có chỉ mục 0.

Có thể đánh giá các bộ đếm trong chỉ mục bằng cách chọn "Mở rộng lệnh" và chọn "Thay thế bộ đếm chỉ mục sau khi mở rộng?".

CrochetPARADE cũng cung cấp tùy chọn "Đơn giản hóa hướng dẫn" và khi chọn "Thử đơn giản hóa việc đánh số thứ tự nhãn và tạo bộ đếm chỉ mục?", mã sẽ cố gắng thay thế các biểu thức như ch.A[0],ch.A[1],ch.A[2],ch.A[3]bằngch.A[$vara=0$vara],3*ch.A[++vara]

Nhiều đầu gắn kèm: @0 @1 @2
Lưu ý rằng trong móc len, chúng ta có thể móc qua lại giữa các hàng khác nhau, hoặc nói chung là ở các vị trí khác nhau trong một sản phẩm. Để theo dõi vị trí móc của mình ở các điểm gắn khác nhau, chúng ta có thể sử dụng các "đầu gắn" khác nhau, mỗi đầu được đánh số bằng một số nguyên sau ký @hiệu (mặc định @là @0). Các bộ đếm của đầu gắn này hoạt động độc lập. Ví dụ: sc@[-1,2],dc@1[-2,3],sc@[@+2],dc@1[@1+2],tcsẽ gắn mũi thứ hai sctại [-1,4], và mũi thứ hai dctại [-2,5]; tcsẽ gắn vào mũi tiếp theo trên đầu gắn mặc định, tức là vào [-1,5](tương tự như tc@[@+1]). Chúng ta có thể sử dụng bất kỳ phương pháp đánh số nào được mô tả ở trên với bất kỳ đầu gắn nào.

Đính kèm một mũi khâu trống
Có thể đặt lại điểm gắn kết ở bất kỳ vị trí nào trong một hàng bằng cách sử dụng một mũi khâu trống. Ví dụ, sc,dc,@[@-1],trtương đương với sc,dc,tr@[@], cả hai đều buộc các mũi khâu trvà dcgắn vào cùng một điểm. Logic ở đây là điểm gắn kết cuối cùng sau dc, được dịch chuyển trở lại điểm gắn kết của scbằng toán tử @[@-1], do đó mũi khâu tiếp theo trsẽ gắn vào điểm gắn kết của dc.
