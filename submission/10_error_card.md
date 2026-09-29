# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B4 | MISSING | 4 |
| center | B4 | SPURIOUS | 4 |
| center | C0 | WRONG_CLASS | 1 |
| edge | B4 | SPURIOUS | 1 |
| edge | C0 | IGNORE_SCOPE | 1 |
| edge | C0 | WRONG_CLASS | 1 |
| mid | B4 | MISSING | 24 |
| mid | B4 | SPURIOUS | 7 |
| unknown | B4 | MISSING | 3 |

## Top defects
- MISSING: 31 (ví dụ frame adasind_261480.jpg)
- SPURIOUS: 12 (ví dụ frame adasind_249480.jpg)
- WRONG_CLASS: 2 (ví dụ frame adasind_019560.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

- Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy: lỗi nổi bật là `MISSING`, với 24 ca ở vùng `mid` của block B4 và 4 ca ở `center`. Ở B4-mid, reference và model cùng thấy nhiều object nhưng learner bỏ sót; delta sau rework cho thấy lỗi có thể sửa được vì `mid` giảm missing từ 12 xuống 5. Các ca `M_only` của model được giữ riêng, chưa đủ dữ liệu để kết luận model domain error từ một slice ba frame.
- Cách sửa và ai nhận việc (`owner`): Huan/`annotator` bổ sung các box P1 theo R01/R03, export và lock vòng `rework`; Thanh/`qa` kiểm độc lập XML v2 và ảnh; Cao/`qa` đối chiếu delta và chốt. Ca R4 frame `adasind_261480.jpg` giao `qa` kiểm thêm vì là `R_only` và đang `E5_unresolved`.
- Bằng chứng (ảnh trong `screenshots/`, dòng findings, rule): `submission/screenshots/qa_adasind_261480.png`, `submission/screenshots/qa_adasind_265065.png`, `r1_craft/compare.html`, `r3_diag/model_compare.html`, `submission/rework/delta.md`; áp dụng R01 về H≥40 và R03 về rider + bike là một box Bike.
