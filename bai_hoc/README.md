# Tài liệu học CrochetPARADE - Từ cơ bản đến nâng cao

## Giới thiệu

Đây là bộ tài liệu học tập hoàn chỉnh về **CrochetPARADE** (Crochet Pattern Renderer, Analyzer and Debugger) bằng **tiếng Việt**, được biên soạn dựa trên manual gốc của Svetlin Tassev.

**CrochetPARADE** là ngôn ngữ lập trình chuyên dụng để viết pattern móc len:
- ✅ Chính xác, không mơ hồ
- ✅ Render 2D/3D trước khi móc
- ✅ Tự động phát hiện lỗi
- ✅ Dễ chia sẻ và học

## 📚 Cấu trúc khóa học

Khóa học gồm **10 bài học**, chia thành 3 phần:

### **PHẦN 1: CƠ BẢN** (Bài 1-4)
Thời gian: ~7-8 giờ | 4-5 buổi học

- **[Bài 1: Giới thiệu và Cú pháp Cơ bản](./bai_01_gioi_thieu_va_cu_phap_co_ban.md)** ⭐
  - CrochetPARADE là gì?
  - Mũi móc cơ bản: ch, sc, dc, hdc, tr
  - Nhân mũi và block
  - Pattern đầu tiên

- **[Bài 2: Làm việc với Hàng và Vòng](./bai_02_lam_viec_voi_hang_va_vong.md)** ⭐
  - Lệnh `turn` để lật hàng
  - Skip (`sk`) và slip stitch (`ss`)
  - Móc vòng tròn với `ring`
  - Hiểu "hướng móc"

- **[Bài 3: Tăng, Giảm và Biến thế Mũi](./bai_03_tang_giam_va_bien_the_mui.md)** ⭐⭐
  - Tăng: `sc2inc`, `sc3inc`
  - Giảm: `sc2tog`, `sc3tog`
  - Front/Back loop: `scfl`, `scbl`
  - Front/Back post: `fpdc`, `bpdc`

- **[Bài 4: Attachment Cơ bản](./bai_04_attachment_co_ban.md)** ⭐⭐⭐
  - Attachment tuyệt đối: `@[row,stitch]`
  - Attachment tương đối: `@[@+n]`
  - Current position: `@[%,%-3]`
  - Multiple heads: `@0`, `@1`

### **PHẦN 2: TRUNG BÌNH** (Bài 5-7)
Thời gian: ~6-7 giờ | 4-5 buổi học

- **[Bài 5: Labels Đơn giản](./bai_05_labels_don_gian.md)** ⭐⭐
  - Gắn label: `.A`, `.B`
  - Móc vào label: `@A`
  - Label groups: `5ch.A`, `3sc@A`
  - Indexed labels: `.A[0]`, `.A[1]`

- **[Bài 6: Labels Nâng cao với Counters](./bai_06_labels_nang_cao_counters.md)** ⭐⭐⭐
  - Counters: `$k=0$`, `k++`, `++k`
  - Counter arithmetic: `(k++)%6`
  - INDEX_ARRAY: thứ tự tùy chỉnh

- **[Bài 7: Labeled Groups và Modifiers](./bai_07_labeled_groups_va_modifiers.md)** ⭐⭐⭐⭐
  - Modifier `^`: Gắn vào post
  - Modifier `!`: Bỏ mũi biên
  - Modifier `+`: Thêm mũi biên
  - Modifier `~`: Đảo chiều
  - Multiple sets: `@A[;0]`, `@A[;1]`
  - SORT_LABEL

### **PHẦN 3: NÂNG CAO** (Bài 8-10)
Thời gian: ~6-8 giờ | 4-5 buổi học

- **[Bài 8: Định nghĩa Stitches Mới](./bai_08_dinh_nghia_stitches_moi.md)** ⭐⭐⭐⭐
  - Tạo alias: `DEF: p=3ch,ss`
  - Copy stitch: `Copy(sc,height,width)`
  - Raw stitch grammar (nâng cao)

- **[Bài 9: Tools và Pattern Generators](./bai_09_tools_va_generators.md)** ⭐⭐⭐
  - Expand Instructions
  - Simplify Instructions
  - **Find Project Periphery** ⭐
  - Sphere Generator
  - Axial Shape Generator

