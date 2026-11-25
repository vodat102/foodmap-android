# FoodMap

## Product Specification v0.2

**Project type:** Android Mobile Application  
**Development approach:** Agile / Scrum-inspired  
**Initial platform:** Android  
**Primary language:** Java  
**Document status:** Draft  
**Version:** 0.2  
**Last updated:** 25/11/2026  
**Course:** SE114 – Nhập môn ứng dụng di động (UIT)  
**Team size:** 2 thành viên

### Thay đổi trong v0.2

- Bổ sung tính năng **Food Check-in** (lấy cảm hứng từ Locket) vào MVP: chụp món ăn tại quán bằng camera trong app, tự gắn vị trí và thời gian thật.
- Phát triển theo **2 giai đoạn**: Giai đoạn 1 – MVP offline (Room); Giai đoạn 2 – Social Check-in với bạn bè (Firebase).
- Đăng ký / đăng nhập chuyển sang Giai đoạn 2; MVP không yêu cầu tài khoản.
- Đối chiếu với yêu cầu đồ án môn SE114 (mục 16) và trả lời các Open Questions của v0.1 (mục 17).
- Cập nhật Technical Direction theo các quyết định đã chốt (Java, XML, Room, seed JSON, CameraX).

# 1. Product Vision

FoodMap là ứng dụng Android hỗ trợ người dùng khám phá món ăn và lựa chọn địa điểm ăn uống phù hợp với nhu cầu, vị trí và hoàn cảnh hiện tại.

FoodMap không hướng tới việc thay thế các ứng dụng bản đồ tổng quát. Thay vào đó, sản phẩm tập trung vào một vấn đề cụ thể:

> **“Tôi muốn ăn gì và nên ăn ở đâu?”**

Ứng dụng chuyển bài toán từ “tìm một nhà hàng” thành “tìm một lựa chọn ăn uống phù hợp”.

Bên cạnh việc khám phá, FoodMap cho phép người dùng ghi lại trải nghiệm ăn uống thật của mình qua **Food Check-in**: chụp món ăn ngay tại quán, ảnh được gắn vị trí và thời gian thực tế, giúp đánh giá trở nên chân thật và sống động.

# 2. Problem Statement

Người dùng thường gặp tình huống:

- Muốn ăn nhưng chưa biết ăn món gì.
- Biết món muốn ăn nhưng không biết địa điểm phù hợp.
- Có ngân sách giới hạn.
- Muốn tìm địa điểm gần vị trí hiện tại.
- Khó so sánh nhiều địa điểm dựa trên nhiều tiêu chí cùng lúc.
- Khi ở một khu vực mới, đặc biệt là khách du lịch, khó khám phá những món ăn phù hợp với nhu cầu cá nhân.
- Review trên mạng khó kiểm chứng: không biết người viết có thật sự đến quán hay ăn vào lúc nào.

Các ứng dụng bản đồ hiện tại cung cấp lượng dữ liệu lớn về địa điểm nhưng FoodMap hướng tới việc đơn giản hóa quá trình **khám phá → lọc → so sánh → quyết định**.

# 3. Target Users

## 3.1. Primary Users

### User A — Sinh viên / người trẻ

Đặc điểm:

- Thường xuyên ăn ngoài.
- Có ngân sách giới hạn.
- Quan tâm đến khoảng cách.
- Có nhu cầu khám phá món ăn mới.
- Thường khó quyết định “hôm nay ăn gì”.

### User B — Người khám phá khu vực mới

Đặc điểm:

- Không quen thuộc với khu vực.
- Muốn tìm món ăn đặc trưng hoặc phù hợp sở thích.
- Quan tâm đến đánh giá, khoảng cách và giá.

### User C — Khách du lịch

Đặc điểm:

- Không quen thuộc với địa phương.
- Muốn khám phá món ăn địa phương.
- Cần thông tin dễ hiểu và nhanh chóng.

# 4. Core Value Proposition

