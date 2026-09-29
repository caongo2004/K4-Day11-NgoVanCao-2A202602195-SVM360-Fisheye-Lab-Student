# Đề xuất gold set theo camera — tình huống giả lập

**Đầu bài:** 50.000 frame từ bốn camera SVM, ngân sách chọn 200 frame để review/gold. Đây là tình huống trên slide,
**không phải** 50.000 frame có trong repo. Phân bổ đúng 200 ở `45_sampling_plan.csv` cho bốn camera, mỗi camera có
normal và hard slice. “Gold set” ở đây là **kế hoạch tạo** reference sau kiểm chứng, không phải teaching reference
ADASIND hoặc nhãn bạn vừa vẽ. Nếu cần, dùng `notebooks/day11-svm360-colab.ipynb` để thử tổng phân bổ; notebook
không làm thay phần lý do.

| camera_id | Hard case cần chọn | Vì sao dễ sai | Annotation space / calibration cần giữ | Cách review trước khi gọi là gold |
|---|---|---|---|---|
| front | Seam góc trước, người đi bộ/xe hai bánh nhỏ, fisheye gần xe | Dễ bị che, méo hình và trùng vùng nhìn với left/right | Giữ timestamp, camera pose, calibration nội tại/ngoại tại, visible extent, truncated/occluded và mapping sang BEV | A gán, B review độc lập; C phân xử. Chỉ gọi gold sau khi kiểm agreement theo ca và giải quyết bất đồng bằng ảnh gốc + calibration |
| rear | Đêm, glare, xe theo sau, reverse và vật ra khỏi FOV | Ánh sáng thấp, phản xạ và Outside dễ làm mất identity hoặc box | Giữ exposure, timestamp, calibration, frame vào/ra, Outside và track evidence | Review độc lập theo event, không đếm burst liên tiếp; refresh khi đổi camera, exposure profile hoặc rule |
| left | Seam trái, xe đỗ/che khuất, vật cắt biên | Chồng lấn với front/rear và partial visibility làm box khác nhau | Giữ overlap geometry, timestamp, pose, calibration và visible polygon/box trên ảnh gốc | B kiểm ca hard, C phân xử seam policy trước khi hợp nhất track |
| right | Seam phải, vulnerable road users và méo fisheye rìa | Góc nhìn và distortion khác front/left; object nhỏ dễ bị bỏ sót | Giữ camera-specific calibration, timestamp, visible extent, keyframe/Outside và BEV transform | A/B review độc lập theo camera; chỉ refresh sau drift calibration hoặc thay đổi taxonomy |

- Khi nào cần refresh gold set (đổi camera, calibration hoặc rule): Refresh khi đổi camera hoặc lens, calibration/BEV transform, firmware/exposure đáng kể, taxonomy/rule, phân bố môi trường, hoặc khi audit phát hiện drift hay bất đồng lặp lại.
- Một ca seam/cross-camera cần policy và evidence trước khi ghép hai box: Giữ cả hai quan sát ban đầu, đối chiếu timestamp đồng bộ, calibration và vùng overlap; người review quyết định một object hợp nhất, hai object hay Outside theo policy output đích. Không nối track chỉ vì hình dáng giống nhau; lưu ảnh hai camera, transform/BEV và lý do quyết định.
- Vì sao peer agreement hoặc quality report trên ảnh một camera chưa chứng minh gold set đúng cho cả bốn camera: Mỗi camera có distortion, exposure, blind spot, seam và phân bố object khác nhau. Agreement trên ADASIND một camera chỉ nói về slice đó; cần review riêng theo camera, normal/hard và calibration trước khi gọi bộ nhãn bốn camera là gold.
