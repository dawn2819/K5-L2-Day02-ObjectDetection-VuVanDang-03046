# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp

| Lớp | Định nghĩa của bạn | Ví dụ/điểm phân biệt |
| --- | --- | --- |
| `car` | Xe con, sedan, hatchback, SUV gia đình, taxi, xe bán tải (pickup cabin nhỏ). | Xe cá nhân dưới 9 chỗ ngồi; xe bán tải nhỏ chở người/hàng nhẹ vẫn tính là `car`. |
| `truck` | Xe tải chở hàng thương mại, xe đầu kéo, xe container, xe bồn. | Thân xe có cabin tách biệt rõ ràng với thùng hàng phía sau; kích thước lớn phục vụ vận tải hàng hóa. |
| `bus` | Xe buýt công cộng, xe khách du lịch, minibus chở khách nhiều chỗ (>16 chỗ). | Thân xe dài, nhiều hàng ghế hành khách, cửa lên xuống đặc thù xe khách. |
| `van` | Xe van, minivan, MPV cỡ lớn hoặc xe chở hàng thùng kín liền khối. | Thân xe dạng hộp liền một khối giữa khoang lái và khoang chở hàng/chở người; không có thùng hàng rời như `truck`. |

## Quy tắc chung

- Box bám sát vật thể nghĩa là: Bounding box ôm sát mép ngoài nhìn thấy được của thân xe, không lấy dư mặt đường, bầu trời hay vật thể bên cạnh.
- Vật thể bị che khuất: Nếu bị che một phần bởi cây cối, cột đèn hoặc xe khác, chỉ vẽ box bao quanh phần thực tế nhìn thấy được, miễn là nhận diện được lớp. Nếu phần nhìn thấy quá nhỏ (<10-15%) không nhận diện được thì bỏ qua.
- Vật thể bị cắt bởi rìa ảnh: Box chạm sát mép biên ảnh; tuyệt đối không tưởng tượng phần thân xe nằm ngoài khung hình.
- Vật thể rất nhỏ/mơ hồ: Xe ở hậu cảnh quá xa, mờ nhòe không đủ đặc trưng nhận diện class thì không gán để tránh tạo nhiễu cho mô hình.

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh | Tình huống | Quyết định cuối | Lý do theo schema |
| --- | --- | --- | --- |
| `drive_003` | Xe tải nhỏ / xe van chở hàng thùng kín nhìn từ phía sau ở khoảng cách trung bình. | Gán `van` (hoặc `truck` tùy thiết kế thùng). | Thân xe dạng khối hộp liền, nếu cabin tách rời thùng thì gán `truck`, liền khối thì gán `van`. |
| `drive_019` | Nhiều xe con nối đuôi nhau và bị xe đi trước che khuất một phần đầu xe. | Vẽ từng box riêng biệt ôm phần thân nhìn thấy của mỗi xe. | Quy tắc mỗi xe một box, không gộp hai xe thành một box lớn; không đoán phần bị che khuất. |
| `drive_027` | Xe ở mép phải khung hình bị cắt một nửa thân xe. | Vẽ box bám từ mép ảnh ôm trọn nửa thân xe còn lại. | Tuân thủ quy tắc cắt khung: chạm biên ảnh, chỉ tính phần xuất hiện trong ảnh. |