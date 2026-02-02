Hướng nối các mũi khâu tuần tự.
Nếu không chỉ định điểm gắn kết, mã sẽ cố gắng suy ra điểm gắn kết tiếp theo của mũi khâu tiếp theo trong dự án của bạn. Nó thực hiện điều đó bằng cách kiểm tra xem có bao nhiêu turnchỉ thị ở cuối các hàng giữa hàng (gọi là A để dễ tham khảo) của điểm gắn kết của mũi khâu trước đó và hàng hiện tại. Nếu số đó là số chẵn, thì mũi khâu tiếp theo sẽ mặc định gắn vào mũi khâu tiếp theo của A theo hướng móc của A. Nếu số đó là số lẻ, thì mũi khâu tiếp theo sẽ gắn vào mũi khâu trước đó trên A (vì chúng ta đang đi theo thứ tự ngược lại). Điều này sẽ phù hợp với hướng móc tự nhiên khi thực hiện dự án thực tế.


Nếu bạn đang móc vào một nhóm mũi khâu được đánh dấu bằng cách gắn vào nhãn đó, thì hướng móc mặc định được xác định bởi số lượng turnchỉ thị giữa hàng của mũi khâu đầu tiên trong nhóm được đánh dấu và hàng của mũi khâu đó trong tập hợp các mũi khâu được móc vào nhóm được đánh dấu đó, sau khi thực hiện các bước sau: 1. Nếu nhiều tập hợp mũi khâu được gắn vào cùng một nhóm được đánh dấu, hãy sắp xếp chúng theo thứ tự được chỉ định sau ; (ví dụ: các mũi khâu được gắn ,A[0;0]vào trước A[0;1]); và 2. Đảo ngược thứ tự của bất kỳ tập hợp nào có bổ ngữ ~sau nhãn gắn (ví dụ: @A~).
Lưu ý: Một turnchỉ thị bên trong một tập hợp mũi khâu được đóng ngoặc gắn vào một nhóm có nhãn (ví dụ: [7dc,turn 6dc]@A) không chia phần gắn kết thành nhiều tập hợp mũi khâu và do đó không ảnh hưởng đến hướng gắn kết giữa chừng. Hướng gắn kết được chọn một lần cho tập hợp mũi khâu (sau khi sắp xếp theo ;và áp dụng bất kỳ ~đảo chiều nào). Nếu bạn cần các hướng hoặc thứ tự khác nhau trên nhiều đoạn gắn kết, hãy sử dụng các tập hợp mũi khâu với A[]và @A[;i], và sử dụng ~để đảo chiều một tập hợp cụ thể.

Ví dụ, hai khối lệnh sau được phân tích cú pháp giống hệt nhau (phần bên turntrong @Akhối không ảnh hưởng đến hướng gắn kết):

[9ch,turn
sk,8sc].A,ch,turn
sk,8sc,turn
[7dc,turn
6dc]@A
Và

[9ch,turn
sk,8sc].A,ch,turn
sk,8sc,turn
[7dc,
6dc]@A
Để kiểm soát thứ tự/hướng giữa các phân đoạn, hãy sử dụng @A[;0], @A[;1], v.v., và thêm vào ~để đảo ngược một phân đoạn cụ thể.

Một mũi khâu nối tiếp một mũi khâu (hoặc một nhóm mũi khâu) được gắn vào một nhóm mũi khâu đã được đánh dấu, sẽ nối tiếp mũi khâu nối tiếp toàn bộ nhóm đó. Do đó, trong cả hai ví dụ bên dưới, mũi tr sẽ nối tiếp mũi dc, ngay cả khi 4 mũi sc được nối vào A theo thứ tự ngược lại (như được chỉ ra bởi dấu ngã):

6ch,turn
        sk,2ch,dc,2sk,(3ch).A,2sc,turn
        sk,ch,sc,4sc@A,tr
Và

6ch,turn
        sk,2ch,dc,2sk,(3ch).A,2sc,turn
        sk,ch,sc,4sc@A~,tr
Và trong ví dụ bên dưới, cả hai mũi tr đều được gắn vào cùng một mũi dc, vì điểm gắn được di chuyển về mũi cuối cùng của A bởi các ký hiệu @A ngay trước mỗi mũi tr:

6ch,turn
        sk,2ch,dc,2sk,(3ch).A,2sc,turn
        sk,ch,sc,2sc@A,tr,2sc@A,tr,sc
Nếu thực hiện các mũi khâu ở phần thân của một mũi khâu bằng cách sử dụng dấu mũ (ví dụ: .A^), thì hướng móc mặc định là từ điểm gắn của mũi khâu đến đỉnh của mũi khâu, trừ khi có số lượng turnchỉ dẫn lẻ giữa hàng của đỉnh mũi khâu đó và mũi khâu đầu tiên trong tập hợp các mũi khâu được thực hiện ở phần thân (sau khi đã thực hiện việc sắp xếp tương tự như trong đoạn trước).

Lưu ý: Khi gắn vào các mũi khâu, các mũi khâu được đánh số tương ứng với tất cả các nút trên cùng (xem "định nghĩa mũi khâu thô" bên dưới) có trong các mũi khâu đó. Điều đó có nghĩa là một mũi khâu (ví dụ sc2inc: , là 2 mũi đơn trong cùng một mũi khâu) có hai nút trên cùng, thì mỗi nút trên cùng đó sẽ được đánh số tuần tự trong hàng/vòng đang được thực hiện. Các mũi khâu không có nút trên cùng (ví dụ: bên trong là một mũi bỏ qua, sk, được xử lý như một mũi khâu không có nút trên cùng) không được đánh số và do đó không thể gắn mũi khâu vào chúng.
