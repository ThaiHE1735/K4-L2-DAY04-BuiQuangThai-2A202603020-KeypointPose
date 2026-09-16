# Visibility report

- Thư mục nhãn: `dataset\labels\train`
- 20 ảnh, 29 skeleton, trung bình 15.79 khớp có v > 0 mỗi người
- Tổng: v=2 332 | v=1 126 | v=0 35

| # | Khớp | v=2 | v=1 | v=0 | %v=1 |
| ---: | --- | ---: | ---: | ---: | ---: |
| 0 | nose | 23 | 6 | 0 | 21% |
| 1 | left_eye | 22 | 7 | 0 | 24% |
| 2 | right_eye | 22 | 7 | 0 | 24% |
| 3 | left_ear | 12 | 17 | 0 | 59% |
| 4 | right_ear | 14 | 15 | 0 | 52% |
| 5 | left_shoulder | 25 | 4 | 0 | 14% |
| 6 | right_shoulder | 28 | 1 | 0 | 3% |
| 7 | left_elbow | 24 | 5 | 0 | 17% |
| 8 | right_elbow | 25 | 4 | 0 | 14% |
| 9 | left_wrist | 20 | 9 | 0 | 31% |
| 10 | right_wrist | 20 | 8 | 1 | 28% |
| 11 | left_hip | 19 | 9 | 1 | 31% |
| 12 | right_hip | 21 | 7 | 1 | 24% |
| 13 | left_knee | 14 | 8 | 7 | 28% |
| 14 | right_knee | 16 | 6 | 7 | 21% |
| 15 | left_ankle | 13 | 7 | 9 | 24% |
| 16 | right_ankle | 14 | 6 | 9 | 21% |

## Nhận xét

Ba khớp có `%v=1` cao nhất là:
1. `left_ear` — 59%
2. `right_ear` — 52%
3. `left_wrist` và `left_hip` — cùng 31%

Tai có tỷ lệ occluded cao vì tóc, góc quay đầu hoặc vật che làm tâm tai khó nhìn rõ nhưng tai vẫn còn trong frame. Cổ tay và hông thường bị thân người, xe, quần áo hoặc tư thế che nên cần ước lượng giải phẫu. Các giá trị `v=0` tập trung chủ yếu ở knee/ankle, phù hợp với các ảnh người bị crop ở mép ảnh; các trường hợp cảnh báo đã được xem lại bằng overlay.
