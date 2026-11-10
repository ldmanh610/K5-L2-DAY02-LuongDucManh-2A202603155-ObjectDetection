# Báo cáo cá nhân — Ngày 2 Object Detection

Đổi tên file theo `MSSV_HoTen.md`, ví dụ `20241234_NguyenVanAn.md`. Điền kết quả thật, xóa dòng hướng dẫn khi nộp. Xem [quy định nộp](../../SUBMISSION.md).

## 1. Thông tin học viên

- Họ tên:LuongDucManh
- MSSV: 2A202603155
- Email: 369ldmanh@gmail.com
- Lớp: K5-L2A
- Link repo bài làm:https://github.com/ldmanh610/K5-L2-DAY02-LuongDucManh-2A202603155-ObjectDetection
- Link Colab đã chạy:
- 1 : https://colab.research.google.com/drive/1GmIGBUqGeqjPGSxoWEQmeOlJetc5FFHU#scrollTo=0f04d1c9
- 2 : https://colab.research.google.com/drive/1GmIGBUqGeqjPGSxoWEQmeOlJetc5FFHU?usp=sharing

## 2. Schema và mini guideline

Dẫn tới [GUIDELINE_MINI.md](../../GUIDELINE_MINI.md). Tóm tắt ba ca mơ hồ đã quyết định, cách áp dụng schema và phần cần giảng viên làm rõ.

## 3. Annotation và self-QC

- Số file nhãn train: 50

- Kết quả checker và lỗi đã xử lý:
  - Chạy:
    python tools/check_yolo_labels.py
  - Kết quả:
    ĐẠT cấu trúc: 50/50 file nhãn hợp lệ.

- Danh sách ít nhất 10 ảnh đã rà bằng mắt:
  - drive_001
  - drive_005
  - drive_010
  - drive_016
  - drive_024
  - drive_027
  - drive_028
  - drive_037
  - drive_041
  - drive_050

- Lỗi bỏ sót/box/class phát hiện khi rà và cách sửa:
  - Điều chỉnh box sát vật thể hơn.
  - Bỏ các xe quá nhỏ ở xa.
  - Bổ sung một số xe bị che khuất nhưng vẫn nhận diện được.

- Commit khóa nhãn ban đầu:
  -  e2edf15 Add files via upload

## 4. Gold QC và rework

| Chỉ số | Trước sửa | Sau sửa nếu có |
|---|---:|---:|
| TP | 404 | 399 |
| FP | 317 | 295 |
| FN | 249 | 254 |
| Precision | 0.5603 | 0.5749 |
| Recall | 0.6187 | 0.6110 |
| F1 | 0.5881 | 0.5924 |
| mean_iou_of_matches | 0.8571 | 0.8574 |
| passed | false | false |

Dẫn tới outputs/annotation_evaluation.json.

Đã thực hiện một vòng rework sau khi nhận gold labels.

Các ảnh có sai lệch lớn gồm:
- drive_002
- drive_024
- drive_026
- drive_027
- drive_041
- drive_050

Các điều chỉnh:
- Giảm số lượng box trên xe rất nhỏ ở xa.
- Rà lại xe bị che khuất.
- Điều chỉnh class đối với các trường hợp dễ nhầm giữa car và van.

Kết quả sau rework:
- Precision tăng nhẹ.
- Mean IoU duy trì ở mức cao (>0.85).
- F1 vẫn chưa đạt ngưỡng yêu cầu 0.80.

## 5. Kết quả YOLO

- Runtime, GPU/CPU, phiên bản Ultralytics và Torch:
  - GPU: Tesla T4
  - CUDA: 13.0
  - Ultralytics: 8.4.208
  - Torch: 2.14.1+cu130

- Các tham số thay đổi so với notebook nếu có và lý do:
  - Không thay đổi cấu hình mặc định của notebook.

- Đường dẫn best checkpoint trong phiên chạy:
  - /content/Day2-Lab/outputs/yolo26_runs/vehicle_annotation/weights/best.pt

| Chỉ số trên 10 ảnh eval | Giá trị |
|---|---:|
| Precision | 0.635 |
| Recall | 0.566 |
| mAP50 | 0.642 |
| mAP50–95 | 0.431 |

Đặt cả 2 folder `assets/eval_predictions/` và `assets/yolo26_runs/` (giải nén từ `day2_colab_outputs.zip`) cạnh báo cáo và dẫn link tương đối. Không chỉ ghi số; chỉ ra ít nhất một ảnh và vật thể cụ thể.

Trả lời bốn câu hỏi cuối notebook:

1. Lớp nào recall thấp nhất? Ảnh nào minh họa?
- car    Recall = 0.915
- truck  Recall = 0.600
- bus    Recall = 0.000
- van    Recall = 0.750

3. Nếu mAP50 cao nhưng mAP50–95 thấp, cần kiểm điều gì trên box?
- Nếu mAP50 cao nhưng mAP50-95 thấp thì cần kiểm tra độ chính xác của bounding box.
Mô hình có thể phát hiện đúng đối tượng nhưng box chưa đủ sát vật thể, dẫn đến giảm điểm ở các ngưỡng IoU cao.

5. Lỗi class nào có thể liên quan guideline? Dữ kiện nào hỗ trợ nhận xét?
- Nhóm lỗi dễ liên quan đến guideline là car và van hoặc car và bus.
Các lớp này có hình dạng tương đối giống nhau ở khoảng cách xa hoặc khi bị che khuất.
Việc định nghĩa lớp chưa nhất quán có thể dẫn tới sai nhãn và ảnh hưởng kết quả huấn luyện.
7. Vì sao không dùng 10 ảnh eval để train? Vai trò validation của chúng trong notebook là gì?
- Không sử dụng eval để train nhằm tránh rò rỉ dữ liệu (data leakage).
Trong notebook, eval được dùng làm validation để theo dõi quá trình huấn luyện và chọn best checkpoint.
Nếu đưa eval vào train thì các chỉ số đánh giá sẽ không phản ánh đúng khả năng tổng quát hóa của mô hình.
## 6. Khó khăn và cách xử lý

| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
|---|---|---|---|
| Export CVAT |Chưa biết format phù hợp | Chọn Ultralytics YOLO Detection|Xuất thành công |
| Annotation| Khó phân biệt car/van/bus ở xa| Xem lại schema và guideline| Cải thiện một phần|
| Checker|Chạy sai thư mục |Điều hướng tới thư mục repo | Checker chạy thành công|
| Gold QC| F1 thấp| Rework nhiều ảnh có sai lệch lớn|F1 tăng ít, vẫn chưa đạt |
| Colab| Chưa quen YOLO|Thực hiện theo notebook | Train thành công|
| Evaluation| Recall lớp bus thấp| Phân tích dữ liệu và kết quả eval|Xác định nguyên nhân do dữ liệu ít |
## 7. Tự đánh giá theo rubric

Đối chiếu [RUBRIC.md](../../RUBRIC.md): phần nào đã có kết quả, phần nào còn thiếu hoặc chưa kiểm được. Không tự nhận hoàn thành bước chưa chạy.

## 8. Công cụ AI và tài liệu tham khảo

Ghi công cụ đã dùng, dùng ở bước nào và phần đã tự kiểm tra; không dùng thì ghi rõ. Liệt kê nguồn ngoài repo được sử dụng. Không ghi mật khẩu/token hoặc đính kèm gold train.
