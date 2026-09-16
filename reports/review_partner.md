# Review partner

## Trạng thái

Không thực hiện kiểm chéo với bạn cùng nhóm do giới hạn thời gian trước hạn nộp.

Không tạo tên reviewer, lỗi reviewer hoặc số liệu so sánh giả.

## Các bước tự kiểm đã thực hiện thay thế

1. Chạy:
   `python tools/check_pose_labels.py --images dataset/images/train --labels dataset/labels/train`
2. Kết quả:
   - Đã đọc 20/20 file nhãn
   - 29 skeleton
   - `v=2 332 | v=1 126 | v=0 35`
   - **ĐẠT định dạng**
3. Chạy:
   `python tools/visualize_pose.py --images dataset/images/train --labels dataset/labels/train --out outputs/vis_train`
4. Đã tạo overlay cho 29 skeleton và kiểm vùng vai/hông, đường nối giữa người và các keypoint bị che.
5. Chạy:
   `python tools/visibility_report.py --labels dataset/labels/train --out outputs/visibility_report.json --markdown reports/visibility_report.md`

## Lỗi tìm được

Không ghi nhận lỗi định dạng từ validator. Validator có 7 cảnh báo về `v=0` cần xem bằng ảnh gốc; đây là cảnh báo, không phải lỗi chặn nộp.

| Ảnh | Người thứ | Khớp | Lỗi gì | Sửa thế nào |
| --- | ---: | --- | --- | --- |
| train_01 | 1 | knee/ankle | Cảnh báo có nhiều `v=0` | Kiểm lại với mép ảnh; nếu khớp ra ngoài frame thì giữ `v=0`, nếu chỉ bị che thì đổi `v=1`. |
| train_01 | 2 | knee/ankle | Cảnh báo có nhiều `v=0` | Kiểm lại theo cùng quy tắc Outside/Occluded. |
| train_04 | 1 | nhiều khớp | Validator cảnh báo 7 khớp `v=0` | So lại ảnh gốc; chỉ giữ `v=0` cho khớp thật sự ngoài frame. |
| train_04 | 2 | nhiều khớp | Validator cảnh báo 4 khớp `v=0` | So lại ảnh gốc; nếu còn trong frame nhưng bị che thì `v=1`. |
| train_10 | 1 | nhiều khớp | Validator cảnh báo 4 khớp `v=0` | Kiểm lại theo mép ảnh. |
| train_11 | 1 | nhiều khớp | Validator cảnh báo 4 khớp `v=0` | Kiểm lại theo mép ảnh. |
| train_13 | 2 | nhiều khớp | Validator cảnh báo 4 khớp `v=0` | Kiểm lại theo mép ảnh. |

## Kết luận

- Lỗi/cảnh báo lặp lại nhiều nhất: phân biệt `Outside (v=0)` với `Occluded (v=1)`.
- Đây chủ yếu là vấn đề quyết định visibility, không phải lỗi cấu trúc file.
