# Báo cáo cá nhân — Ngày 2 Object Detection

Đổi tên file theo `MSSV_HoTen.md`, ví dụ `20241234_NguyenVanAn.md`. Điền kết quả thật, xóa dòng hướng dẫn khi nộp. Xem [quy định nộp](../../SUBMISSION.md).

## 1. Thông tin học viên

- Họ tên:LuongDucManh
- MSSV: 2A202603155
- Email: 369ldmanh@gmail.com
- Lớp: K5-L2
- Link repo bài làm:https://github.com/ldmanh610/K5-L2-DAY02-LuongDucManh-2A202603155-ObjectDetection
- Link Colab đã chạy: 

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
- Các tham số thay đổi so với notebook nếu có và lý do:
- Đường dẫn best checkpoint trong phiên chạy:

| Chỉ số trên 10 ảnh eval | Giá trị |
|---|---:|
| Precision | |
| Recall | |
| mAP50 | |
| mAP50–95 | |

Đặt cả 2 folder `assets/eval_predictions/` và `assets/yolo26_runs/` (giải nén từ `day2_colab_outputs.zip`) cạnh báo cáo và dẫn link tương đối. Không chỉ ghi số; chỉ ra ít nhất một ảnh và vật thể cụ thể.

Trả lời bốn câu hỏi cuối notebook:

1. Lớp nào recall thấp nhất? Ảnh nào minh họa?
2. Nếu mAP50 cao nhưng mAP50–95 thấp, cần kiểm điều gì trên box?
3. Lỗi class nào có thể liên quan guideline? Dữ kiện nào hỗ trợ nhận xét?
4. Vì sao không dùng 10 ảnh eval để train? Vai trò validation của chúng trong notebook là gì?

## 6. Khó khăn và cách xử lý

| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
|---|---|---|---|
| | | | |

## 7. Tự đánh giá theo rubric

Đối chiếu [RUBRIC.md](../../RUBRIC.md): phần nào đã có kết quả, phần nào còn thiếu hoặc chưa kiểm được. Không tự nhận hoàn thành bước chưa chạy.

## 8. Công cụ AI và tài liệu tham khảo

Ghi công cụ đã dùng, dùng ở bước nào và phần đã tự kiểm tra; không dùng thì ghi rõ. Liệt kê nguồn ngoài repo được sử dụng. Không ghi mật khẩu/token hoặc đính kèm gold train.