FoodMap cung cấp khả năng:

> **Tìm món ăn phù hợp trước, tìm địa điểm sau.**

Thay vì bắt đầu bằng:

> “Nhà hàng nào gần tôi?”

người dùng có thể bắt đầu bằng:

> “Tôi muốn ăn gì?”

Sau đó hệ thống hỗ trợ lọc và lựa chọn địa điểm dựa trên:

- Món ăn
- Khoảng cách
- Giá
- Đánh giá
- Thời gian hoạt động
- Danh mục món ăn
- Nhu cầu / sở thích của người dùng

Ngoài ra, FoodMap bổ sung một giá trị khác biệt:

> **Đánh giá thật — chụp tại quán, có vị trí và thời gian thật.**

# 5. Product Principles

FoodMap được xây dựng theo 5 nguyên tắc:

### 5.1. Food-first

Món ăn là đối tượng trung tâm của trải nghiệm khám phá.

### 5.2. Decision-oriented

Ứng dụng không chỉ cung cấp dữ liệu mà hỗ trợ người dùng đưa ra quyết định.

### 5.3. Explainable

Khi đề xuất một địa điểm, hệ thống nên có khả năng giải thích tại sao địa điểm đó phù hợp.

### 5.4. Trustworthy

Thông tin về địa điểm và đánh giá cần có nguồn gốc rõ ràng và hạn chế dữ liệu không đáng tin cậy. Food Check-in hiện thực nguyên tắc này: ảnh chỉ được chụp bằng camera trong app, vị trí và thời gian được ghi tự động.

### 5.5. Incremental Development

Sản phẩm được phát triển từng bước thông qua các Sprint, không cố hoàn thành toàn bộ hệ thống ngay từ đầu.

# 6. Product Scope

## 6.1. MVP — Minimum Viable Product

Phiên bản MVP dự kiến bao gồm:

### User

- Xem vị trí hiện tại.
- Tìm kiếm món ăn.
- Xem danh sách địa điểm.
- Xem địa điểm trên bản đồ.
- Xem thông tin nhà hàng.
- Xem các món ăn được phục vụ.
- Xem rating / review.
- Lọc kết quả.
- Lưu địa điểm yêu thích.
- Check-in món ăn tại quán bằng camera trong app.
- Xem / sửa / xóa check-in của mình (nhật ký ăn uống).

MVP hoạt động **offline**, không yêu cầu đăng nhập. Dữ liệu quán và món lấy từ seed JSON nội bộ; dữ liệu của người dùng (favorite, check-in) lưu bằng Room trên thiết bị. Đăng ký / đăng nhập chuyển sang Giai đoạn 2 cùng các tính năng xã hội.

### Food Discovery

Người dùng có thể tìm kiếm theo món ăn.

Ví dụ:

> “Bún bò”

Hệ thống trả về các địa điểm có món tương ứng.

### Filtering

Người dùng có thể lọc theo:

- Khoảng cách.
- Khoảng giá.
- Rating.
- Danh mục món ăn.
- Trạng thái đang mở cửa.

### Restaurant Detail

Thông tin dự kiến:

- Tên.
- Hình ảnh.
- Địa chỉ.
- Vị trí.
- Khoảng giá.
- Rating.
- Review.
- Danh sách món.
- Giờ hoạt động.
- Các check-in đã thực hiện tại quán.

### Food Check-in

Tính năng lấy cảm hứng từ Locket: người dùng chụp món ăn ngay tại quán để ghi lại trải nghiệm thật.

