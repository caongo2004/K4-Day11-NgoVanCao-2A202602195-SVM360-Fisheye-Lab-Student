# Guideline patch

- **Rule mới đề xuất:** R12 — Khi một object reference có box cao ≥40 px nhưng learner không có box, người soát phải đánh dấu frame/object cụ thể và kiểm ảnh gốc trước khi rework. Nếu reference thấy nhưng model không thấy, chưa được kết luận là annotator error chỉ từ kết quả model; phải ghi `E5_unresolved` và escalation khi chưa đủ bằng chứng.
- **Áp dụng cho:** Box object trong các zone center/mid/edge; đặc biệt object nhỏ, bị che hoặc nằm gần biên fisheye. Không thay thế R01, R03 hoặc R09.
- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:** R01 quy định ngưỡng box nhưng chưa nêu quy trình phân xử khi reference và model bất đồng. Trong slice B4-mid, R4 của `adasind_261480.jpg` là `R_only`, nên cần bước kiểm chứng để tránh sửa nhãn đúng hoặc đổ lỗi cho model từ một ca.
- **`rules_version` mới:** v1.1.0
- **Hiệu lực từ:** Vòng rework sau khi C phân xử findings; đề xuất, chưa sửa trực tiếp `docs/02-rules-vi.md`.
