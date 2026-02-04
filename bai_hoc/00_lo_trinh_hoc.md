# Lộ trình học CrochetPARADE - Từ cơ bản đến nâng cao

## Giới thiệu khóa học

Đây là bộ tài liệu học tập hoàn chỉnh về **CrochetPARADE** - ngôn ngữ lập trình chuyên dụng để viết pattern móc len chính xác, có thể render 2D/3D và debug trước khi móc thật.

### Đối tượng học viên

- **Người biết móc cơ bản**, muốn viết pattern chính xác
- **Người thiết kế pattern**, cần công cụ để verify và chia sẻ
- **Người học lập trình**, muốn ứng dụng vào thủ công
- **Giáo viên dạy móc**, cần tài liệu rõ ràng cho học viên

### Điều kiện tiên quyết

✅ Hiểu biết cơ bản về móc len (chain, single crochet, double crochet)  
✅ Có máy tính và truy cập internet (https://crochetparade.org)  
✅ Kiên nhẫn và sẵn sàng thử nghiệm  

❌ **KHÔNG** cần biết lập trình trước  
❌ **KHÔNG** cần biết móc giỏi  

## Cấu trúc khóa học

### **PHẦN 1: CƠ BẢN** (Bài 1-4)

#### **Bài 1: Giới thiệu và Cú pháp Cơ bản** ⭐
**Thời lượng:** 60 phút  
**Nội dung:**
- CrochetPARADE là gì?
- Các mũi móc cơ bản: ch, sc, dc, hdc, tr
- Nhân mũi và block: `10sc`, `[sc,dc]*3`
- Comment và formatting

**Sau bài này bạn có thể:** Viết pattern vuông/chữ nhật đơn giản

---

#### **Bài 2: Làm việc với Hàng và Vòng** ⭐
**Thời lượng:** 90 phút  
**Nội dung:**
- Lệnh `turn` để lật hàng
- `sk` (skip) và `ss` (slip stitch)
- Móc vòng tròn với `ring`
- Hiểu "hướng móc" (direction of attachment)

**Sau bài này bạn có thể:** Móc khăn có lật hàng, móc vòng tròn cơ bản

---

#### **Bài 3: Tăng, Giảm và Biến thế Mũi** ⭐⭐
**Thời lượng:** 90 phút  
**Nội dung:**
- Tăng mũi: `sc2inc`, `sc3inc`
- Giảm mũi: `sc2tog`, `sc3tog`
- Front/Back loop: `scfl`, `scbl`
- Front/Back post: `fpdc`, `bpdc`

**Sau bài này bạn có thể:** Viết pattern hình cầu, hình trụ, texture đơn giản

---

#### **Bài 4: Attachment Cơ bản** ⭐⭐⭐
**Thời lượng:** 120 phút  
**Nội dung:**
- Attachment tuyệt đối: `@[row,stitch]`
- Attachment tương đối: `@[@+n]`
- Attachment theo loại mũi: `@[sc:row,stitch]`
- Current position: `@[%,%-3]`

**Sau bài này bạn có thể:** Móc vào vị trí bất kỳ, tạo hình phức tạp hơn

---

### **PHẦN 2: TRUNG BÌNH** (Bài 5-7)

#### **Bài 5: Labels Đơn giản** ⭐⭐
**Thời lượng:** 90 phút  
**Nội dung:**
- Label đơn: `.A`, `@A`
- Label nhóm (group): `5ch.A`, `3sc@A`
- Multiple labels: `.A.B`
- Attachment distribution

**Sau bài này bạn có thể:** Đánh dấu và móc vào khoảng chain, tạo motif

---

#### **Bài 6: Labels Nâng cao với Counters** ⭐⭐⭐
**Thời lượng:** 120 phút  
**Nội dung:**
- Indexed labels: `.A[0]`, `.A[1]`
- Counters: `$k=0$`, `k++`, `++k`
- `INDEX_ARRAY`: định nghĩa thứ tự tùy chỉnh
- Counter arithmetic: `A[(k++)%5]`

**Sau bài này bạn có thể:** Viết pattern với labels động, xử lý nhiều nhóm phức tạp

---

#### **Bài 7: Labeled Groups và Modifiers** ⭐⭐⭐⭐
**Thời lượng:** 150 phút  
**Nội dung:**
- Gắn vào thân mũi: `.A^`
- Bỏ mũi biên: `.A!`, `.A!0`, `.A!1`
- Thêm mũi biên: `.A+`, `.A+0`, `.A+1`
- Đảo chiều: `@A~`
- Multiple stitch sets: `@A[;0]`, `@A[;1]`
- Gắn vào mũi cụ thể: `@A[][2]`
- `SORT_LABEL`: sắp xếp labels

**Sau bài này bạn có thể:** Xử lý Irish crochet, lace phức tạp, ráp mảnh

---

### **PHẦN 3: NÂNG CAO** (Bài 8-10)

#### **Bài 8: Định nghĩa Stitches Mới** ⭐⭐⭐⭐
**Thời lượng:** 120 phút  
**Nội dung:**
- Tạo alias: `DEF: p=3ch,ss@[@]`
- Copy stitch: `DEF: rsc=Copy(sc)`
- Thay đổi height/width: `Copy(dc,3,0.9)`
- Raw stitch grammar: `^top:bottom~attachments:other:connections`

**Sau bài này bạn có thể:** Định nghĩa mũi móc tùy chỉnh, mở rộng thư viện stitches

---

#### **Bài 9: Tools và Pattern Generators** ⭐⭐⭐
**Thời lượng:** 90 phút  
**Nội dung:**
- Expand Instructions: bung pattern ra
- Simplify Instructions: nén pattern lại
- Find Project Periphery: tìm biên, gắn label tự động
- Sphere Generator: tạo hình cầu
- Axial Shape Generator: tạo hình trụ, mũ, thân amigurumi
- Object Transform: di chuyển/xoay các mảnh rời

**Sau bài này bạn có thể:** Sử dụng công cụ nâng cao, tự động hóa pattern

---

#### **Bài 10: Dự án Thực tế** ⭐⭐⭐⭐⭐
**Thời lượng:** 180+ phút  
**Nội dung:**
- Amigurumi hoàn chỉnh (đầu, thân, tay, chân, ráp)
- Filet crochet: chart và spaces
- Irish crochet: motifs và nối mảnh
- Lace: picots, shell, V-stitch
- Troubleshooting và debugging

**Sau bài này bạn có thể:** Viết pattern chuyên nghiệp, thiết kế và chia sẻ

---

## Thời gian học dự kiến

| Trình độ | Thời gian | Số buổi (90 phút/buổi) |
|----------|-----------|------------------------|
| **Cơ bản** (Bài 1-4) | 7-8 giờ | 4-5 buổi |
| **Trung bình** (Bài 5-7) | 6-7 giờ | 4-5 buổi |
| **Nâng cao** (Bài 8-10) | 6-8 giờ | 4-5 buổi |
| **Tổng cộng** | 20-25 giờ | 12-15 buổi |

💡 **Gợi ý:** Mỗi tuần học 2-3 buổi → hoàn thành trong **4-6 tuần**

## Cách sử dụng tài liệu này

### Cho học viên tự học

1. **Đọc lý thuyết** ở đầu mỗi bài
2. **Xem ví dụ** và render trên https://crochetparade.org
3. **Làm bài tập** từ cơ bản đến nâng cao
4. **Kiểm tra đáp án** sau khi làm xong
5. **Thử challenge** nếu còn thời gian
6. **Chuyển bài tiếp** khi hiểu ≥80% bài tập

### Cho giảng viên dạy lớp

**Chuẩn bị:**
- Máy chiếu + projector để demo live coding
- Mỗi học viên có laptop/tablet truy cập CrochetPARADE
- Chuẩn bị mẫu móc thực tế để so sánh với render

**Cấu trúc 1 buổi học (90 phút):**
- **15 phút:** Lý thuyết + ví dụ minh họa
- **40 phút:** Thực hành có hướng dẫn (bài tập cơ bản)
- **20 phút:** Thực hành độc lập (bài tập nâng cao)
- **10 phút:** Review và Q&A
- **5 phút:** Giới thiệu bài tiếp

**Đánh giá:**
- Sau **Bài 4:** Kiểm tra cơ bản (viết pattern khăn, vòng tròn)
- Sau **Bài 7:** Kiểm tra trung bình (viết pattern có labels phức tạp)
- Sau **Bài 10:** Dự án cuối khóa (thiết kế pattern từ ý tưởng)

## Tài liệu tham khảo

- **Manual gốc:** `manual.md` (764 dòng, tiếng Anh)
- **Tài liệu nhanh:** `hướng_dẫn_crochet_parade_từ_cơ_bản_dến_nang_cao.md`
- **Website chính thức:** https://crochetparade.org
- **Showcase patterns:** Xem trên website, mục "Examples"

## FAQ - Câu hỏi thường gặp

### Q1: Tôi không biết lập trình, có học được không?
**A:** Có! CrochetPARADE được thiết kế cho **người móc len**, không phải lập trình viên. Nếu bạn biết móc, bạn chỉ cần học cách "viết lại" những gì bạn đã móc.

### Q2: Tôi không giỏi móc len, có học được không?
**A:** Có! Nhiều học viên dùng CrochetPARADE để **hiểu móc len tốt hơn** thông qua mô hình 3D. Bạn có thể học song song.

### Q3: Mất bao lâu để viết được pattern thực tế?
**A:** 
- Sau **Bài 4** (1 tuần): Pattern đơn giản (khăn, túi cơ bản)
- Sau **Bài 7** (3 tuần): Pattern trung bình (mũ, amigurumi đơn giản)
- Sau **Bài 10** (6 tuần): Pattern chuyên nghiệp (amigurumi phức tạp, lace)

### Q4: Có cần thuộc lòng cú pháp không?
**A:** Không! Dùng tài liệu như **cheat sheet**. Sau 10-20 pattern bạn sẽ thuộc tự nhiên.

### Q5: Nên học theo thứ tự hay nhảy bài?
**A:** 
- **Bài 1-4:** Bắt buộc học tuần tự (nền tảng)
- **Bài 5-7:** Có thể học lướt qua, quay lại khi cần
- **Bài 8-10:** Học theo nhu cầu

### Q6: Tôi chỉ muốn viết pattern amigurumi, học bài nào?
**A:** 
- **Bắt buộc:** Bài 1, 2, 3, 4 (nền tảng)
- **Quan trọng:** Bài 5 (labels)
- **Tùy chọn:** Bài 9 (generators - tạo hình cầu tự động)
- **Thực hành:** Bài 10

### Q7: Tôi muốn thiết kế lace, học bài nào?
**A:** 
- **Bắt buộc:** Bài 1, 2, 4 (attachment quan trọng nhất!)
- **Quan trọng:** Bài 5, 6, 7 (labels phức tạp)
- **Thực hành:** Bài 10 (Irish crochet, lace)

## Lời khuyên cho người học

### ✅ NÊN:
- **Thử nghiệm trên website** ngay khi học mỗi khái niệm
- **Render 3D** để xem pattern có đúng không
- **So sánh** pattern CrochetPARADE với pattern truyền thống
- **Móc thử** một vài pattern để verify
- **Tham gia cộng đồng** (Forum trên website)

### ❌ KHÔNG NÊN:
- Học vẹt cú pháp mà không thử
- Bỏ qua bài tập và đáp án
- Nhảy thẳng vào bài khó mà chưa vững nền tảng
- Nản lòng khi gặp lỗi (debugging là cốt lõi của CrochetPARADE!)

## Lộ trình nâng cao (Sau khóa học)

Sau khi hoàn thành 10 bài, bạn có thể:

1. **Đóng góp vào cộng đồng:**
   - Viết pattern và chia sẻ
   - Dịch pattern từ tiếng Anh sang CrochetPARADE
   - Hỗ trợ người mới học

2. **Nghiên cứu sâu:**
   - Đọc manual gốc (tiếng Anh) để hiểu chi tiết
   - Thử nghiệm raw stitch grammar
   - Tạo thư viện stitches riêng

3. **Ứng dụng thực tế:**
   - Viết pattern để bán
   - Dạy móc len kết hợp CrochetPARADE
   - Thiết kế sản phẩm thương mại

---

## Bắt đầu học

👉 **Bắt đầu với [Bài 1: Giới thiệu và Cú pháp Cơ bản](./bai_01_gioi_thieu_va_cu_phap_co_ban.md)**

Chúc bạn học tốt! 🧶✨

---

**Tác giả tài liệu:** Biên soạn từ manual gốc của Svetlin Tassev  
**Giấy phép:** CC BY-NC-SA 4.0 (giống manual gốc)  
**Cập nhật:** Tháng 2, 2026