- **[Bài 10: Dự án Thực tế](./bai_10_du_an_thuc_te.md)** ⭐⭐⭐⭐⭐
  - Amigurumi hoàn chỉnh
  - Filet crochet
  - Irish crochet
  - Troubleshooting
  - Best practices

## 🎯 Bắt đầu học

### Bước 1: Đọc lộ trình
👉 **[Lộ trình học chi tiết](./00_lo_trinh_hoc.md)**

### Bước 2: Chuẩn bị
- ✅ Truy cập https://crochetparade.org
- ✅ Có laptop/máy tính (không hỗ trợ mobile tốt)
- ✅ Hiểu biết cơ bản về móc len (không bắt buộc)

### Bước 3: Bắt đầu
👉 **[Bài 1: Giới thiệu và Cú pháp Cơ bản](./bai_01_gioi_thieu_va_cu_phap_co_ban.md)**

## 📊 Thời gian học dự kiến

| Trình độ | Thời gian | Số buổi (90 phút/buổi) |
|----------|-----------|------------------------|
| **Cơ bản** (Bài 1-4) | 7-8 giờ | 4-5 buổi |
| **Trung bình** (Bài 5-7) | 6-7 giờ | 4-5 buổi |
| **Nâng cao** (Bài 8-10) | 6-8 giờ | 4-5 buổi |
| **Tổng cộng** | 20-25 giờ | 12-15 buổi |

💡 **Gợi ý:** Mỗi tuần học 2-3 buổi → hoàn thành trong **4-6 tuần**

## 🎓 Đối tượng học viên

Khóa học phù hợp với:

✅ **Người biết móc cơ bản**, muốn viết pattern chính xác  
✅ **Người thiết kế pattern**, cần công cụ verify  
✅ **Người học lập trình**, muốn ứng dụng vào thủ công  
✅ **Giáo viên dạy móc**, cần tài liệu rõ ràng  

❌ **KHÔNG** cần biết lập trình trước  
❌ **KHÔNG** cần biết móc giỏi  

## 📖 Đặc điểm tài liệu

### ✅ Ưu điểm

- **Tiếng Việt dễ hiểu:** Giữ thuật ngữ tiếng Anh chuyên ngành
- **Có hệ thống:** Từ cơ bản đến nâng cao
- **Nhiều ví dụ:** Mỗi khái niệm có 3-5 ví dụ minh họa
- **Bài tập có đáp án:** Tự học hoặc dạy lớp đều được
- **Pattern thực tế:** Áp dụng ngay vào dự án
- **Best practices:** Kinh nghiệm thực tế

### 🎯 So với manual gốc

| | Manual gốc | Tài liệu này |
|---|---|---|
| **Ngôn ngữ** | Tiếng Anh | Tiếng Việt |
| **Cấu trúc** | Tham khảo | Học tuần tự |
| **Ví dụ** | Ít | Nhiều (3-5/khái niệm) |
| **Bài tập** | Không có | Có (cơ bản + nâng cao) |
| **Đáp án** | Không | Có chi tiết |
| **Dự án** | Showcase | Hướng dẫn từng bước |

## 📂 Cấu trúc thư mục

```
bai_hoc/
├── README.md                                    # File này
├── 00_lo_trinh_hoc.md                          # Lộ trình chi tiết
├── bai_01_gioi_thieu_va_cu_phap_co_ban.md     # Bài 1
├── bai_02_lam_viec_voi_hang_va_vong.md        # Bài 2
├── bai_03_tang_giam_va_bien_the_mui.md        # Bài 3
├── bai_04_attachment_co_ban.md                 # Bài 4
├── bai_05_labels_don_gian.md                   # Bài 5
├── bai_06_labels_nang_cao_counters.md          # Bài 6
├── bai_07_labeled_groups_va_modifiers.md       # Bài 7
├── bai_08_dinh_nghia_stitches_moi.md          # Bài 8
├── bai_09_tools_va_generators.md               # Bài 9
└── bai_10_du_an_thuc_te.md                    # Bài 10
```

## ❓ FAQ - Câu hỏi thường gặp

