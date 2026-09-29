# Exit ticket

Đọc `docs/10-svm360-reading-vi.md` trước khi trả lời câu 1–2. Các câu về zone, `why`, rework, parking và sampling
đã nằm trong file tương ứng nên không hỏi lại ở đây.

1. Một vật ở vùng seam giữa hai camera thật xuất hiện với hai box khác nhau: đó là lỗi `DUPLICATE` hay cần một quy
   tắc riêng? Vì sao? Không tự động gọi là `DUPLICATE`; cần rule cross-camera riêng. Hai box có thể là hai quan sát hợp lệ của cùng một vật trong vùng overlap. Cần timestamp đồng bộ, calibration/BEV transform và policy output để quyết định giữ, hợp nhất hoặc để tầng sau xử lý. C đề xuất, B kiểm bằng chứng seam, A xác nhận khả năng gán nhãn.
2. Một vật đi qua nhiều frame trên cùng camera: khi nào giữ cùng track ID, khi nào thêm keyframe hoặc trạng thái
   Outside? Nêu bằng chứng sẽ cần trước khi nối track qua hai camera. Giữ cùng track ID khi identity và quan sát liên tục còn đủ chắc chắn; thêm keyframe khi hình học, pose, occlusion hoặc visibility thay đổi đáng kể; dùng Outside khi vật ra khỏi FOV thay vì kéo box tưởng tượng. Trước khi nối qua hai camera cần timestamp đồng bộ, calibration, camera pose, vùng seam/overlap, track evidence hai phía và policy output đích. Không dùng zone center/mid/edge như camera ID.
3. Nhìn lại cả buổi: một chỗ bạn tin nhãn mình đúng nhưng reference hoặc người soát nghĩ khác (dẫn frame/`object_ref`),
   bạn đã xử lý thế nào, và nếu làm lại slice này bạn sẽ đổi gì trong cách làm? Ở `adasind_261480.jpg`, R4 là `R_only`: reference thấy object nhưng learner và model không cùng thấy. C không biểu quyết theo số đông mà ghi `E5_unresolved`, giữ action `rework` và giao QA kiểm ảnh gốc, overlay và ngưỡng R01 trước khi sửa. A chịu trách nhiệm xác nhận nhãn, B kiểm độc lập, C ghi decision log. Nếu làm lại, nhóm sẽ kiểm đủ cả ba frame trước khi lock, đánh dấu object thiếu ngay khi self-QC và lưu ảnh bằng chứng trước khi mở reference.

Đóng góp: A/Huan thực hiện nhãn, self-QC, lock và rework; B/Thanh thực hiện QA độc lập và kiểm lại v2; C/Cao tổng hợp findings, phân xử, kế hoạch bốn camera và chạy các gate.