- Chỉ chụp bằng camera trong app (CameraX); không cho chọn ảnh từ thư viện.
- Tự động gắn vị trí (GPS) và thời gian tại thời điểm chụp; người dùng không chỉnh sửa được hai thông tin này.
- Gợi ý quán gần nhất dựa trên vị trí chụp (dùng DistanceCalculator); người dùng xác nhận hoặc chọn quán khác. Nếu không có quán phù hợp, check-in vẫn được lưu mà không gắn quán.
- Nhập caption và số sao (1–5).
- Timeline “Nhật ký ăn uống”: danh sách check-in của bản thân, mới nhất lên đầu; có trạng thái danh sách rỗng.
- Sửa caption / số sao; xóa check-in (có hộp thoại xác nhận).
- Trang chi tiết quán hiển thị các check-in tại quán đó.

Dữ liệu check-in (Room entity, dự kiến):

    CheckIn
      id
      photoPath
      latitude, longitude   (tự động, không sửa được)
      capturedAt            (tự động, không sửa được)
      restaurantId          (có thể null)
      caption
      rating                (1–5)
      createdAt, updatedAt

**Giới hạn đã biết:** chặn ảnh thư viện và ghi GPS/thời gian lúc chụp đủ đảm bảo độ tin cậy ở phạm vi đồ án, nhưng không chống được việc người dùng giả lập GPS (mock location).

## 6.2. Phân giai đoạn phát triển

- **Giai đoạn 1 – MVP (offline, Room):** Food Discovery, Filtering, Restaurant Detail, Favorite và Food Check-in cá nhân.
- **Giai đoạn 2 – Social Check-in (Firebase):** đăng nhập, kết bạn, feed check-in của bạn bè, thả cảm xúc, bình luận (xem 7.7). Chỉ triển khai khi MVP đã hoàn thành và ổn định.

# 7. Future Features

Các chức năng sau chưa thuộc MVP nhưng có thể phát triển trong các Sprint tiếp theo:

## 7.1. Personalized Recommendation

Hệ thống đề xuất món ăn / địa điểm dựa trên:

- Lịch sử tìm kiếm.
- Favorite.
- Rating.
- Sở thích.
- Ngân sách.
- Khoảng cách.

## 7.2. “What Should I Eat?”

Người dùng cung cấp:

- Ngân sách.
- Khoảng cách.
- Khẩu vị.
- Loại món.
- Thời gian.

Hệ thống đưa ra một số lựa chọn.

## 7.3. Explainable Recommendation

Ví dụ:

> “Địa điểm này được đề xuất vì cách bạn 700m, nằm trong ngân sách 50.000đ và có rating 4.6/5 cho món bạn đang tìm.”

## 7.4. User Reviews

Người dùng có thể:

- Đánh giá.
- Viết review.
- Đăng hình ảnh.
- Chỉnh sửa / xóa review của mình.

**Ghi chú:** trong MVP, nhu cầu đánh giá được đáp ứng một phần qua Food Check-in (có số sao và cảm nhận). Review dạng văn bản đầy đủ phát triển sau.

## 7.5. Restaurant / Admin Management

Admin có thể:

- Thêm nhà hàng.
- Chỉnh sửa thông tin.
- Quản lý món ăn.
- Kiểm duyệt review.
- Quản lý dữ liệu.

## 7.6. Analytics

Theo dõi:

- Món ăn được tìm kiếm nhiều.
- Địa điểm được xem nhiều.
- Món ăn phổ biến theo khu vực.
- Xu hướng tìm kiếm.

## 7.7. Social Check-in (Giai đoạn 2)

Mở rộng Food Check-in thành mạng xã hội nhỏ giữa bạn bè, theo mô hình Locket:

- Đăng ký / đăng nhập (Firebase Authentication).
- Kết bạn: gửi, chấp nhận, từ chối lời mời.
- Feed check-in của bạn bè.
- Thả cảm xúc vào check-in.
- Bình luận.
- Chỉ bạn bè mới xem được check-in (Firestore Security Rules).

**Lưu ý kỹ thuật:**

- Cloud Storage for Firebase yêu cầu gói Blaze (pay-as-you-go; vẫn có mức sử dụng miễn phí nhưng phải liên kết tài khoản thanh toán).
- Phương án thay thế để lưu ảnh: Cloudinary hoặc Supabase Storage.
- Cần phương án demo khả thi: tài khoản demo và dữ liệu mẫu.

