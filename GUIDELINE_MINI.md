# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp

| Lớp | Định nghĩa của bạn | Ví dụ/điểm phân biệt |
| --- | --- | --- |
| `car` | Xe con dùng để chở người như sedan, hatchback, SUV, taxi hoặc pickup cỡ nhỏ. | Kích thước nhỏ hơn bus và truck, thường từ 4–7 chỗ. |
| `truck` | Xe tải chở hàng hoặc xe đầu kéo. | Có thùng hàng hoặc khoang chở hàng riêng biệt. |
| `bus` | Xe buýt hoặc xe khách chở nhiều hành khách. | Thân dài, nhiều cửa sổ, sức chứa lớn. |
| `van` | Xe van hoặc minivan dùng để chở người hoặc hàng hóa. | Kích thước lớn hơn car nhưng nhỏ hơn bus, thân xe dạng hộp. |

## Quy tắc chung

- Box bám sát vật thể nghĩa là: Bounding box ôm sát phần thân xe nhìn thấy được, không lấy thêm mặt đường, bầu trời hoặc xe bên cạnh.
- Vật thể bị che khuất: Vẫn gán nhãn nếu còn đủ thông tin để nhận diện đúng lớp.
- Vật thể bị cắt bởi rìa ảnh: Chỉ box phần nhìn thấy được, không suy đoán phần nằm ngoài ảnh.
- Vật thể rất nhỏ/mơ hồ: Không tự đoán lớp, ghi nhận vào guideline để trao đổi với giảng viên.

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh | Tình huống | Quyết định cuối | Lý do theo schema |
| --- | --- | --- | --- |
| `drive_001.jpg` | Xe truck bị che một phần phía sau xe khác | Gán `truck` | Vẫn nhận diện được loại xe từ phần còn nhìn thấy |
| `drive_016.jpg` | Xe car bị che một phần bởi cây xanh | Gán `car` | Vẫn nhận diện được loại xe từ phần thân xe còn nhìn thấy |
| `drive_037.jpg` | Xe car bị cắt bởi mép ảnh | Vẽ box chạm mép ảnh | Chỉ box phần nhìn thấy được, không suy đoán phần ngoài khung hình |
