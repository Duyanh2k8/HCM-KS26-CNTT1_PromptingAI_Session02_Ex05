# Bài 5: Cơ chế In-Context Learning trong Phân loại Review Khách hàng
## Phần 1. Phân tích cơ chế
In-Context Learning (ICL) là cách AI học thông qua những ví dụ và thông tin được cung cấp trong câu lệnh mà không cần phải huấn luyện lại mô hình.

Cách hoạt động khá đơn giản: Người dùng đưa cho AI một số ví dụ về câu đánh giá và kết quả phân loại đúng. AI sẽ dựa vào đó để nhận ra cách phân biệt giữa lời khen thật và lời chê mang tính mỉa mai. Sau đó, khi gặp một câu đánh giá mới, AI sẽ áp dụng những gì đã nhận biết từ các ví dụ để đưa ra kết quả.

Ví dụ, câu nói máy có nhiệt độ CPU lên đến 98 độ C nhưng lại bảo không cần bật lò sưởi thực chất là đang chê máy quá nóng. Nếu chỉ nhìn vào những từ như "đẹp mê ly" hay "khỏi cần bật lò sưởi", AI rất dễ hiểu nhầm thành lời khen.

Vì vậy, ICL giúp AI hiểu cách sử dụng từ ngữ trong từng tình huống tốt hơn mà không cần thay đổi trọng số của mô hình.
## Phần 2. Sửa lỗi bằng Few-shot
### Prompt đề xuất:
Bạn là nhân viên kiểm tra đánh giá sản phẩm của TechShop. Hãy đọc nội dung khách hàng nhận xét và phân loại thành TÍCH CỰC hoặc TIÊU CỰC.

Lưu ý: Cần đọc hiểu toàn bộ câu, không được chỉ dựa vào những từ mang ý nghĩa khen ngợi. Hãy chú ý những câu nói mỉa mai, nói quá hoặc khen nhưng thực chất là đang chê.

**Ví dụ 1:**

Input: "Máy nóng thật đấy, chơi game một lúc mà CPU lên tận 98 độ, mùa đông chắc khỏi cần máy sưởi."

Output: TIÊU CỰC

Lý do: Khách hàng đang chê máy quá nóng khi sử dụng.

**Ví dụ 2:**

Input: "Pin tốt quá, mới dùng từ sáng đến trưa đã hết sạch, đúng là không cần mang sạc theo làm gì!"

Output: TIÊU CỰC

Lý do: Khách hàng đang mỉa mai vì pin nhanh hết, không sử dụng được lâu.

**Ví dụ 3:**

Input: "Shop giao hàng nhanh thật, đặt hàng cả tuần mới nhận được, chắc shipper đi tham quan trước khi giao."

Output: TIÊU CỰC

Lý do: Khách hàng không hài lòng vì thời gian giao hàng quá lâu.

**Bây giờ hãy phân loại đánh giá sau:**

Review: {review}

Yêu cầu:
- Kết quả: TÍCH CỰC hoặc TIÊU CỰC.
- Giải thích ngắn gọn lý do phân loại.
- Chú ý ý nghĩa thực sự của câu nói, tránh hiểu nhầm lời mỉa mai thành lời khen.