# 8. Core User Flow

## Flow 1 — Search Food

    Open App
       ↓
    Search Food
       ↓
    Enter "Bún bò"
       ↓
    System returns matching restaurants
       ↓
    Apply filters
       ↓
    View results
       ↓
    Select restaurant
       ↓
    Restaurant Detail
       ↓
    Choose / Navigate

## Flow 2 — Discover Nearby Food

    Open App
       ↓
    Get current location
       ↓
    Select food category
       ↓
    Find nearby restaurants
       ↓
    Filter
       ↓
    Compare
       ↓
    Restaurant Detail

## Flow 3 — Personalized Discovery

    Open App
       ↓
    "What should I eat?"
       ↓
    Select preferences
       ↓
    System processes preferences
       ↓
    Generate recommendations
       ↓
    Explain recommendation
       ↓
    Restaurant Detail

## Flow 4 — Food Check-in

    Open App
       ↓
    Tap "Check-in"
       ↓
    Grant camera & location permission
       ↓
    Take photo (in-app camera)
       ↓
    System records GPS + time
       ↓
    Suggest nearest restaurant
       ↓
    Confirm restaurant, add caption & rating
       ↓
    Save (Room)
       ↓
    View in Food Diary timeline

# 9. Initial User Stories

## Epic 1 — Account

**Ghi chú v0.2:** Epic này chuyển sang Giai đoạn 2, cần thiết khi có tính năng xã hội.

### US-001

As a user, I want to register an account so that I can use personalized features.

### US-002

As a user, I want to log in so that I can access my account.

### US-003

As a user, I want to log out so that my account remains secure.

# Epic 2 — Food Discovery

### US-004

As a user, I want to search for a dish so that I can find places serving it.

### US-005

As a user, I want to browse food categories so that I can discover food more easily.

### US-006

As a user, I want to see nearby restaurants so that I can find convenient places to eat.

# Epic 3 — Restaurant

### US-007

As a user, I want to view restaurant details so that I can decide whether to visit.

### US-008

As a user, I want to see restaurant location on a map so that I know where it is.

### US-009

As a user, I want to see the restaurant’s food menu so that I know what it serves.

# Epic 4 — Filtering

### US-010

As a user, I want to filter restaurants by distance so that I can find nearby places.

### US-011

As a user, I want to filter by price so that I can find restaurants within my budget.

### US-012

As a user, I want to filter by rating so that I can narrow down the results.

# Epic 5 — Review

### US-013

As a user, I want to read reviews so that I can understand other users’ experiences.

### US-014

As a user, I want to rate a restaurant so that I can share my experience.

### US-015

As a user, I want to write a review so that I can help other users make decisions.

# Epic 6 — Favorite

### US-016

As a user, I want to save a restaurant so that I can find it again later.

### US-017

As a user, I want to view my favorite restaurants so that I can manage places I am interested in.

# Epic 7 — Food Check-in

### US-023

As a user, I want to check in at a restaurant by taking a photo with the in-app camera so that my experience is recorded authentically.

### US-024

As a user, I want my check-in to automatically record my location and time so that it can be trusted as real.

### US-025

As a user, I want the app to suggest the nearest restaurant when I check in so that I can tag the place quickly.

### US-026

As a user, I want to view my check-in timeline (food diary) so that I can look back on what and where I ate.

### US-027

As a user, I want to edit the caption and rating of my check-in so that I can fix mistakes.

### US-028

As a user, I want to delete my check-in so that I can remove entries I no longer want.

### US-029

As a user, I want to see check-ins on a restaurant’s detail page so that I can see real dishes and experiences there.

# Epic 8 — Social Check-in (Giai đoạn 2)

### US-030

As a user, I want to add friends so that we can share check-ins with each other.

### US-031

