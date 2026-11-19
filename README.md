# TechTalent Recruitment Form

> Bài thực hành: Xây dựng Cổng Đăng Ký Tuyển Dụng TechTalent bằng HTML thuần.

## 1. Mục tiêu

Thiết kế lại biểu mẫu tuyển dụng từ Legacy Code, sử dụng đúng các thẻ HTML Form và khả năng kiểm tra dữ liệu mặc định của HTML5. **Giai đoạn 1 không sử dụng CSS hoặc JavaScript.**

## 2. Yêu cầu chức năng

| Thông tin | Phần tử HTML dự kiến | Lưu ý |
| --- | --- | --- |
| Họ và tên | `input type="text"` | Có `label`, `name`, `required` |
| Mật khẩu hệ thống | `input type="password"` | Ẩn ký tự khi nhập |
| Email liên hệ | `input type="email"` | Trình duyệt kiểm tra định dạng |
| Giới tính | `input type="radio"` | Các lựa chọn dùng cùng `name`, chỉ chọn một |
| Ngày sinh | `input type="date"` | Sử dụng bộ chọn ngày |
| Vị trí ứng tuyển | `select` và `option` | Chọn từ danh sách định sẵn |
| CV định dạng PDF | `input type="file"` | Khai báo `accept=".pdf,application/pdf"` |
| Gửi hồ sơ | `button type="submit"` | Kích hoạt kiểm tra hợp lệ trước khi gửi |

## 3. Yêu cầu cấu trúc và thuộc tính

- Dùng `<form>` để chứa toàn bộ trường nhập liệu.
- Chia hai nhóm bằng `<fieldset>` và `<legend>`: **Thông tin cá nhân** và **Thông tin chuyên môn**.
- Dùng `<label for="...">` trỏ tới `id` tương ứng của từng trường; với radio, có nhãn riêng cho từng lựa chọn.
- Mỗi trường gửi dữ liệu phải có `name`; các trường bắt buộc dùng `required`.
- Chọn `method="POST"` thay vì GET vì form có dữ liệu nhạy cảm và tệp CV. Khi gửi tệp thực tế, cần `enctype="multipart/form-data"`.
- `action` phải trỏ tới endpoint xử lý hồ sơ **khi backend được triển khai**; hiện tại chỉ xây dựng và kiểm tra giao diện HTML, không giả định có hệ thống nhận hồ sơ.

**Lưu ý bảo mật:** `POST` không tự mã hóa dữ liệu; khi triển khai thực tế cần HTTPS, kiểm tra dữ liệu phía server, giới hạn/kểm tra loại file và xử lý mật khẩu an toàn. `accept` chỉ hỗ trợ lọc lựa chọn tệp trên giao diện, không đảm bảo file thực sự là PDF.

## 4. Cấu trúc thư mục dự kiến

```text
techtalent-recruitment-form/
├── index.html          # Form HTML5 do học viên triển khai
├── test_report.txt     # Nhật ký kiểm thử validation
├── ai_prompt_log.md    # Các prompt AI đã thực sự sử dụng và mục đích
└── README.md           # Mô tả và checklist bài thực hành
```

## 5. Kế hoạch triển khai

1. **Phân tích (10 phút):** Chỉ ra lỗi của Legacy Code và ánh xạ trường dữ liệu với thẻ phù hợp.
2. **Thiết kế (10 phút):** Phác thảo nhóm `fieldset`/`legend`, chọn `method`, `action` và các thuộc tính.
3. **Lập trình (25 phút):** Tự viết `index.html` với input đúng loại, `label`, `id`, `name`, `required`.
4. **Kiểm thử (10 phút):** Mở trang trong trình duyệt, thử dữ liệu sai và ghi kết quả vào `test_report.txt`.

## 6. Checklist kiểm thử và nghiệm thu

- [ ] Bỏ trống trường bắt buộc và submit: trình duyệt chặn gửi.
- [ ] Nhập email thiếu `@`: trình duyệt báo định dạng không hợp lệ.
- [ ] Mật khẩu hiển thị dạng ký tự được che.
- [ ] Hai radio giới tính không thể cùng được chọn.
- [ ] Có bộ chọn ngày sinh.
- [ ] Vị trí ứng tuyển là dropdown.
- [ ] Trường CV mở hộp thoại chọn file có bộ lọc PDF (cần xác thực file ở server khi triển khai).
- [ ] Bấm nhãn của từng trường để kiểm tra khả năng focus/chọn input.
- [ ] Có đủ `name`, `id`, `required` ở các trường tương ứng.
- [ ] Có hai nhóm `fieldset` kèm `legend` đúng mục đích.
- [ ] Ghi nhận kết quả test thực tế trong `test_report.txt`.
- [ ] Ghi lại prompt đã thực sự hỏi AI vào `ai_prompt_log.md`, không tạo lịch sử giả.

## 7. Câu hỏi vấn đáp cần chuẩn bị

**Vì sao chọn POST thay vì GET?** GET thường đưa dữ liệu biểu mẫu vào URL; POST gửi dữ liệu trong phần thân request, phù hợp hơn với hồ sơ có mật khẩu và file. POST vẫn cần HTTPS.

**`name` khác `id` thế nào?** `id` định danh phần tử để liên kết nhãn và phục vụ các mục đích trên trang; `name` là tên khóa của dữ liệu khi submit. Bỏ `name` thường khiến giá trị trường đó không được gửi cùng form.

**Làm sao giới hạn chọn PDF?** Dùng `accept=".pdf,application/pdf"` cho `input type="file"`; server vẫn cần xác minh loại và nội dung tệp.

## 8. Hồ sơ nộp bài

- `index.html`: Mã nguồn HTML form đã hoàn thiện.
- `test_report.txt`: Kết quả kiểm thử validation trên trình duyệt, có thể kèm đường dẫn ảnh chụp nếu có.
- `ai_prompt_log.md`: Prompt thực tế và mục đích sử dụng AI.

## 9. Quy tắc sử dụng AI

Chỉ dùng AI để tra cứu cú pháp, giải thích thuộc tính, gợi ý loại input và phản biện/test logic. **Không yêu cầu AI viết toàn bộ form và không sao chép mã chưa hiểu.**
