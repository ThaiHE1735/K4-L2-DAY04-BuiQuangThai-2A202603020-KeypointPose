# Reviewer checklist

Người gán: Bùi Quang Thái  
Người kiểm: Không thực hiện kiểm chéo  
Ngày: 2026-09-16

> Không có reviewer độc lập. Bảng dưới ghi trạng thái self-check có bằng chứng; các mục cần reviewer được ghi N/A thay vì tạo dữ liệu giả.

| | Mục kiểm | Trạng thái | Ghi chú |
| --- | --- | --- | --- |
| 1 | Mọi người trong ảnh đều có đủ 17 điểm, không ai bị thiếu | Self-check | Validator đọc được toàn bộ nhãn; cần evaluator/gold để xác nhận coverage cuối. |
| 2 | Bật đường nối: không có xương nào cắt chéo ở vai hoặc hông | Self-check | Đã chạy `visualize_pose.py`; không có reviewer độc lập. |
| 3 | Không có xương nào kéo dài sang một cơ thể khác | Self-check | Đã chạy visualization; không có reviewer độc lập. |
| 4 | Khớp bị che dùng `v=1` và có chấm, không phải `v=0` | Cần rà soát | Validator phát 7 cảnh báo về `v=0`; đã ghi trong `review_partner.md`. |
| 5 | `v=0` chỉ xuất hiện ở khớp thật sự ra ngoài mép ảnh | Cần rà soát | Có 35 keypoint `v=0`; tập trung ở knee/ankle. |
| 6 | Không có dấu hiệu dùng Hidden | Self-check | Không có bằng chứng sử dụng Hidden trong output validator. |
| 7 | Export đúng COCO Keypoints 1.0: mảng keypoints có 51 số mỗi người | Đạt | Converter chạy thành công và tạo 20 file nhãn. |
| 8 | Bản YOLO Pose: mỗi dòng 56 số, `kpt_shape: [17, 3]` | Đạt định dạng | `check_pose_labels.py` báo ĐẠT định dạng. |
| 9 | Visibility report đã nộp, và hai bảng đã được đặt cạnh nhau | Một phần | Có visibility report của bản thân; không có bản so sánh peer review. |
| 10 | Mọi ca không rõ đều được ghi trong `GUIDELINE_MINI.md` | Đạt | Đã ghi 3 ca mơ hồ và rule xử lý. |
| 11 | `check_pose_labels.py` chạy 0 lỗi | Đạt | Có 7 cảnh báo nhưng không có lỗi chặn nộp. |

## Hai câu kết luận

- Lỗi/cảnh báo lặp lại nhiều nhất: phân biệt keypoint Outside (`v=0`) và Occluded (`v=1`).
- Đây là lỗi/guideline visibility cần rà soát bằng ảnh gốc; không phải lỗi format.
