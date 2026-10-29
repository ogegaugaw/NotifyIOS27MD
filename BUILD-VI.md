# NotifyIOS 27 MD — hướng dẫn build

## Trạng thái gói

Đây là mã nguồn của dự án `Dynamic-Island--1.6.5.zip` đã được đổi định danh ứng dụng:
- Tên hiển thị: `NotifyIOS 27 MD`
- Application ID / namespace: `com.meixuxdigital.notifyios27`
- Version: `27.0-MD` (versionCode 27)

**Lưu ý quan trọng:** gói đầu vào là dự án Dynamic Island (`com.akira.island`), không phải mã nguồn `DigitalNotify-main` (`com.digitalsmod.digitalnotify`) được mô tả trong yêu cầu. Vì vậy gói này giữ tính năng sẵn có của dự án Dynamic Island; chưa thể xác nhận hoặc tích hợp các lớp `OverlayController.kt`, `GlassBannerView.kt`, `GlassShaderApi33.kt`, `NotificationHistoryStore.kt` và bộ điều khiển âm thanh theo kiến trúc DigitalNotify khi các tệp đó không có trong ZIP đầu vào.

## Build bằng Android Studio

1. Giải nén ZIP.
2. Mở thư mục `Dynamic-Island--1.6.5` bằng Android Studio.
3. Chờ Gradle tải dependencies và sync hoàn tất.
4. Chọn **Build > Build Bundle(s) / APK(s) > Build APK(s)**.
5. APK debug thường nằm ở `app/build/outputs/apk/debug/app-debug.apk`.

Yêu cầu: JDK 17, Android SDK và kết nối mạng lần đầu để Gradle tải distribution/dependencies.

## Build bằng Termux (Android ARM64)

1. Cài các công cụ cần thiết và Android SDK phù hợp với môi trường của bạn.
2. Vào thư mục dự án, sau đó chạy:

   ```sh
   chmod +x gradlew
   ./gradlew assembleDebug
   ```

3. APK debug sẽ được tạo tại `app/build/outputs/apk/debug/app-debug.apk` nếu build thành công.

Nếu gặp lỗi AAPT2 do Gradle tải binary x86_64 trên Android ARM64, cần cấu hình Gradle dùng AAPT2 ARM64 tương thích với SDK/AGP đang cài; không phải lỗi Kotlin của dự án. Không thêm cấu hình đường dẫn AAPT2 cố định vào ZIP vì đường dẫn trên mỗi thiết bị có thể khác nhau.

## Kiểm tra trước khi phát hành

- Cấp quyền Accessibility và Notification Access theo hướng dẫn trong ứng dụng.
- Kiểm tra trên thiết bị thật các tính năng cần quyền hệ thống.
- APK debug được ký bằng debug keystore; không dùng debug APK làm bản phát hành chính thức.
