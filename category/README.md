# Icon danh mục ORIGAMI

Thêm ảnh icon vào chính thư mục `category` này, theo tên file trong bảng bên dưới. Không cần tạo ảnh giả cho icon chưa có. Ưu tiên WebP/PNG nền trong suốt, ảnh vuông khoảng 128–256 px.

## Dùng trên GitHub và Remote Config

1. Tìm icon và lưu theo tên file tương ứng. Nếu dùng PNG/JPG thay WebP, sửa đuôi file trong JSON hoặc chạy lại script.
2. Commit/push thư mục `category` lên GitHub repo `hoang6845/data_clone_1`, nhánh `main`. App tải URL raw GitHub, nên file chỉ lưu trên máy sẽ chưa hiển thị trong app.
3. Trên Firebase project `origami-android-ee03c`, tạo key **`origami_category_icons`**, kiểu **JSON**. Dán toàn bộ nội dung file `origami_category_icons.json` rồi Publish. Key này chỉ quản lý icon; không thay thế `origami_catalog` hoặc cấu hình quảng cáo.
4. Mở lại app và chờ tải config thành công. Bản release có thời gian cache Remote Config khoảng 1 giờ.

JSON đã có URL dự kiến cho tất cả danh mục. Những ảnh chưa có trên GitHub sẽ dùng icon local hiện tại của từng danh mục. URL rỗng, thiếu ID, URL lỗi, ảnh 404 hoặc mất mạng khi ảnh chưa cache cũng dùng icon local. JSON lỗi toàn bộ sẽ giữ config icon hợp lệ gần nhất.

Để bỏ một icon remote, xóa entry của ID đó hoặc đặt giá trị thành chuỗi rỗng `""`, rồi Publish. Để bỏ toàn bộ icon remote, dùng `{"schemaVersion":1,"icons":{}}`. Khi thay nội dung ảnh nhưng giữ tên file, nên thêm tham số phiên bản vào URL, ví dụ `origami_new.webp?v=2`, để Glide tải lại thay vì dùng ảnh cache.

App cần được cập nhật một lần lên bản có hỗ trợ key icon này. Sau đó thêm/sửa/xóa icon qua GitHub và Remote Config không cần build lại app. Schema Room không thay đổi; bài, favorite và tiến độ không bị tác động.

## Tên file

| Danh mục | ID | Tên file đề xuất |
|---|---|---|
| All | `origami_all` | `origami_all.webp` |
| New | `origami_new` | `origami_new.webp` |
| Weapons | `origami_weapons` | `origami_weapons.webp` |
| Halloween | `origami_halloween` | `origami_halloween.webp` |
| Christmas | `origami_christmas` | `origami_christmas.webp` |
| Airplanes | `origami_airplanes` | `origami_airplanes.webp` |
| Animal | `origami_animal` | `origami_animal.webp` |
| Dinosaur | `origami_dinosaur` | `origami_dinosaur.webp` |
| Events | `origami_events` | `origami_events.webp` |
| Clothes | `origami_clothes` | `origami_clothes.webp` |
| Flower | `origami_flower` | `origami_flower.webp` |
| Food & Fruit | `origami_fruit` | `origami_fruit.webp` |
| Furniture | `origami_furniture` | `origami_furniture.webp` |
| Birds | `origami_birds` | `origami_birds.webp` |
| Insects | `origami_insects` | `origami_insects.webp` |
| Vehicle | `origami_vehicle` | `origami_vehicle.webp` |
| Boats | `origami_boats` | `origami_boats.webp` |
| Marine Animals | `origami_marine_animals` | `origami_marine_animals.webp` |

## Tạo lại JSON theo các file đã thêm

Chạy từ thư mục dự án app `C:/origami-world`:

```powershell
python tools/generate_category_icons.py --icon-dir C:/data_1/category
```

Script chỉ đọc thư mục ảnh. JSON mới nằm ở `docs/remote-config/origami_category_icons.json`; bản sao cùng README nằm ở `docs/remote-config/category/`. Copy JSON mới vào thư mục `C:/data_1/category` nếu muốn lưu cùng repo ảnh. Script chọn file WebP/PNG/JPG/JPEG đã có; khi chưa có ảnh sẽ tạo URL dự kiến `.webp` để app fallback. Nếu có nhiều đuôi ảnh cùng một ID, script báo lỗi để tránh chọn nhầm.
