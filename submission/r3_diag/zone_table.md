# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 4 | 2 | 0 | 1 | 4 | MISSING (2) |
| mid | 13 | 12 | 0 | 3 | 7 | MISSING (12) |
| edge | 0 | 0 | 0 | 0 | 1 | — |

## Nhận xét

- Zone `mid` có nhiều vấn đề nhất: người gán nhãn thiếu `12/13` object reference, còn model thiếu `3` và có `7` dự đoán thừa. Ở `center`, người thiếu `2/4`, model thiếu `1` và có `4` dự đoán thừa. `edge` không có object reference nên chưa đủ mẫu để đánh giá, dù model có `1` dự đoán thừa.
- Giả thuyết chính là object dày và nhỏ trong vùng mid làm tăng nguy cơ bỏ sót; méo fisheye, che khuất và các vật gần nhau có thể làm model sinh box thừa. Kết luận chỉ dựa trên 3 frame của slice `B4-mid`; center/mid/edge là khoảng cách tương đối tới tâm vòng kính, không cho biết vật gần hay xa xe hoặc camera trước/sau. Vùng edge không có mẫu reference, nên cần thêm frame trước khi kết luận về hiệu năng ở edge.
