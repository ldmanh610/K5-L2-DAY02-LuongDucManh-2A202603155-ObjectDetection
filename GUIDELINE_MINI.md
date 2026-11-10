# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp

| Lớp | Định nghĩa của bạn | Ví dụ/điểm phân biệt |
| --- | --- | --- |
| `car` | Con xe phục vụ người đi bộ giao thông. | Kích thước nhỏ hơn bus và truck, thường 4–7 chỗ, tỷ lệ  mới hơn các xe khác, có mũi nhọn giống các kiểu mũ đi . |
| `truck` | Xe tải chở hàng hoặc xe đầu kéo.| Có khoang hàng hoặc thùng tải riêng biệt, thường giao động vật thể tư cân bằng xe khong bị  |
| `bus` |Xe buýt hoặc xe khách chở nhiều hành khách. |Thân dài, nhiều cửa sổ, sức chứa lớn, tỷ lệ hay có mấy quảng cáo của: nhãn hàng, người nổi tiếng, nghiên cứu đột phá , tiếp thị không âm thanh |
| `van` |Xe van hoặc minivan chở người/hàng | Kích thước lớn hơn car nhưng nhỏ hơn bus, thân hộp kín, tỷ lệ có mũi nhọn như con hải cẩu|

## Quy tắc chung

- Box bám sát vật thể nghĩa là: Bounding box ôm sát phần thân xe nhìn thấy được, không lấy thêm mặt đường, bầu trời hoặc xe bên cạnh.
- Vật thể bị che khuất: Vẫn gán nhãn nếu còn đủ thông tin để nhận diện đúng lớp.
- Vật thể bị cắt bởi rìa ảnh: Chỉ box phần nhìn thấy được, không suy đoán phần nằm ngoài ảnh.
- Vật thể rất nhỏ/mơ hồ: Không tự đoán lớp, ghi nhận vào guideline để trao đổi với giảng viên.

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh | Tình huống | Quyết định cuối | Lý do theo schema |
| --- | --- | --- | --- |
| `drive_001.jpg` | xe `truck` sau xe `car` sau cột | Gán `truck` | Vẫn nhận diện được loại xe từ phần còn nhìn thấy |
| `drive_016.jpg` | xe `car` lấp sau hàng cây cảnh quan đô thị | Gán `car` | Suy đoán phần nằm trong khung hình trước và sau dự đoán chuyển động|
| `drive_037.jpg` | xe `car` vượt khỏi khung hình máy cố định một góc |Vẽ box chạm mép ảnh | Quy tắc không suy đoán phần nằm ngoài khung hình|
