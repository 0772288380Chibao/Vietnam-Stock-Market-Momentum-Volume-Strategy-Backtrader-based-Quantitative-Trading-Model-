##  README chi tiết cho GitHub
 Mô tả dự án

Dự án này triển khai chiến lược Volume-Momentum Trading bằng thư viện Backtrader, kết hợp sức mạnh của momentum, khối lượng giao dịch, và đường trung bình động (MA) để xác định cơ hội mua/bán tối ưu trên thị trường chứng khoán Việt Nam.
Mục tiêu của chiến lược là tối đa hóa lợi nhuận điều chỉnh rủi ro (risk-adjusted return) thông qua việc tự động chọn cổ phiếu có động lượng cao và quản trị vốn hiệu quả.

##  Cấu trúc chiến lược
 Momentum Calculation

- Momentum được tính từ hồi quy tuyến tính log-returns của giá đóng cửa.

- Hệ số góc (slope) được annualize, nhân với R² để đo sức mạnh của xu hướng.

 VolumeMomentumStrategy

- Sử dụng hai đường MA100 và MA200 để xác định xu hướng chính.

- Khi giá vượt MA100 hoặc MA200 → tăng quy mô vị thế tương ứng 10% và 20%.

- Điều kiện mua: Giá tăng > buy_threshold (mặc định 1%), Khối lượng tăng mạnh > 1.7 × SMA20(volume)

- Điều kiện bán: Giá giảm > sell_threshold (mặc định 6%), Khối lượng tăng > 1.3 × SMA20(volume)

- Quản lý rủi ro: Stop Loss 10%, Take Profit 35%.

Theo dõi và tính toán Sharpe Ratio, Max Drawdown, Daily Return.

 Momentum-based Stock Selection

- Tính momentum cho danh sách cổ phiếu (VN100).

- Cập nhật danh sách cổ phiếu top 40% momentum cao nhất mỗi 20 ngày.

- Backtest lần lượt trên từng cổ phiếu và tổng hợp kết quả hiệu suất.

 Chỉ số đo lường hiệu suất

- Sharpe Ratio	Đo lường lợi nhuận vượt trội so với rủi ro.
- Max Drawdown (%)	Mức sụt giảm tối đa của danh mục.
- Return (%)	Tỷ suất lợi nhuận tương đối.
- Average Momentum	Mức động lượng trung bình của cổ phiếu.
   Công nghệ sử dụng

- Python, Backtrader, Pandas, Numpy, Scipy

- Vnstock API (lấy dữ liệu cổ phiếu Việt Nam)

- Các mô hình momentum-based selection và trend-following dynamic sizing

 Pipeline
1. Tính toán momentum cho từng cổ phiếu trong VN100
2. Chọn top 40% cổ phiếu có momentum cao nhất
3. Cập nhật danh sách top mỗi 20 ngày
4. Chạy backtest cho từng cổ phiếu với VolumeMomentumStrategy
5. Tổng hợp và báo cáo các chỉ số hiệu suất
