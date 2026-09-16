# Báo cáo Ngày 4 - Keypoint & Pose

Họ tên: Bùi Quang Thái  
Nhóm: Chưa cung cấp  
Ngày: 2026-09-16

> Báo cáo này điền toàn bộ phần có bằng chứng hiện tại. Những mục chưa có output gold/model được ghi rõ là **chưa có dữ liệu**, thay vì tự tạo số.

## 1. Nhãn của tôi

| Chỉ số | Giá trị |
| --- | ---: |
| Số ảnh đã gán | 20 |
| Số skeleton | 29 |
| v=2 / v=1 / v=0 | 332 / 126 / 35 |
| Thời gian trung bình mỗi ảnh | Không ghi nhận chính xác |

Ba khớp có `%v=1` cao nhất:

1. `left_ear` — 59%
2. `right_ear` — 52%
3. `left_wrist` và `left_hip` — cùng 31%

Các khớp tai có tỷ lệ `v=1` cao nhất vì tóc, góc quay đầu và vật che làm tâm tai không nhìn rõ dù tai vẫn nằm trong frame. Cổ tay và hông cũng thường bị cơ thể, xe hoặc quần áo che nên cần ước lượng vị trí giải phẫu. Vì vậy các khớp có `%v=1` cao cũng là các khớp tôi phải suy luận nhiều nhất khi gán.

Kết quả self-check cấu trúc:
- 20/20 file nhãn đọc được.
- 29 skeleton.
- `check_pose_labels.py`: **ĐẠT định dạng**.
- Cờ visibility: `v=2 332 | v=1 126 | v=0 35`.
- Validator đưa ra 7 cảnh báo về nhiều `v=0`; đây là cảnh báo cần đối chiếu ảnh gốc chứ không phải lỗi format.

## 2. Chấm với gold

Tại thời điểm hoàn thiện báo cáo này, chưa có output `outputs/eval_vs_gold.json` được cung cấp, vì vậy không tự tạo số liệu OKS.

| Chỉ số | Trước rework | Sau rework |
| --- | ---: | ---: |
| OKS trung bình | Chưa có dữ liệu | Chưa có dữ liệu |
| OKS@0.50 | Chưa có dữ liệu | Chưa có dữ liệu |
| OKS@0.75 | Chưa có dữ liệu | Chưa có dữ liệu |
| Lỗi `dao_trai_phai` | Chưa có dữ liệu | Chưa có dữ liệu |
| Lỗi `nham_nguoi` | Chưa có dữ liệu | Chưa có dữ liệu |
| Lỗi `xoa_khop_bi_che` | Chưa có dữ liệu | Chưa có dữ liệu |

**Tôi đã sửa gì giữa hai lần chạy:**

Chưa có vòng rework dựa trên gold được ghi nhận trong dữ liệu hiện có. Trước khi nhận gold, tôi đã tự kiểm bằng validator, visualization và visibility report; các cảnh báo tập trung vào phân biệt `v=0` và `v=1`.

**Lỗi đảo trái/phải của tôi xảy ra ở ảnh nào?**

Chưa có `eval_vs_gold.json` để khẳng định có hay không lỗi `dao_trai_phai`. Self-check bằng visualization đã tập trung vào vùng vai và hông vì đây là nơi đường nối cắt chéo dễ lộ lỗi trái/phải.

## 3. Kiểm chéo

Không thực hiện kiểm chéo với bạn cùng nhóm do giới hạn thời gian trước hạn nộp. Không tạo reviewer hoặc số liệu so sánh giả.

Khớp có `%v=1` cao nhất trong báo cáo của bản thân là:
- `left_ear`: 59%
- `right_ear`: 52%
- `left_wrist` và `left_hip`: 31%

Không có bảng của bạn cùng nhóm nên không tính được cột lệch giữa hai người.

Luật đã bổ sung vào `GUIDELINE_MINI.md`:
- Nếu khớp còn trong frame nhưng bị tóc, mũ, cơ thể hoặc vật thể che, vẫn đặt điểm ước lượng và dùng `v=1`.
- Chỉ dùng `v=0` khi khớp thật sự ra ngoài mép ảnh.

## 4. Model

Tại thời điểm hoàn thiện báo cáo này, chưa có `outputs/eval_model.json` được cung cấp. Vì vậy không tự tạo metric model.

| Chỉ số | yolo26n-pose gốc | Sau fine-tune | Chênh |
| --- | ---: | ---: | ---: |
| pose_mAP50 | Chưa có dữ liệu | Chưa có dữ liệu | Chưa có dữ liệu |
| pose_mAP50-95 | Chưa có dữ liệu | Chưa có dữ liệu | Chưa có dữ liệu |
| pose_precision | Chưa có dữ liệu | Chưa có dữ liệu | Chưa có dữ liệu |
| pose_recall | Chưa có dữ liệu | Chưa có dữ liệu | Chưa có dữ liệu |
| box_mAP50-95 | Chưa có dữ liệu | Chưa có dữ liệu | Chưa có dữ liệu |

### Trả lời năm câu hỏi ở cuối notebook

1. `pose_mAP50-95` thay đổi bao nhiêu?  
   Chưa có `eval_model.json`, nên chưa thể tính chênh lệch thật.

2. `box_mAP` và `pose_mAP` chênh nhau bao nhiêu?  
   Chưa có metric model để so sánh.

3. Một ảnh test model đoán sai thuộc loại lỗi nào?  
   Chưa có output visualize của notebook để gọi tên lỗi bằng bằng chứng.

4. Ảnh nào có OKS thấp nhất giữa nhãn của tôi và model? Ai đúng?  
   Chưa có output so nhãn với model.

5. Ảnh tôi gán tệ nhất có cũng là ảnh model đoán tệ nhất không?  
   Chưa có dữ liệu model để kết luận.

## 5. Một rule evidence tôi đã dùng

Ở `train_01`, phần thân dưới của người bị cắt bởi mép dưới của ảnh. Với `left_knee`/`right_knee` và các cổ chân đã thực sự nằm ngoài frame, tôi dùng `v=0` thay vì đặt điểm ước lượng. Bằng chứng là phần chân tiếp tục xuống dưới biên ảnh và không còn vùng pixel nào chứa vị trí khớp; đây là Outside thật, không phải occlusion. Trường hợp này khác với cổ tay hoặc hông bị vật thể che nhưng vẫn còn trong khung, khi đó tôi dùng `v=1` và vẫn đặt tọa độ ước lượng.

## 6. Tóm tắt self-check

- Export đã convert thành 20 file YOLO Pose.
- Validator đọc được 20/20 file và báo **ĐẠT định dạng**.
- Đã tạo `outputs/vis_train`.
- Đã tạo `outputs/visibility_report.json`.
- Đã tạo `reports/visibility_report.md`.
- Không thực hiện peer review.
- Chưa có dữ liệu gold/model trong tài liệu được cung cấp tại thời điểm viết báo cáo.
