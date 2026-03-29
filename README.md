UK Online Retail — Revenue Dashboard

📌 Giới thiệu Dự án này thực hiện phân tích dữ liệu bán lẻ trực tuyến (UK Online
Retail) bằng Python, với mục tiêu:

1. Làm sạch dữ liệu giao dịch.
2. Tính toán các chỉ số doanh thu theo thời gian, quốc gia, sản phẩm.
3. Thực hiện phân tích RFM (Recency, Frequency, Monetary) để phân khúc khách
   hàng.
4. Trực quan hóa kết quả bằng dashboard nhiều biểu đồ.

⚙️ Công nghệ sử dụng Python 3.x Pandas: xử lý và tổng hợp dữ liệu. Matplotlib:
trực quan hóa dữ liệu. Matplotlib Gridspec: bố cục dashboard. Warnings: tắt cảnh
báo không cần thiết.

📂 Quy trình phân tích Load Data

Đọc file CSV retail_data.csv với encoding ISO-8859-1.

Data Cleaning

Loại bỏ CustomerID bị null.

Giữ lại các giao dịch có Quantity > 0 và UnitPrice > 0.

Chuyển đổi InvoiceDate sang kiểu datetime.

Tạo cột Revenue = Quantity * UnitPrice.

Tạo cột Month để phân tích theo tháng.

Aggregation

Doanh thu theo tháng.

Doanh thu theo quốc gia (top 8).

Doanh thu theo sản phẩm (top 8).

RFM Analysis

Recency: số ngày kể từ lần mua gần nhất.

Frequency: số lượng hóa đơn duy nhất.

Monetary: tổng doanh thu.

Phân khúc khách hàng theo percentile (Low/Medium/High).

Mapping sang nhóm hành vi: VIP, Potential Whale, Loyal Middle, Middle Risk,
Brand Fans, Churn Risk.

Visualization (Dashboard)

Doanh thu theo tháng (line chart).

Doanh thu theo quốc gia (bar chart).

Top sản phẩm theo doanh thu (bar chart).

Tỷ trọng doanh thu theo nhóm RFM (donut chart).

Số khách hàng theo nhóm RFM (bar chart).

Doanh thu theo nhóm RFM theo tháng (stacked bar chart).

📊 Kết quả File dashboard được lưu dưới dạng retail_dashboard.png.

Dashboard hiển thị toàn cảnh doanh thu, phân khúc khách hàng, và sản phẩm chủ
lực.

🚀 Cách chạy pip install pandas matplotlib python retail_dashboard.py

🔮 Hướng phát triển

- Xuất dữ liệu RFM sang CSV để dùng cho clustering (K-means).
- Tích hợp thêm Power BI hoặc Tableau để trực quan hóa nâng cao.
- Phân tích giỏ hàng (basket analysis) để tìm sản phẩm thường mua cùng nhau.
=======

>>>>>>> c3415cf0fa6df92185df40c8866303c1f00e576f