As a user, I want to see my friends’ check-ins in a feed so that I can discover places they enjoyed.

### US-032

As a user, I want to react to a friend’s check-in so that I can respond quickly.

### US-033

As a user, I want to comment on a friend’s check-in so that we can talk about the food.

# 10. Product Backlog — v0.2

| ID     | Feature                        | Priority | MVP            |
|--------|--------------------------------|----------|----------------|
| US-001 | Register                       | High     | Phase 2        |
| US-002 | Login                          | High     | Phase 2        |
| US-003 | Logout                         | Medium   | Phase 2        |
| US-004 | Search food                    | Critical | Yes            |
| US-005 | Food categories                | High     | Yes            |
| US-006 | Nearby restaurants             | Critical | Yes            |
| US-007 | Restaurant detail              | Critical | Yes            |
| US-008 | Map                            | Critical | Yes            |
| US-009 | Menu                           | High     | Yes            |
| US-010 | Distance filter                | High     | Yes            |
| US-011 | Price filter                   | High     | Yes            |
| US-012 | Rating filter                  | Medium   | Yes            |
| US-013 | View reviews                   | High     | Yes            |
| US-014 | Rating                         | Medium   | Yes (Check-in) |
| US-015 | Write review                   | Medium   | Later          |
| US-016 | Favorite                       | High     | Yes            |
| US-017 | Favorite management            | Medium   | Yes            |
| US-018 | Personalized recommendation    | High     | Later          |
| US-019 | “What should I eat?”           | High     | Later          |
| US-020 | Explainable recommendation     | High     | Later          |
| US-021 | Admin management               | Medium   | Later          |
| US-022 | Analytics                      | Low      | Later          |
| US-023 | Check-in with in-app camera    | Critical | Yes            |
| US-024 | Auto GPS + time on check-in    | Critical | Yes            |
| US-025 | Suggest nearest restaurant     | High     | Yes            |
| US-026 | Check-in timeline (food diary) | Critical | Yes            |
| US-027 | Edit check-in                  | High     | Yes            |
| US-028 | Delete check-in                | High     | Yes            |
| US-029 | Check-ins on restaurant detail | Medium   | Yes            |
| US-030 | Add friends                    | Medium   | Phase 2        |
| US-031 | Friends’ check-in feed         | Medium   | Phase 2        |
| US-032 | React to check-in              | Low      | Phase 2        |
| US-033 | Comment on check-in            | Low      | Phase 2        |

# 11. Non-Functional Requirements — Initial Draft

## NFR-001 — Usability

Các chức năng chính phải có navigation rõ ràng và người dùng mới có thể hiểu cách sử dụng mà không cần hướng dẫn dài.

## NFR-002 — Performance

Các thao tác tìm kiếm và hiển thị dữ liệu cần phản hồi trong thời gian hợp lý trong điều kiện mạng bình thường.

## NFR-003 — Reliability

Ứng dụng cần xử lý các trường hợp:

- Không có Internet.
- Không có dữ liệu.
- Location bị từ chối.
- API lỗi.
- Dữ liệu không hợp lệ.
- Camera bị từ chối (hiển thị hướng dẫn và nút mở Cài đặt).
- Không xác định được vị trí khi check-in (vẫn cho lưu, không gắn quán).

## NFR-004 — Security

Thông tin tài khoản và dữ liệu người dùng phải được xử lý an toàn trong phạm vi kiến thức và yêu cầu của project.

## NFR-005 — Maintainability

Code phải được tổ chức theo kiến trúc phù hợp với Android project và hạn chế việc đặt toàn bộ logic trong Activity/Fragment.

## NFR-006 — Scalability

Thiết kế MVP cần cho phép bổ sung recommendation, review, admin và các tính năng khác mà không phải viết lại toàn bộ hệ thống.

## NFR-007 — Data Authenticity

Thời gian và vị trí của check-in phải được ghi nhận tự động tại thời điểm chụp và người dùng không được chỉnh sửa. Ảnh check-in chỉ được tạo từ camera trong app.

