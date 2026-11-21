# TEAM — Ngày 12

Mã bộ ảnh: **G08** · Hình thức: Team

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|-------------------------------|
| Nguyễn Xuân Khánh | 2A202603075 | có | Võ Khắc Xuân Nguyên | 74                            |

Ca hai bạn vẫn không thống nhất và đã hỏi coach (ghi tên ảnh + đối tượng):

- S01–S08 (cả `_rgb` và `_ir`), tag `frame_meta`, thuộc tính `light`: hai bạn thống nhất ghi `unknown` vì SVIRO là ảnh dựng (Guideline 4.1). Coach đồng ý.
- D03, D04, mắt bị che bởi đốm phản xạ hoặc kính: hai bạn thống nhất ghi `unknown` theo quy tắc "không thấy thì unknown" (Guideline 4.4-1). Coach đồng ý.

Kết quả tự kiểm sau review: `export_final_v2.zip` chạy `cabin_check check --expect 22` báo 0 lỗi, 0 cảnh báo (xem `check_final_v2.txt`). Bản trước review (`export_final.zip`) còn 1 lỗi và 22 cảnh báo, được giữ nguyên để đối chiếu (xem `check_final.txt`).

## Cá nhân
### NguyenXuanKhanh-2A202603075
- Phần mình làm: gán đủ 22 ảnh trên CVAT của mình; review chéo với Võ Khắc Xuân Nguyên bằng `cabin_check diff` (74 điểm khác), điền `disagreement_log.csv`, sửa nhãn của mình và export lại thành `export_final_v2.zip`.
- Điều mình học được hôm nay: đọc lỗi và cảnh báo của `cabin_check`, tự sửa nhãn của mình và chỉ ra chỗ bạn gán khác guideline, thống nhất cách gán với bạn dựa trên guideline, và nhớ rằng hai người trùng nhãn chỉ cho thấy nhất quán, chưa chắc đúng.