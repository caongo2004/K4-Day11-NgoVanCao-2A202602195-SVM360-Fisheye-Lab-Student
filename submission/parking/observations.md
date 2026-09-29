# Quan sát vạch ô đỗ

- Hai vạch `parking_line` đã vẽ (mô tả vị trí trong ảnh):
  1. Một vạch chia ô ở khu vực tiền cảnh bên trái ảnh, chạy chéo từ gần mép dưới lên phía giữa ảnh.
  2. Một vạch chia ô ở khu vực giữa–phải ảnh, là đoạn sơn trắng dài tạo ranh giới giữa hai ô đỗ.

- Một vạch/dấu sơn hoặc biên **không** vẽ, và vì sao:
  Không gán các vạch/biên chạy dài theo lối xe hoặc các đoạn sơn ở xa không xác định rõ chức năng chia một ô đỗ riêng, vì theo guideline chỉ các đoạn sơn thực sự tạo ranh giới ô đỗ mới được gán `parking_line`.

- Polygon `free_space` dừng ở đâu; có phần bị che nào không:
  Polygon `free_space` bao phần mặt đường trống nhìn thấy trong khu vực lối xe chạy của bãi đỗ. Polygon dừng tại các ranh giới mặt đường/curb phía xa và tránh vùng có xe màu đỏ cùng các vật cản nhìn thấy. Không kéo polygon xuyên qua xe hoặc vùng bị che.

- Ca chưa chắc cần hỏi người soát (nếu không có, ghi “không có”):
  Không có.