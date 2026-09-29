# Đối chiếu chất lượng cục bộ — rectangle

Teaching reference, không phải gold set đã phê duyệt; không có điểm đạt tự động.
Nguồn: export r1_craft đã khóa SHA256 `aef2a93944528abc291fdf6f6d2be71b7ea049f26e56c64cfde33431672c58ab`; slice `B4-mid`.
Ghép hình học greedy một-một theo IoU ≥ 0.50, rồi so class; H ≥ 40 px.
Box trái nằm chủ yếu trong ignore_region reference không tính. Polygon, polyline, track không được chấm.
Đây là phép tính offline của lab, không phải báo cáo hay kết quả tương đương CVAT Premium.

Frame được tính: adasind_249480.jpg, adasind_261480.jpg, adasind_265065.jpg. Frame thiếu trong export: không.
TP=3; FP=0; FN=14; số lần đối chiếu=17; mean IoU của TP=0.939.

| Chỉ số | Micro | Macro | Nhãn thấp nhất |
|---|---:|---:|---:|
| accuracy | 0.176 | 0.835 | 0.706 |
| precision | 1.000 | 0.600 | 0.000 |
| recall | 0.176 | 0.240 | 0.000 |
| jaccard | 0.176 | 0.240 | 0.000 |
| dice | 0.300 | 0.333 | 0.000 |

| Nhãn | TP | FP | FN | Accuracy | Precision | Recall | Jaccard | Dice |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Bike | 1 | 0 | 4 | 0.765 | 1.000 | 0.200 | 0.200 | 0.333 |
| Car | 1 | 0 | 1 | 0.941 | 1.000 | 0.500 | 0.500 | 0.667 |
| Pedestrian | 0 | 0 | 5 | 0.706 | 0.000 | 0.000 | 0.000 | 0.000 |
| ThreeWheeler | 0 | 0 | 3 | 0.824 | 0.000 | 0.000 | 0.000 | 0.000 |
| Truck | 1 | 0 | 1 | 0.941 | 1.000 | 0.500 | 0.500 | 0.667 |

| Frame | TP | FP | FN | Accuracy | Precision | Recall |
|---|---:|---:|---:|---:|---:|---:|
| adasind_249480.jpg | 2 | 0 | 0 | 1.000 | 1.000 | 1.000 |
| adasind_261480.jpg | 1 | 0 | 6 | 0.143 | 1.000 | 0.143 |
| adasind_265065.jpg | 0 | 0 | 8 | 0.000 | 0.000 | 0.000 |

Confusion matrix: hàng = teaching reference; cột = export đã khóa.
`<missing>` là thiếu box; `<extra>` là box thừa. Xem `local_quality_confusion.csv`.

| Reference \ Export | Bike | Car | Pedestrian | ThreeWheeler | Truck | <missing> |
|---|---:|---:|---:|---:|---:|---:|
| Bike | 1 | 0 | 0 | 0 | 0 | 4 |
| Car | 0 | 1 | 0 | 0 | 0 | 1 |
| Pedestrian | 0 | 0 | 0 | 0 | 0 | 5 |
| ThreeWheeler | 0 | 0 | 0 | 0 | 0 | 3 |
| Truck | 0 | 0 | 0 | 0 | 1 | 1 |
| <extra> | 0 | 0 | 0 | 0 | 0 | 0 |

Chi tiết xung đột trong `local_quality_conflicts.csv`; dữ liệu máy đọc trong `local_quality.json`.
Mismatching label đóng góp một FP cho class vẽ và một FN cho class reference; attribute khác được báo riêng.
Micro accuracy đếm mỗi cặp ghép sai class là một lần đối chiếu; Jaccard đếm cả FP và FN.
Macro/worst bỏ nhãn không xuất hiện ở cả hai phía; chỉ số không có mẫu là N/A.
