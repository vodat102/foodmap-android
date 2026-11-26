<div align="center">

# 🍜 FoodMap

**Ăn gì? Ăn ở đâu?** — Ứng dụng Android giúp bạn khám phá món ăn và chọn quán phù hợp với vị trí, ngân sách và khẩu vị.

![Platform](https://img.shields.io/badge/platform-Android-3DDC84?logo=android&logoColor=white)
![Language](https://img.shields.io/badge/language-Java-ED8B00?logo=openjdk&logoColor=white)
![Min SDK](https://img.shields.io/badge/minSdk-24-blue)
![Database](https://img.shields.io/badge/database-Room-4285F4)
![Status](https://img.shields.io/badge/status-Sprint%200-orange)

Đồ án môn **SE114 – Nhập môn ứng dụng di động** · Trường Đại học Công nghệ Thông tin (UIT)

</div>

---

## 📖 Giới thiệu

Các ứng dụng bản đồ cho bạn rất nhiều dữ liệu về địa điểm, nhưng không giúp bạn **quyết định**. FoodMap đi theo hướng ngược lại:

> **Tìm món ăn phù hợp trước, tìm địa điểm sau.**

Người dùng bắt đầu bằng câu hỏi *"Tôi muốn ăn gì?"*, sau đó ứng dụng hỗ trợ **khám phá → lọc → so sánh → quyết định** dựa trên khoảng cách, giá, đánh giá và giờ mở cửa.

Điểm khác biệt của FoodMap là **Food Check-in**: chụp món ăn ngay tại quán bằng camera trong app, ảnh được tự động gắn **vị trí GPS** và **thời gian thật**, giúp đánh giá trở nên đáng tin cậy.

## ✨ Tính năng

### Giai đoạn 1 — MVP (offline, không cần tài khoản)

| Nhóm | Tính năng |
|---|---|
| 🔍 **Khám phá món ăn** | Tìm kiếm theo tên món, duyệt theo danh mục, xem quán gần vị trí hiện tại |
| 🎛️ **Bộ lọc** | Lọc theo khoảng cách, khoảng giá, rating, danh mục, trạng thái đang mở cửa |
| 🏪 **Chi tiết quán** | Thông tin, hình ảnh, giờ mở cửa, thực đơn, đánh giá, vị trí trên bản đồ |
| ❤️ **Yêu thích** | Lưu và quản lý danh sách quán yêu thích |
| 📸 **Food Check-in** | Chụp món bằng camera trong app, tự gắn GPS + thời gian, gợi ý quán gần nhất, thêm caption và số sao |
| 📔 **Nhật ký ăn uống** | Timeline check-in của bạn; sửa caption / số sao, xóa check-in |

### Giai đoạn 2 — Social Check-in (dự kiến)

Đăng nhập (Firebase Auth), kết bạn, feed check-in của bạn bè, thả cảm xúc và bình luận.

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
| Bản đồ | Google Maps SDK (dự phòng: mở app Google Maps qua Intent) |
| Giai đoạn 2 | Firebase Authentication, Cloud Firestore |

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
│   │   ├── entity/      Restaurant, Food, RestaurantFood, Review, Favorite, CheckIn
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

3. _(Tuỳ chọn)_ Cấu hình Google Maps API key trong `local.properties`:

   ```properties
   MAPS_API_KEY=your_api_key_here
   ```

   Nếu không có key, ứng dụng vẫn chạy bình thường và sẽ mở ứng dụng Google Maps khi xem vị trí quán.

4. Chọn thiết bị và nhấn **Run ▶**, hoặc build bằng dòng lệnh:

   ```bash
   ./gradlew assembleDebug        # Windows: gradlew.bat assembleDebug
   ```

### Dữ liệu thử nghiệm

Dữ liệu quán và món ăn được nạp tự động từ [`app/src/main/assets/foodmap_seed.json`](app/src/main/assets/foodmap_seed.json) vào Room ở lần mở app đầu tiên. Không cần kết nối Internet hay tài khoản.

### Kiểm thử

```bash
./gradlew testDebugUnitTest    # Unit test
./gradlew lint                 # Kiểm tra lint
```

## 🗺️ Lộ trình

- [x] Sprint 0 — Chốt phạm vi, đặc tả sản phẩm v0.2, khởi tạo project
- [ ] Sprint 1 — Nền tảng: Room, seed data, navigation, Resource\<T\>
- [ ] Sprint 2 — Khám phá món ăn, bộ lọc, chi tiết quán
- [ ] Sprint 3 — Food Check-in và nhật ký ăn uống
- [ ] Sprint 4 — Yêu thích, bản đồ, xử lý quyền và lỗi, hoàn thiện demo
- [ ] Giai đoạn 2 — Social Check-in với Firebase

Chi tiết từng sprint: [`docs/sprints/`](docs/sprints/).

## 👥 Thành viên

| Thành viên | MSSV | Phụ trách |
|---|---|---|
| Võ Thành Đạt | 24520296 | Food Check-in (CameraX, vị trí, gợi ý quán, nhật ký) |
| Nguyễn Văn Diễn | 24520300 | Khám phá món ăn, bộ lọc, chi tiết quán, yêu thích |

**Giảng viên hướng dẫn:** ThS. Hoàng Văn Hà

## 🤝 Quy trình làm việc

- Nhánh `main` luôn build được; mỗi tính năng làm trên nhánh `feature/<tên-ngắn>` và merge qua Pull Request.
- Commit theo định dạng `<type>(<scope>): <summary>`, ví dụ `feat(checkin): capture GPS and time when photo is taken`.
- Không commit thông tin bí mật: `local.properties`, API key, `google-services.json`.

## 📄 Giấy phép

Dự án được thực hiện cho mục đích học tập trong khuôn khổ môn SE114 tại UIT.
