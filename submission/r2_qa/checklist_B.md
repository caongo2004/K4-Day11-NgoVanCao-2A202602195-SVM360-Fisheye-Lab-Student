# Checklist QA — B · B4-mid

## 1. Thông tin bàn giao

- Người phụ trách B: Lê Sĩ Thành — MSSV 2A202602125 (theo TEAMMATES.md).
- Người gán nhãn A: Nguyễn Đăng Huân — định danh huan.
- Slice chung: B4-mid.
- Mã khóa: 7E4F-2FE7.
- XML: submission/r1_craft/annotations.xml.
- SHA256 bản khóa: 7e4f2fe7137e1a64ba9bc7da24ad2c62175aae462676ce3c7f50efb945dc7e1e.
- Thời điểm nhận: cần xác nhận lại. Ghi chú cũ là 12:03 ngày 29/09/2026, trong khi lock ghi 12:34:13 cùng ngày; chưa dùng mốc cũ làm bằng chứng nhận bản khóa này.
- Thời điểm B chốt QA: chưa xác nhận.

Checklist được trợ lý hỗ trợ kiểm từ ảnh gốc và XML; các dấu tick ghi việc đã được kiểm kỹ thuật, không thay lời xác nhận cá nhân của B. Chưa dùng reference/model của slice chính trong lượt kiểm này. Tick nghĩa là đã kiểm mục đó, không có nghĩa nhãn đã đúng hoặc lỗi đã sửa.

## 2. Chuẩn bị

- [x] Đã đối chiếu luật docs/02-rules-vi.md trong lượt kiểm hỗ trợ.
- [x] Đã nhận XML, lock.txt, slice và mã khóa.
- [x] Đã xác minh XML khớp toàn bộ SHA256 trong lock sau khi khôi phục xuống dòng LF; nội dung nhãn giữ nguyên.
- [x] Đã chạy QA thành công, tạo qa_overlay.html.
- [x] Lượt kiểm hỗ trợ dùng ảnh gốc và nhãn A, không mở reference/model B4-mid.
- [ ] B xác nhận lịch sử QA độc lập của mình và thời điểm chốt.

Lệnh đã dùng:

```powershell
python3 lab11.py qa --slice B4-mid --file "submission/r1_craft/annotations.xml" --code 7E4F-2FE7
```

## 3. Kết quả từng frame

### Frame 1 — adasind_249480.jpg

- [x] Đã đối chiếu hai box L1 Truck và L2 Bike với ảnh gốc.
- [x] Đã xem cách gộp người ngồi trên xe và xe trong L2 theo R03.
- [x] Đã kiểm sự tồn tại của hai lens_border và một ego_body trong XML.
- [ ] Cần phóng to kiểm hình học sát mép bánh của L2; chưa kết luận box sai.
- [ ] Cần xác minh loại xe L1 theo R04 vì phần phía trước bị làm mờ.
- [ ] Cần soát lại ego_body trên CVAT: polygon hiện bao nhiều vùng đáy/vành đen; phần ego nhìn thấy ở mép trái cần xác định phạm vi.
- [ ] Chưa xác nhận đã rà hết vật nền xa, thuộc tính và tỷ lệ box nằm trong ignore.

Kết luận: đã kiểm hai box chính; còn các ca cần xác minh. Không kết luận toàn frame đạt.

Bằng chứng: [ảnh gốc](../../assets/images/adasind_249480.jpg), [overlay](qa_overlay.html), [XML](../r1_craft/annotations.xml).

### Frame 2 — adasind_261480.jpg

- [x] Đã xác định frame chỉ có một rectangle Car nhưng có nhiều polygon đối tượng.
- [x] Đã xác định Bike lớn bên phải (polygon[2]) thiếu box, polygon cao khoảng 713 px: R01.
- [x] Đã xác định ThreeWheeler phía trái (polygon[4]) thiếu box, polygon cao khoảng 127 px: R01.
- [x] Đã xem Bike mép trái và xe màu sáng bên trái: có polygon nhưng chưa có box tương ứng.
- [x] Đã xem Car L1 bị người/xe hai bánh che một phần; occluded=true phù hợp quan sát.
- [x] Đã xác định các shape chưa có group_id, cần hoàn thiện ghép cặp K12.
- [ ] Cần kiểm đầy đủ đường bao ignore, các vật nền xa và hình học/thuộc tính sau khi A bổ sung box.

