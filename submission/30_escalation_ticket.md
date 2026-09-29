# Escalation ticket

## Ticket 1

- **Frame:** `adasind_261480.jpg`, object `R4`, cell `R_only`, slice `B4-mid`
- **Ảnh chụp:** `submission/screenshots/qa_adasind_261480.png`; overlay: `submission/r3_diag/model_compare.html#adasind_261480.jpg`
- **Expected impact:** Có thể là một box ThreeWheeler bị learner bỏ sót, nhưng nếu reference sai thì rework sẽ tạo false positive. Quyết định sai làm thay đổi missing count của vùng center và ảnh hưởng đánh giá QA.
- **Owner:** `qa`
- **Recommendation:** Thanh và Cao mở ảnh gốc, overlay và reference, đo chiều cao visible object theo R01, kiểm R03/R09 nếu có rider/ignore. Nếu H≥40 và in-scope thì giao Huan thêm box; nếu không, giữ với lý do và cập nhật decision log. Không sửa chỉ vì model không dự đoán object.
