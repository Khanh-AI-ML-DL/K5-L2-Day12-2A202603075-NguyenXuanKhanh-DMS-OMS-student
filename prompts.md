# Khai báo dùng AI — Nguyễn Xuân Khánh

Không đưa ảnh cabin hay ảnh tài xế (kể cả ảnh chụp màn hình) cho bất kỳ công cụ AI nào. Không nhờ AI tự gán nhãn.

| # | Công cụ | Bạn hỏi gì (tóm tắt) | Bạn dùng kết quả thế nào | Bạn có kiểm lại không? Bằng gì? |
|---|---|---|---|---|
| 1 | Claude | Lập danh sách việc, các bước và lệnh từ GUIDE.md; tóm tắt bảng nội dung Guideline Cabin v1.0 | Dùng làm checklist theo thứ tự Task 0 đến 4 | Có, đối chiếu lại với GUIDE.md |
| 2 | Claude | Giải thích ý nghĩa thuộc tính của các label (face, person, hand...) | Đọc để hiểu, gán nhãn theo guideline | Có, đối chiếu với §4.1 và §4.5 của guideline |
| 3 | Claude | Kiểm tra version và cập nhật CVAT bằng Docker; gỡ lỗi Docker | Chạy các lệnh trong terminal của mình | Có, kiểm bằng docker compose ps và trang About của CVAT |
| 4 | Claude | Cách chạy cabin_check, đọc kết quả, chạy bù checkpoint từ export_final.zip | Chạy lệnh, tự sửa nhãn trên CVAT, export v2 | Có, chạy lại cabin_check trên export_final_v2.zip |
