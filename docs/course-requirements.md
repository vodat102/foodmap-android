# SE114 – Yêu cầu đồ án (tóm tắt từ tài liệu giảng viên)

## Điểm số
- Đồ án: 70% (chấm vấn đáp). Bài tập: 30%. Thuyết trình: không bắt buộc, điểm cộng.
- Rubric: Giỏi = làm được 90% tính năng đã cam kết; > 9 điểm cần tính năng sáng tạo. Khá = 60%, TB = 50%.

## Ràng buộc chung
- Android native, Java hoặc Kotlin. Cấm React Native / framework đa nền tảng.
- Nhóm 2–3 người; chia việc đều, thể hiện rõ đóng góp từng người.
- Được dùng AI, nhưng mỗi SV phải giải thích được kiến trúc, luồng xử lý và code quan trọng.

## Yêu cầu tối thiểu
1. ≥ 4 màn hình chức năng.
2. ≥ 1 thực thể chính lưu bền vững; người dùng thêm/xem/sửa/xóa; validate input; xử lý danh sách rỗng.
3. ≥ 1 tính năng đặc thù Android (camera, vị trí, thông báo...) phục vụ bài toán, hoặc nghiệp vụ ngoài CRUD.
4. Chạy trên máy thật/emulator; xử lý từ chối quyền, mất mạng (nếu có API), dữ liệu lỗi, thao tác sai.
5. Bàn giao: mã nguồn, hướng dẫn cài đặt/chạy, dữ liệu thử nghiệm, demo luồng chính.

## Hồ sơ nộp
- Đề cương 2–4 trang: `MSSV1_MSSV2_SE114_FoodMap.pdf`.
- Báo cáo 20–50 trang.
- Link GitHub (ưu tiên public) có lịch sử commit.

## FoodMap đáp ứng thế nào
| Yêu cầu | Cách đáp ứng |
|---|---|
| ≥ 4 màn hình | Home, tìm kiếm + lọc, chi tiết quán, chụp check-in, timeline check-in, yêu thích |
| CRUD | CheckIn: tạo / xem timeline / sửa caption, số sao / xóa |
| Tính năng Android | CameraX + Fused Location |
| Nghiệp vụ ngoài CRUD | Tìm kiếm kết hợp bộ lọc; gợi ý quán gần nhất khi check-in |
| Từ chối quyền | Vị trí: chọn quán thủ công. Camera: thông báo + mở Cài đặt |
| Dữ liệu thử nghiệm | `app/src/main/assets/foodmap_seed.json` |
