<div align="center">

# 🍜 FoodMap

**Ăn gì? Ăn ở đâu?** — Ứng dụng Android giúp bạn khám phá món ăn và chọn quán phù hợp với vị trí, ngân sách và khẩu vị.

![Platform](https://img.shields.io/badge/platform-Android-3DDC84?logo=android&logoColor=white)
![Language](https://img.shields.io/badge/language-Java-ED8B00?logo=openjdk&logoColor=white)
![Min SDK](https://img.shields.io/badge/minSdk-24-blue)
![Database](https://img.shields.io/badge/database-Room-4285F4)
![Status](https://img.shields.io/badge/status-Sprint%200-orange)
[![Android CI](https://github.com/vodat102/foodmap-android/actions/workflows/android-ci.yml/badge.svg)](https://github.com/vodat102/foodmap-android/actions/workflows/android-ci.yml)

Đồ án môn **SE114 – Nhập môn ứng dụng di động** · Trường Đại học Công nghệ Thông tin (UIT)

</div>

---

## 📖 Giới thiệu

Các ứng dụng bản đồ cho bạn rất nhiều dữ liệu về địa điểm, nhưng không giúp bạn **quyết định**. FoodMap đi theo hướng ngược lại:

> **Tìm món ăn phù hợp trước, tìm địa điểm sau.**

Người dùng bắt đầu bằng câu hỏi *"Tôi muốn ăn gì?"*, sau đó ứng dụng hỗ trợ **khám phá → lọc → so sánh → quyết định** dựa trên khoảng cách, giá và rating.

Điểm khác biệt của FoodMap là **Food Check-in**: chụp món ăn ngay tại quán bằng camera trong app, ảnh được tự động gắn **vị trí GPS** và **thời gian thật**, giúp đánh giá trở nên đáng tin cậy.

## ✨ Tính năng

### Giai đoạn 1 — MVP (offline, không cần tài khoản)

| Nhóm | Tính năng |
|---|---|
| 🔍 **Khám phá món ăn** | Tìm kiếm theo tên món, duyệt theo danh mục, xem quán gần vị trí hiện tại |
| 🎛️ **Bộ lọc** | Lọc theo khoảng cách, khoảng giá, rating |
| 🏪 **Chi tiết quán** | Thông tin, hình ảnh, địa chỉ, giờ mở cửa, khoảng giá, rating, thực đơn; nút **Chỉ đường** mở ứng dụng Google Maps |
| ❤️ **Yêu thích** | Lưu và quản lý danh sách quán yêu thích |
| 📸 **Food Check-in** | Chụp món bằng camera trong app, tự gắn GPS + thời gian, gợi ý quán gần nhất, thêm caption và số sao |
| 📔 **Nhật ký ăn uống** | Timeline check-in của bạn; sửa caption / số sao, xóa check-in |

### Màn hình

| # | Màn hình | Mục đích |
|---|---|---|
| 1 | Trang chủ | Danh sách quán gần, danh mục món, ô tìm kiếm, nút Check-in |
| 2 | Tìm kiếm & Lọc | Nhập tên món, chọn bộ lọc, xem danh sách kết quả |
| 3 | Chi tiết quán | Thông tin quán, menu, giờ mở cửa, nút Chỉ đường, nút Yêu thích |
| 4 | Chụp Check-in | Camera trong app; sau khi chụp thì xác nhận quán, nhập caption và số sao |
| 5 | Nhật ký ăn uống | Timeline check-in của bản thân; sửa/xóa từng check-in |
| 6 | Yêu thích | Danh sách quán đã lưu |

Trang chủ, Nhật ký và Yêu thích chuyển qua lại bằng Bottom Navigation.

### Tính năng mở rộng (sau MVP)

- Bản đồ tích hợp trong app (Google Maps SDK).
- Lọc theo danh mục món và trạng thái đang mở cửa.
- Hiển thị check-in trên trang chi tiết quán; đọc và viết review.

### Giai đoạn 2 — Social Check-in (dự kiến)

Đăng nhập (Firebase Auth), kết bạn, feed check-in của bạn bè, thả cảm xúc và bình luận; kèm quản trị & kiểm duyệt nội dung.

> Xem đặc tả đầy đủ tại [`docs/product-spec.md`](docs/product-spec.md).

## 📱 Ảnh chụp màn hình

> _Sẽ cập nhật khi hoàn thành các màn hình chính._

<!--
| Trang chủ | Tìm kiếm & lọc | Chi tiết quán | Check-in | Nhật ký |
|:---:|:---:|:---:|:---:|:---:|
| <img src="docs/screenshots/home.png" width="160"> | <img src="docs/screenshots/search.png" width="160"> | <img src="docs/screenshots/detail.png" width="160"> | <img src="docs/screenshots/checkin.png" width="160"> | <img src="docs/screenshots/diary.png" width="160"> |
-->

## 🛠️ Công nghệ sử dụng

| Thành phần | Lựa chọn |
|---|---|
| Ngôn ngữ | Java |
| Giao diện | XML Layout (View system), Material Components, ViewBinding |
| Kiến trúc | MVVM — ViewModel · Repository · LiveData |
| Lưu trữ | Room (SQLite), dữ liệu mẫu từ JSON seed |
| Camera | CameraX |
| Vị trí | Fused Location Provider |
| Bản đồ | Mở ứng dụng Google Maps qua Intent (Google Maps SDK để ở bản mở rộng) |
| Giai đoạn 2 | Firebase Authentication, Cloud Firestore, dịch vụ lưu ảnh |

## 🏗️ Kiến trúc

```
UI (Activity / Fragment + XML)
  └── ViewModel (mỗi feature một package)
        └── Repository  ──►  Resource<T> (LOADING / SUCCESS / ERROR)
              ├── DAO (Room)
              └── util: LocationHelper → DistanceCalculator
```

```
app/src/main/java/com/example/foodmap/
├── data/
│   ├── local/
│   │   ├── entity/      Restaurant, Food, RestaurantFood, Favorite, CheckIn
│   │   ├── dao/         Mỗi entity một DAO
│   │   └── AppDatabase, SeedLoader
│   └── repository/      RestaurantRepository, FoodRepository, CheckInRepository, ...
├── ui/                  home · search · restaurant · favorite · checkin
└── util/                Resource, LocationHelper, DistanceCalculator
```

Các quyết định kiến trúc được ghi lại trong [`docs/adr/`](docs/adr/).

## 🚀 Cài đặt và chạy

### Yêu cầu

- **Android Studio** bản mới nhất (hỗ trợ Android Gradle Plugin 9.x)
- **JDK 17** trở lên
- Máy ảo hoặc thiết bị thật chạy **Android 7.0 (API 24)** trở lên
- Thiết bị có camera và GPS để dùng Food Check-in

### Các bước

1. Clone repository:

   ```bash
   git clone https://github.com/vodat102/foodmap-android.git
   cd foodmap-android
   ```

2. Mở thư mục bằng Android Studio và đợi Gradle sync xong.

3. Chọn thiết bị và nhấn **Run ▶**, hoặc build bằng dòng lệnh:

   ```bash
   ./gradlew assembleDebug        # Windows: gradlew.bat assembleDebug
   ```

### Dữ liệu thử nghiệm

Dữ liệu quán và món ăn được nạp tự động từ [`app/src/main/assets/foodmap_seed.json`](app/src/main/assets/foodmap_seed.json) vào Room ở lần mở app đầu tiên. Không cần kết nối Internet, tài khoản hay API key. Khi phát triển, app dùng một tọa độ mặc định (khu vực Làng Đại học / Thủ Đức) trước khi ghép GPS thật.

### Kiểm thử

```bash
./gradlew testDebugUnitTest    # Unit test
./gradlew lint                 # Kiểm tra lint
```

## 🗺️ Lộ trình

- [x] Sprint 0 — Chốt phạm vi, đặc tả sản phẩm v0.3, khởi tạo project, hoàn thành đề cương
- [ ] Tuần 1 — Dựng khung app: Room, seed JSON, Bottom Navigation, khung 6 màn hình
- [ ] Tuần 2 — Các màn hình khám phá quán (tọa độ mặc định); tích hợp camera và GPS
- [ ] Tuần 3 — Hoàn thiện Check-in, Nhật ký ăn uống, Yêu thích → MVP chạy được
- [ ] Tuần 4 — Xử lý trường hợp biên (từ chối quyền, dữ liệu lỗi), test chéo, sửa lỗi
- [ ] Tuần 5 — Viết báo cáo, chuẩn bị demo
- [ ] Giai đoạn 2 — Social Check-in với Firebase

Chi tiết từng sprint: [`docs/sprints/`](docs/sprints/).

## 👥 Thành viên

| Thành viên | MSSV | Phụ trách |
|---|---|---|
| Võ Thành Đạt | 24520296 | Food Check-in (CameraX, lưu ảnh, GPS, gợi ý quán gần nhất), Nhật ký ăn uống, xử lý từ chối quyền Camera/GPS; tổng hợp báo cáo |
| Nguyễn Văn Diễn | 24520300 | Bottom Navigation, nạp seed JSON vào Room, Trang chủ, Tìm kiếm & Lọc, Chi tiết quán, Yêu thích; khung XML màn hình 4, 5 |
| Cả hai | | Thiết kế CSDL Room, Repository, DistanceCalculator; review chéo cuối mỗi tuần |

**Giảng viên hướng dẫn:** ThS. Hoàng Văn Hà

## 🤝 Quy trình làm việc

- Nhánh `main` luôn build được; mỗi tính năng làm trên nhánh `feature/<tên-ngắn>` và merge qua Pull Request.
- `main` được bảo vệ: không push thẳng, PR cần **1 approval** của thành viên còn lại và CI (`build`: assembleDebug + unit test) phải xanh; merge bằng **Squash**.
- Hướng dẫn chi tiết từng bước: [`docs/CONTRIBUTING.md`](docs/CONTRIBUTING.md).
- Commit theo định dạng `<type>(<scope>): <summary>`, ví dụ `feat(checkin): capture GPS and time when photo is taken`.
- Không commit thông tin bí mật: `local.properties`, API key, `google-services.json`.

## 📄 Giấy phép

Dự án được thực hiện cho mục đích học tập trong khuôn khổ môn SE114 tại UIT.
