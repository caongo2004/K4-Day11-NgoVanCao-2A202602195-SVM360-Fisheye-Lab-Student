# Thành viên và phân vai — Day11 SVM 360 Fisheye

## 1. Thông tin nhóm

- Khóa/lớp: K4
- Tên nhóm: Thanh - Huan - Cao
- Repo Public: [Điền link GitHub]
- Máy giữ hồ sơ chính / người quản lý: Cao
- Slice chung lấy từ mode.json: **B4-mid**
- Tên định danh vai A dùng cho `--self`: **huan**
- Kênh trao đổi nội bộ: [Điền]
- Đại diện nộp (vai C): **Ngô Văn Cao - 2A202602195**
- Commit chốt bài: [Điền sau]

## 2. Ba vai chính

| Vai | Họ và tên | MSSV | Tên định danh trong mode | Slice assignment | Trách nhiệm |
|---|---|---|---|---|---|
| A · Gán nhãn | Huan | 2A202602097 | `huan` | **B4-mid** | Parking, C0, slice chính, self-QC, lock, rework |
| B · QA độc lập | Thanh | 2A202602125 | `thanh` | B3-edge | QA độc lập trên **slice chung B4-mid**, finding QA, kiểm lại rework |
| C · Chẩn đoán & điều phối | Ngô Văn Cao | 2A202602195 | `cao` | B2-center | Chẩn đoán trên **slice chung B4-mid**, phân xử, báo cáo, check và nộp |

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
| P2 · Khóa bản đầu | Huan → Thanh, Cao | XML, `lock.txt`, B4-mid, commit | Xác nhận đúng bản khóa | [Điền sau] |
| P3 · Chốt QA mù | Thanh → Cao, Huan | `qa_review.md`, findings, ảnh bằng chứng | Cao kiểm frame/object/rule | [Điền sau] |
| P4 · Quyết định sửa | Cao → Huan, Thanh | finding, decision log, commit | Nhận quyết định sửa | [Điền sau] |
| P5 · Kiểm bản sửa | Huan → Thanh → Cao | v2, lock2, review, delta | Thanh kiểm lại; Cao đọc delta | [Điền sau] |
| P6 · Chốt nộp | Huan, Thanh → Cao | manifest, commit chốt | Cao chạy `check` | [Điền sau] |