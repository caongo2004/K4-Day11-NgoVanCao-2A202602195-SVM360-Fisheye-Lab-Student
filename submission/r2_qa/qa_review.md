# QA review · B4-mid

- Mã khóa: 7E4F-2FE7
- Người gán nhãn: huan.
- Reviewer B: [Điền họ tên sau khi kiểm lại].
- Nhận xét được trợ lý hỗ trợ từ ảnh gốc và XML của A, chưa dùng reference/model. B cần xác nhận trước khi chốt QA.

## Ba nhận xét chính

| Frame | Đối tượng / vị trí | Rule | Nhận xét và đề nghị |
|---|---|---|---|
| adasind_261480.jpg | Các polygon Bike, ThreeWheeler và Car phía trái | R01 | Một số vật cao trên 40 px mới có polygon, chưa có box. A bổ sung rectangle cho từng vật theo phần nhìn thấy; polygon không thay thế box. |
| adasind_265065.jpg | Xe bên trái và ba người bên phải | R01 | Đã có polygon nhưng cả frame chưa có box. A thêm box cho xe và từng người, kiểm lại class theo guideline. |
| Toàn slice B4-mid | Các cặp box–polygon K12 | Yêu cầu K12 tại P2 | XML chưa có group_id. A kiểm đúng bốn đối tượng được gợi ý, bảo đảm mỗi đối tượng có box và polygon cùng class, rồi ghép cùng group. |

## Bằng chứng

- [Ảnh 261480](../../assets/images/adasind_261480.jpg)
- [Ảnh 265065](../../assets/images/adasind_265065.jpg)
- [Overlay QA](qa_overlay.html) và [XML đã khóa](../r1_craft/annotations.xml)

Đây là bản tóm tắt các vấn đề chính, không khẳng định các phần còn lại đều đúng. Đối tượng chưa có box được mô tả bằng vị trí, không tự đặt mã L. B kiểm lại và thêm screenshot trước khi bàn giao C; A sửa trong CVAT sau khi nhóm phân xử, giữ nguyên XML đã khóa.


## Findings và ảnh minh chứng đã bổ sung

Đã thêm ba dòng r2_qa cụ thể vào findings.csv: Bike lớn bên phải (261480, polygon[2]); ThreeWheeler bên trái (261480, polygon[4]); người bên phải gần tường (265065, polygon[2]). Các dòng để trống why. polygon[n] là thứ tự polygon trong image XML, tính cả ignore; đây là tham chiếu mô tả, không phải mã box L và không tự chứng minh độ phủ zone.

- [Minh chứng 261480](../screenshots/qa_adasind_261480.png)
- [Minh chứng 265065](../screenshots/qa_adasind_265065.png)

Ảnh PNG là ảnh chụp trình duyệt của trang overlay dựng từ ảnh gốc và XML đã khóa, không phải ảnh chụp CVAT. Màu cam là polygon đối tượng; màu xanh là box hiện có; ignore được ẩn để dễ nhìn. Trang HTML nguồn được lưu cạnh PNG. Không dùng reference/model.

B cần kiểm lại ba dòng, điền tên reviewer và xác nhận trước khi thông báo QA đã chốt. Chưa có bản sửa nên chưa kiểm rework.