# 12. Technical Direction — v0.2

Các quyết định đã chốt:

    Android (native)
       ├── Java
       ├── UI: XML Layout (View system)
       ├── ViewModel (package theo feature)
       ├── Repository
       │     ├── DAO (Room)
       │     └── util: LocationHelper → DistanceCalculator
       ├── Room / Local Data (seed: assets/foodmap_seed.json)
       ├── CameraX (Food Check-in)
       ├── Fused Location Provider
       └── Giai đoạn 2: Firebase Auth + Firestore + lưu ảnh

- Dữ liệu: JSON seed → Repository → Room; quan hệ nhiều-nhiều Food ↔ Restaurant qua RestaurantFood.
- Dùng chung Resource\<T\> (LOADING / SUCCESS / ERROR) cho mọi feature.
- MVP không dùng REST API hay backend.
- Bản đồ: Google Maps SDK nếu cấu hình được API key; phương án dự phòng là mở ứng dụng Google Maps qua Intent.

# 13. Agile Development Strategy

FoodMap được phát triển theo Sprint.

Mỗi Sprint bao gồm:

    Sprint Planning
          ↓
    Development
          ↓
    Testing
          ↓
    Sprint Review
          ↓
    Retrospective
          ↓
    Backlog Refinement

Mỗi Sprint phải tạo ra một Increment có thể chạy được.

# 14. Definition of Done — Initial

Một User Story chỉ được xem là hoàn thành khi:

- Code đã implement.
- Chức năng chạy được.
- Các trường hợp lỗi chính đã được xử lý.
- Đã test chức năng.
- UI không có lỗi nghiêm trọng.
- Code đã được review.
- Code được commit lên Git.
- Documentation liên quan được cập nhật.
- Thành viên phụ trách giải thích được luồng xử lý và các đoạn code chính (theo quy định sử dụng AI của môn học).

# 15. Project Success Criteria

FoodMap có hai nhóm tiêu chí thành công.

## Academic Success

- Đáp ứng yêu cầu môn học.
- Hoàn thành các chức năng bắt buộc.
- Có kiến trúc và code rõ ràng.
- Có kiểm thử.
- Có tài liệu.
- Có demo tốt.

## Product Success

Sau phiên bản MVP, project hướng tới:

- Có người dùng thử thực tế.
- Thu thập feedback.
- Theo dõi hành vi sử dụng.
- Cải thiện sản phẩm qua từng iteration.
- Có thể tiếp tục phát triển sau khi kết thúc môn học.

# 16. Course Requirements Mapping (SE114)

Đối chiếu yêu cầu tối thiểu của đồ án tự chọn môn SE114 với FoodMap:

| **Yêu cầu**                                                                           | **Cách FoodMap đáp ứng**                                                                          | **Trạng thái** |
|---------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|----------------|
| ≥ 4 màn hình chức năng                                                                | Trang chủ / danh sách, tìm kiếm + lọc, chi tiết quán, chụp check-in, timeline check-in, yêu thích | Đạt            |
| Thực thể lưu bền vững có thêm / xem / sửa / xóa; validate input; xử lý danh sách rỗng | CheckIn (Room): tạo, xem timeline, sửa caption / số sao, xóa                                      | Đạt (kế hoạch) |
| ≥ 1 tính năng đặc thù Android                                                         | Camera (CameraX) + vị trí (Fused Location)                                                        | Đạt (kế hoạch) |
| Xử lý nghiệp vụ ngoài CRUD                                                            | Tìm kiếm kết hợp bộ lọc; gợi ý quán gần nhất khi check-in                                         | Đạt (kế hoạch) |
| Xử lý từ chối quyền, dữ liệu lỗi, thao tác không hợp lệ                               | Vị trí: chọn quán thủ công; Camera: thông báo + mở Cài đặt                                        | Cần làm        |
| Dữ liệu thử nghiệm                                                                    | assets/foodmap_seed.json + vài check-in mẫu                                                       | Đạt            |
| Dịch vụ ngoài có cách demo khả thi                                                    | MVP offline; Maps có phương án dự phòng                                                           | Đạt            |
| Nộp: mã nguồn GitHub có lịch sử commit, hướng dẫn cài đặt, demo                       | Mỗi thành viên commit phần feature mình sở hữu                                                    | Duy trì        |
| Báo cáo 20–50 trang; đề cương 2–4 trang                                               | Đề cương: MSSV1_MSSV2_SE114_FoodMap.pdf                                                           | Cần làm        |

