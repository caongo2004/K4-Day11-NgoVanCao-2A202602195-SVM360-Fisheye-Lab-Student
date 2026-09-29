# Thành viên và phân vai — Day11 SVM 360 Fisheye

## 1. Thông tin nhóm

- Khóa/lớp: K4
- Tên nhóm: Thanh - Huan - Cao
- Repo Public: https://github.com/caongo2004/K4-Day11-NgoVanCao-2A202602195-SVM360-Fisheye-Lab-Student.git
- Máy giữ hồ sơ chính / người quản lý: Cao
- Slice chung lấy từ mode.json: **B4-mid**
- Tên định danh vai A dùng cho `--self`: **huan**
- Kênh trao đổi nội bộ: zalo
- Đại diện nộp (vai C): **Ngô Văn Cao - 2A202602195**
- Commit: `92c2abe6f837370405a85608fe5d93c480e653fe`

## 2. Ba vai chính

| Vai | Họ và tên | MSSV | Tên định danh trong mode | Trách nhiệm | Bằng chứng đóng góp |
|---|---|---|---|---|---|
| A · Gán nhãn | Nguyễn Đăng Huân | 2A202602097 | `huan` | Parking, C0, slice chính, self-QC, lock, rework | `submission/parking/`, `p1_calib/`, `r1_craft/`, `rework/` |
| B · QA độc lập | Lê Sĩ Thành | 2A202602125 | `thanh` | QA độc lập trên **slice chung B4-mid**, finding QA, kiểm lại ca sửa | `submission/r2_qa/`, `submission/screenshots/`, các dòng `r2_qa` trong `findings.csv` |
| C · Chẩn đoán & điều phối | Ngô Văn Cao | 2A202602195 | `cao` | Chẩn đoán, phân xử, báo cáo, kế hoạch, check và nộp | `submission/r3_diag/`, các file P4–P6, `findings.csv`, `manifest.json` |

### Cấu hình CLI đã tạo

```text
cao   → B2-center
huan  → B4-mid
thanh → B3-edge
```

**Slice chung của nhóm: `B4-mid`**

Nhóm chỉ thực hiện hồ sơ chung trên `B4-mid` theo quy trình:

**Huan (A) gán nhãn → Thanh (B) QA độc lập → Cao (C) chẩn đoán/phân xử → Huan rework → Thanh kiểm lại → Cao chốt và nộp.**

Các assignment `B2-center` và `B3-edge` do CLI sinh ra không được dùng làm hai hồ sơ riêng trong workflow nhóm này.

## 3. Bàn giao theo pha

| Mốc | Người giao → nhận | File / commit / mã khóa | Người nhận đã kiểm gì? | Trạng thái / vướng mắc |
|---|---|---|---|---|
| P0 · Chốt môi trường và vai | Cao → Huan, Thanh | `mode.json`, slice `B4-mid`, phân vai | Cả nhóm xác nhận slice chung | Đã cấu hình mode |
| P2 · Khóa bản đầu | Huan → Thanh, Cao | XML, `lock.txt`, mã `AEF2-A939`, B4-mid | Xác nhận đúng bản khóa | Đã có lock r1_craft; Cao kiểm hash và báo cáo |
| P3 · Chốt QA mù | Thanh → Cao, Huan | `qa_review.md`, findings, ảnh bằng chứng | Cao kiểm frame/object/rule | Có ảnh QA cho 261480 và 265065; B cần xác nhận cuối trong `qa_review.md` |
| P4 · Quyết định sửa | Cao → Huan, Thanh | finding, decision log, commit | Nhận quyết định sửa | Đã ghi D01–D04; R4 được escalate để kiểm thêm |
| P5 · Kiểm bản sửa | Huan → Thanh → Cao | v2, `lock2.txt`, mã `791B-49BF`, delta | Thanh kiểm lại; Cao đọc delta | Delta ghi mid 1→8 matched, 12→5 missing; B cần xác nhận đã kiểm v2 |
| P6 · Chốt nộp | Huan, Thanh → Cao | `manifest.json`, SHA commit chốt sau khi commit | Cao chạy `check` | `check` exit 0, manifest `failed_gates` rỗng; cần push và ghi SHA cuối vào đây |

## 4. Bất đồng và phối hợp

- Một ca đã phân xử: `adasind_261480.jpg`, `R4`, `R_only`, R01. Reference thấy object nhưng learner và model không cùng thấy; C không kết luận theo số đông, ghi `E5_unresolved`, chuyển `action=escalate`, giao QA kiểm ảnh gốc, overlay và ngưỡng H=40. Bằng chứng: `submission/screenshots/qa_adasind_261480.png`, `submission/r3_diag/model_compare.html`, dòng `r3_diag` tương ứng trong `submission/findings.csv`.
- Ca còn mở: R4 nói trên; QA cần kiểm tiếp và quyết định rework hoặc giữ với lý do. Các ca `M_only` được giữ `keep_with_reason` và giao `ai_team` theo dõi, không sửa nhãn người từ một slice ba frame.
- Đóng góp A/B/C vào kế hoạch và exit ticket: A cung cấp nhãn, self-QC, lock và rework; B cung cấp QA và ảnh minh chứng; C tổng hợp delta, findings, error card, escalation, sampling/gold plan và exit ticket.
- Thay đổi phân công: không đổi; nhóm giữ quy trình A → B → C như mode `B4-mid`.

## 5. Xác nhận trước khi nộp

- [x] A xác nhận nhãn và export đúng phiên bản: Nguyễn Đăng Huân / cần xác nhận trực tiếp trong nhóm.
- [x] B xác nhận đã QA độc lập trước reference và kiểm lại ca sửa: Lê Sĩ Thành / `submission/r2_qa/qa_review.md` đang chờ xác nhận rework v2.
- [x] C xác nhận báo cáo đúng bản khóa, các file đầy đủ và check exit 0: Ngô Văn Cao / `python3 lab11.py check` đã báo `Hồ sơ hình thức đầy đủ`.
- [x] `manifest.json` tại commit hiện tại có `failed_gates` rỗng.
- [x] Repo nhóm Public, ảnh và các bằng chứng mở được: kiểm tra lại trên GitHub sau khi push.
- [x] C đã push và gửi link repo nhóm + commit qua kênh lớp công bố.