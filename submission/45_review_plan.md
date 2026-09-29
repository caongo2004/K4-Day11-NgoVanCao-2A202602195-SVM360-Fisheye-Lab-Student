# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| `B4-mid` — `adasind_265065.jpg` | 8 MISSING; 6 RM_noL, 1 R_only, 1 còn status theo overlay | Review trước vì frame có 8 reference object và learner ban đầu thiếu toàn bộ; sau rework vẫn còn 5 missing ở vùng mid | `r1_craft/compare.html`, `r3_diag/model_compare.html`, `qa_adasind_265065.png`, `rework/delta.md`, findings R1–R8 và R01 |
| `B4-mid` — `adasind_261480.jpg` | 6 MISSING; có R2/R3/R7+M và R4/R5/R6 | Có cả ca model cùng thấy với reference và ca `R_only`; phù hợp kiểm quy trình rework và escalation | `qa_adasind_261480.png`, `r1_craft/compare.html`, `r3_diag/model_compare.html`, findings R2–R7, rule R01 và R12 đề xuất |

Giới hạn của kết luận từ ba frame ADASIND: đây là một slice một camera, chỉ có ba frame và không có reference object ở edge. Các số không ước lượng tỷ lệ lỗi cho ADASIND nói chung hay cho bốn camera SVM; teaching reference cũng chưa phải gold set đã phê duyệt.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv` (kể cả tránh đếm nhiều frame liền nhau trong cùng cảnh
như nhiều ca độc lập), và vì sao kế hoạch đó chỉ giúp tìm ca cần soi, chưa đo được tỷ lệ lỗi: C kiểm đủ tám ô camera × normal/hard, tổng frames bằng 200, mỗi ô có risk/rationale và phân bố timestamp theo các sự kiện độc lập. Với một chuỗi liên tiếp, chỉ giữ một hoặc vài keyframe đại diện cho cùng sự kiện; ghi event_id để không biến nhiều frame liền nhau thành nhiều ca. Sau đó B kiểm ngẫu nhiên từng ô và xem có đủ lighting, occlusion, seam, calibration và Outside cases hay chưa. Đây là kế hoạch lấy mẫu có chủ đích để tìm lỗi khó, không phải mẫu ngẫu nhiên có trọng số nên không suy ra tỷ lệ lỗi hay tuyên bố gold set.