Kết luận: cần bổ sung rectangle cho các vật thuộc phạm vi; polygon không thay thế box theo R01. A sửa sau khi nhóm phân xử.

Bằng chứng: [ảnh minh chứng 261480](../screenshots/qa_adasind_261480.png). Hai finding cụ thể đã được thêm vào findings.csv.

### Frame 3 — adasind_265065.jpg

- [x] Đã xác định frame không có rectangle nào trong XML.
- [x] Đã đối chiếu polygon xe bên trái và ba người phía cửa hàng bên phải với ảnh gốc.
- [x] Đã xác định các polygon này có chiều cao trên 40 px nhưng chưa có box: R01.
- [x] Đã ghi finding cho người bên phải gần tường (polygon[2]), cao khoảng 138 px.
- [x] Đã xác định các polygon chưa có group_id.
- [ ] Cần kiểm lại class xe, vật nền xa, vùng ignore và thuộc tính sau khi A bổ sung box.

Kết luận: cần thêm box cho xe và từng người theo phần nhìn thấy. Không coi overlay trống là ảnh không có đối tượng.

Bằng chứng: [ảnh minh chứng 265065](../screenshots/qa_adasind_265065.png).

polygon[n] là thứ tự polygon 1-based trong image của XML, tính cả ignore; không phải ID CVAT hay mã box L. Các tham chiếu này không tự chứng minh độ phủ zone.

## 4. Hồ sơ QA đã chuẩn bị

- [x] Đã xem ba ảnh gốc và đối chiếu XML trong lượt kiểm hỗ trợ.
- [x] Có qa_overlay.html và bản nhận xét qa_review.md.
- [x] Có ba finding r2_qa, cell=L_only, rule_id=R01, why để trống; ba dòng mới qua kiểm tra định dạng.
- [x] Có hai PNG minh chứng và liên kết trong review/findings.
- [x] Ảnh minh chứng ghi rõ là ảnh chụp overlay dựng từ XML, không phải screenshot CVAT; không dùng reference/model.
- [ ] B kiểm lại các nhận xét, bổ sung xác nhận tên reviewer trong qa_review.md.
- [ ] B/C ghi mốc bàn giao P3 thật vào TEAMMATES.md.
- [ ] B thông báo QA đã chốt trước khi C mở reference/model.

Chưa chốt thay B. Các ca còn mở ở mục 3 cần được kiểm hoặc ghi rõ phép kiểm tiếp theo khi bàn giao. Ba dòng C0 cũ có owner=Huan không thuộc enum công cụ; đây là vấn đề hồ sơ chung cần nhóm xử lý, không phải lỗi của ba dòng QA mới.

## 5. Kiểm lại sau rework — đang chờ A

Chưa có annotations-v2.xml/lock2.txt trong submission/rework/ tại lần kiểm hồ sơ này.

| Ca cần kiểm lại | Kết quả hiện tại | Việc B kiểm khi có v2 |
|---|---|---|
| 261480: Bike lớn bên phải | Chưa có bản sửa | Có rectangle chung người và xe, bám phần nhìn thấy; kiểm truncated ở biên phải |
| 261480: ThreeWheeler | Chưa có bản sửa | Có rectangle riêng, class và thuộc tính phù hợp ảnh |
| 265065: người bên phải gần tường | Chưa có bản sửa | Có rectangle Pedestrian bám phần nhìn thấy |
| Các vật chỉ có polygon và K12 | Chưa có bản sửa | Soát các box còn thiếu; kiểm bốn cặp K12 đúng đối tượng và cùng group_id |

- [ ] Nhận đúng v2 và lock2 từ A.
- [ ] Kiểm lại từng ca sửa, giữ nguyên nhận xét ban đầu.
- [ ] Ghi kết quả và ca còn mở vào review.
- [ ] Xác nhận đóng góp và kiểm lại thực tế trong TEAMMATES.md.