# 17. Decisions & Open Questions

Các câu hỏi ở v0.1 đã được trả lời:

1.  **Môn học yêu cầu những thành phần Android nào?** → Tối thiểu 4 màn hình; 1 thực thể lưu bền vững có thêm / xem / sửa / xóa; 1 tính năng đặc thù Android hoặc nghiệp vụ ngoài CRUD; xử lý từ chối quyền và dữ liệu lỗi.
2.  **XML hay Jetpack Compose?** → XML Layout.
3.  **Java hay Kotlin?** → Java.
4.  **Có được sử dụng Google Maps SDK không?** → Được phép; cần phương án dự phòng (Intent mở Google Maps).
5.  **Có được gọi REST API không?** → Được phép, nhưng MVP không dùng.
6.  **Có được sử dụng Firebase không?** → Được phép; dùng ở Giai đoạn 2 (Social Check-in).
7.  **Có bắt buộc SQLite / Room không?** → Phải có lưu trữ bền vững; nhóm chọn Room.
8.  **Có yêu cầu offline không?** → Không bắt buộc; MVP chọn offline hoàn toàn.
9.  **Đồ án cá nhân hay nhóm?** → Nhóm 2 người (môn quy định 2–3 người, không làm cá nhân).
10. **Thời gian thực hiện bao lâu?** → Chưa rõ — theo dõi thông báo của giảng viên.
11. **Tiêu chí chấm điểm cụ thể?** → Đồ án 70% (vấn đáp), bài tập 30%; giỏi khi đạt ≥ 90% tính năng cam kết, \> 9 điểm cần tính năng sáng tạo.
12. **Có giới hạn thư viện bên ngoài không?** → Không cấm thư viện; chỉ cấm framework đa nền tảng (React Native…).
13. **Dữ liệu nhà hàng lấy từ đâu?** → Nhóm tự xây dựng seed JSON.
14. **Có cần triển khai ứng dụng thực tế không?** → Không bắt buộc; chạy trên máy thật / máy ảo, nộp GitHub + hướng dẫn cài đặt + dữ liệu thử + demo.

Câu hỏi còn mở:

- Hạn nộp đề cương, báo cáo và lịch vấn đáp chính thức.
- Dịch vụ lưu ảnh cho Giai đoạn 2: Firebase (gói Blaze) hay Cloudinary / Supabase.

# 18. Current Product Status

**Status:** Discovery / Sprint 0 — đã chốt scope v0.2

**Current objective:**

> **Viết đề cương đồ án (2–4 trang, theo mẫu của giảng viên) dựa trên Product Specification v0.2.**

**Next milestone:**

> **Đề cương được duyệt; dựng khung app (Room + seed + navigation) và bắt đầu Sprint 1.**

**Team split (dự kiến) — Feature Ownership + Shared Foundation:**

- Thành viên A: Food Check-in (CameraX, vị trí, gợi ý quán, timeline).
- Thành viên B: Food Discovery, Filtering, Restaurant Detail, Favorite.
- Dùng chung: Room, Repository, Resource\<T\>, LocationHelper / DistanceCalculator.

**Important principle:**

> Không cần học hết Android trước khi bắt đầu.  
> Kiến thức sẽ được học song song với việc hoàn thành từng Sprint.