### Q1: Tôi không biết lập trình, có học được không?
**A:** Có! CrochetPARADE được thiết kế cho người móc len, không phải lập trình viên.

### Q2: Tôi không giỏi móc len, có học được không?
**A:** Có! Nhiều người dùng CrochetPARADE để hiểu móc len tốt hơn thông qua mô hình 3D.

### Q3: Mất bao lâu để viết được pattern thực tế?
**A:**
- Sau Bài 4 (1 tuần): Pattern đơn giản
- Sau Bài 7 (3 tuần): Pattern trung bình
- Sau Bài 10 (6 tuần): Pattern chuyên nghiệp

### Q4: Có cần thuộc lòng cú pháp không?
**A:** Không! Dùng tài liệu như cheat sheet. Sau 10-20 pattern bạn sẽ thuộc tự nhiên.

### Q5: Nên học theo thứ tự hay nhảy bài?
**A:**
- Bài 1-4: **Bắt buộc** học tuần tự
- Bài 5-7: Có thể học lướt, quay lại khi cần
- Bài 8-10: Học theo nhu cầu

## 🔗 Tài nguyên liên quan

### Trong thư mục gốc
- `manual.md` - Manual gốc tiếng Anh (764 dòng)
- `Specifying attachment points.md` - Chi tiết về attachment
- `defining_new_stitches.md` - Chi tiết về định nghĩa mũi mới

### Online
- **Website:** https://crochetparade.org
- **Showcase:** Xem examples trên website
- **Forum:** Cộng đồng trên website

## 📝 Lời khuyên cho người học

### ✅ NÊN
- Thử nghiệm ngay trên website khi học
- Render 3D để kiểm tra pattern
- Làm tất cả bài tập và kiểm tra đáp án
- Móc thử một vài pattern để verify
- Tham gia cộng đồng

### ❌ KHÔNG NÊN
- Học vẹt cú pháp mà không thử
- Bỏ qua bài tập
- Nhảy thẳng vào bài khó
- Nản lòng khi gặp lỗi (debugging là cốt lõi!)

## 👨‍🏫 Dành cho giảng viên

### Chuẩn bị
- Máy chiếu để demo live coding
- Mỗi học viên có laptop
- Mẫu móc thực tế để so sánh

### Cấu trúc 1 buổi (90 phút)
- 15p: Lý thuyết + ví dụ
- 40p: Thực hành có hướng dẫn
- 20p: Thực hành độc lập
- 10p: Review + Q&A
- 5p: Giới thiệu bài tiếp

### Đánh giá
- Sau Bài 4: Kiểm tra cơ bản
- Sau Bài 7: Kiểm tra trung bình
- Sau Bài 10: Dự án cuối khóa

## 🏆 Sau khóa học

Sau khi hoàn thành, bạn có thể:

1. **Thực hành:**
   - Viết 10+ patterns khác nhau
   - Móc thật để verify
   - Chia sẻ lên cộng đồng

2. **Nâng cao:**
   - Đọc manual gốc chi tiết hơn
   - Raw stitch grammar nâng cao
   - Đóng góp thư viện stitches

3. **Đóng góp:**
   - Dịch patterns từ tiếng Anh
   - Hướng dẫn người mới
   - Tham gia phát triển CrochetPARADE

## 📜 Giấy phép

**Tài liệu này:** CC BY-NC-SA 4.0 (giống manual gốc)  
**Manual gốc:** Svetlin Tassev, CC BY-NC-SA 4.0  
**CrochetPARADE:** GPLv3 (mã nguồn mở)  

## 🙏 Lời cảm ơn

- **Svetlin Tassev:** Tác giả CrochetPARADE và manual gốc
- **Cộng đồng CrochetPARADE:** Feedback và hỗ trợ

---

## 🚀 Bắt đầu ngay

👉 **[Đọc lộ trình học chi tiết](./00_lo_trinh_hoc.md)**

👉 **[Bài 1: Giới thiệu và Cú pháp Cơ bản](./bai_01_gioi_thieu_va_cu_phap_co_ban.md)**

---

**Cập nhật:** Tháng 2, 2026  
**Liên hệ:** (Thêm thông tin liên hệ nếu cần)

Chúc bạn học tốt! 🧶✨
