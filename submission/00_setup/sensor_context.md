# Sensor context

- Rig: Theo quan sát từ nhiều frame, camera fisheye góc rộng có vẻ được gắn trên hoặc rất gần một xe máy và hướng nhìn chủ yếu về phía trước. Không có tài liệu rig chi tiết nên đây chỉ là kết luận từ hình ảnh, không khẳng định chính xác vị trí hoặc thông số lắp đặt.

- `ego_body`: Phần của xe mang camera xuất hiện chủ yếu ở mép trái và góc trái dưới frame. Có thể thấy tay/người lái, tay lái, cụm đồng hồ và một phần thân xe máy trong nhiều ảnh. Các phần này nằm gần cố định ở cùng vùng ảnh qua nhiều frame.

- Vòng kính (lens circle): Biên tròn của ống kính fisheye hiện rõ quanh vùng ảnh hữu dụng. Vòng kính gần như chiếm toàn bộ chiều rộng ảnh và khoảng 80–85% chiều cao khung hình. Phía ngoài vòng kính là vùng tối/đen không thuộc vùng quan sát hữu dụng.