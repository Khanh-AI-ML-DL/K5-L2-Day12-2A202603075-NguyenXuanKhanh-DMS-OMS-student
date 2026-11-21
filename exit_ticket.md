# Exit ticket — Ngày 12

Làm cá nhân, không mở slide, khoảng 10 phút. Ghi đáp án ngay dưới mỗi câu.

**Họ tên:** Nguyễn Xuân Khánh · **Mã:** G08

---

**Câu 1 · Chọn một.** Camera DMS trên nhiều xe tự chiếu đèn LED cận hồng ngoại khoảng 940 nm lên mặt tài xế. Lý do chính là gì?

- A. Để đo nhiệt độ da và phát hiện tài xế bị sốt
- B. Để có ảnh mặt ổn định cả ngày lẫn đêm mà không làm chói mắt tài xế
- C. Để có ảnh màu đẹp hơn cho cuộc gọi video
- D. Để camera nhìn xuyên qua mọi loại kính râm

Đáp án: **B**

Giải thích: Mắt người gần như không nhìn thấy ánh sáng khoảng 940 nm, nên đèn LED chiếu sáng mặt cả ban đêm mà không gây chói. Camera thu ảnh đơn sắc (chỉ có độ sáng) nên ảnh mặt ổn định hơn so với phụ thuộc vào ánh sáng trong xe. 

**Câu 2 · Số, 2 chữ số thập phân.** Camera DMS chạy 30 khung hình/giây. Model ước lượng yaw của đầu tài xế lớn hơn 30° liên tục từ khung hình số 240 đến khung hình số 314, **tính cả khung 240 và khung 314**. Tài xế không nhìn đường trong bao nhiêu giây?

Đáp án: **2.50 s**

Cách tính: số frame = 314 − 240 + 1 = 75 (tính cả hai đầu). Thời gian = 75 / 30 = 2.50 s. 

**Câu 3 · Chọn tất cả đáp án đúng.** Những câu nào đúng về dữ liệu cabin so với dữ liệu camera ngoài xe?

- A. Không thể làm mờ mặt tài xế như làm mờ mặt người qua đường, vì model DMS cần chính khuôn mặt.
- B. Ban đêm, ảnh cabin thường là ảnh hồng ngoại đen trắng, nên thuộc tính màu áo không gán được.
- C. Camera OMS nhìn về phía sau xe, nên ghế ở bên trái ảnh là ghế bên phải của xe.
- D. Vật trong cabin thường ở xa và nhỏ, nhiều vật trong một ảnh.
- E. Cảnh cabin cố định nên không cần guideline hay QC riêng.

Đáp án: **A, B, C**

Giải thích:
- A đúng: DMS cần mắt, mũi, miệng để ước lượng trạng thái, nên làm mờ mặt tài xế sẽ làm mất chính dữ liệu cần dùng.
- B đúng: ảnh IR chỉ có độ sáng, không có màu 
- C đúng: camera OMS nhìn về phía sau xe nên trái ảnh là phải xe 
- D sai: trong cabin, vật ở gần camera và ít vật hơn. "Xa, nhỏ, nhiều vật" mô tả cảnh ngoài xe.
- E sai: cảnh cố định vẫn có nhiều ca mơ hồ (kính phản xạ, ghế trẻ em bị phủ, dây an toàn trong bóng tối), nên vẫn cần guideline và QC.