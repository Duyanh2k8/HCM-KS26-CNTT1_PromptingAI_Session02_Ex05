# Bài 5: Cơ chế In-Context Learning trong Phân loại Review Khách hàng
## Phần 1. Phân tích cơ chế
In-Context Learning (ICL) là khả năng AI học cách làm một nhiệm vụ thông qua những ví dụ được cung cấp ngay trong Prompt mà không cần train lại model hay thay đổi trọng số.

Cơ chế này có thể hiểu như sau: Khi người dùng đưa ra một số ví dụ gồm câu đánh giá và kết quả phân loại, AI sẽ dựa vào đó để nhận biết cách phân biệt lời khen thật với những câu nói mỉa mai. Sau đó, khi gặp một đánh giá mới, AI sẽ áp dụng những gì đã nhận ra từ các ví dụ để đưa ra kết quả.

Trong trường hợp của TechShop, câu nói máy có nhiệt độ CPU lên đến 98 độ C nhưng lại bảo không cần bật lò sưởi thực chất là đang chê máy quá nóng. Nếu chỉ nhìn vào những từ như "đẹp mê ly", "đầm tay" hay "khỏi cần bật lò sưởi", AI rất dễ hiểu nhầm đây là lời khen.

Vì vậy, việc cung cấp ví dụ mẫu giúp AI hiểu được ý nghĩa thực sự của câu nói thay vì chỉ dựa vào nghĩa của từng từ riêng lẻ.
## Phần 2. Sửa lỗi bằng Few-shot
### Prompt Few-shot đề xuất cho TechShop:
Bạn là nhân viên kiểm duyệt đánh giá sản phẩm của TechShop. Nhiệm vụ của bạn là đọc đánh giá của khách hàng và phân loại thành 2 loại: TÍCH CỰC hoặc TIÊU CỰC.

Khi phân loại, cần đọc hiểu toàn bộ câu đánh giá. Không được chỉ nhìn vào những từ mang ý nghĩa khen ngợi vì khách hàng có thể đang nói mỉa mai hoặc khen đểu.

**Ví dụ 1: Về nhiệt độ máy**

Input: "Máy mát thật đấy, mới chơi game một lúc mà CPU đã lên 98 độ, mùa đông chắc khỏi cần bật máy sưởi."

Output: TIÊU CỰC

Lý do: Khách hàng đang mỉa mai vì máy quá nóng khi chơi game.

**Ví dụ 2: Về thời lượng pin**

Input: "Pin trâu quá, mới dùng buổi sáng mà đến trưa đã hết sạch, đúng là không cần mang sạc theo làm gì!"

Output: TIÊU CỰC

Lý do: Khách hàng đang chê pin nhanh hết, thời gian sử dụng không đáp ứng nhu cầu.

**Ví dụ 3: Về thời gian giao hàng**

Input: "Shop giao hàng nhanh ghê, đặt từ tuần trước mà giờ mới nhận được, chắc shipper đi du lịch rồi mới giao."

Output: TIÊU CỰC

Lý do: Khách hàng đang nói mỉa mai vì thời gian giao hàng quá lâu.

**Bây giờ hãy thực hiện nhiệm vụ sau:**

Review: {review}

Yêu cầu:
- Phân loại đánh giá thành TÍCH CỰC hoặc TIÊU CỰC.
- Giải thích ngắn gọn lý do phân loại.
- Chú ý những câu nói mỉa mai, nghĩa bóng hoặc tiếng lóng công nghệ.
- Không kết luận chỉ dựa vào những từ ngữ tích cực xuất hiện trong câu.
