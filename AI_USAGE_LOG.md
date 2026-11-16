# NHẬT KÝ SỬ DỤNG AI & BẢNG ĐỐI CHIẾU YÊU CẦU (`AI_USAGE_LOG.md`)

- **Dự án:** TEAVENTO – Nền tảng đặt dịch vụ tiệc trà và sự kiện doanh nghiệp
- **Người phụ trách:** Đinh Phạm Mỹ Duyên (AI Manager & QA Tester / Security & Innovation Dev)
- **Mục đích:** Ghi nhận lịch sử sử dụng các công cụ AI trong quá trình phân tích, thiết kế hệ thống và lập bảng đối chiếu giữa đề xuất của AI thứ nhất, phản biện độc lập của AI thứ hai và quyết định cuối cùng của nhóm.

---

## 1. Nhật ký sử dụng AI (AI Usage Log)

| STT | Ngày thực hiện | Thành viên | Công cụ AI sử dụng | Mục đích / Nhiệm vụ (Prompt) | Kết quả đầu ra | Đánh giá & Chỉnh sửa của con người |
| :---: | :---: | :---: | :---: | :--- | :--- | :--- |
| **1** | 14/11 | Nguyễn Thị Kim Nguyên (BA) | AI thứ nhất (ChatGPT) | **Prompt 1 (Nhiệm vụ 3 & 5):** Phân tích mục tiêu, phạm vi dự án (In-scope / Out-of-scope), bảng vai trò người dùng, danh sách chức năng (F01-F08) và yêu cầu phi chức năng. | Bản nháp yêu cầu hệ thống ban đầu (`REQUIREMENTS.md`). | AI 1 sinh ra yêu cầu theo khuôn mẫu web bán lẻ hàng hóa thông thường (như điện thoại/quần áo), thiếu đặc thù đặt lịch tiệc trà, tính giá theo số khách và tùy chỉnh menu của TEAVENTO. |
| **2** | 15/11 | Đinh Phạm Mỹ Duyên (AI Manager) | AI thứ hai (Gemini) | **Prompt 2 (Nhiệm vụ 4):** Đóng vai người phản biện độc lập đánh giá bản yêu cầu của AI 1 dựa trên mô tả đề tài TEAVENTO, vấn đề kinh doanh và khảo sát 3 đối thủ (Trái Cây Vuông Tròn, Sugary, PITO). | Bản phân tích phản biện 6 khía cạnh chuyên môn, bộ quy tắc `AGENTS.md` và bảng đối chiếu. | AI 2 chỉ ra chính xác các điểm lệch pha nghiệp vụ, các chức năng thiếu hụt và rủi ro bảo mật. Nhóm họp thống nhất giữ lại những gì phù hợp với quy mô học phần để cập nhật vào `REQUIREMENTS.md`. |

---

## 2. Bảng tổng hợp đối chiếu (AI 1 đề xuất – AI 2 phản biện – Quyết định của nhóm)

Dưới đây là bảng tổng hợp phân tích thực tế của đề tài TEAVENTO theo đúng mẫu hướng dẫn của học phần:

| Nội dung | AI thứ nhất đề xuất | AI thứ hai phản biện | Quyết định của nhóm |
| :--- | :--- | :--- | :--- |
| **Nền tảng phát triển (Web / Mobile App)** | Có (Phát triển cả ứng dụng Web và Mobile). | Vượt quá phạm vi thời gian 1 học phần và nguồn lực của nhóm 6 sinh viên. | Chỉ phát triển Web Responsive (tương thích Desktop, Tablet, Mobile trình duyệt), lược bỏ Mobile App riêng. |
| **Phạm vi loại trừ (Out-of-Scope):** Drone, AR, Tiền mã hóa | Có (Đưa giao hàng bằng drone, thử sản phẩm AR, tiền mã hóa vào Out-of-scope). | Không cần thiết và xa rời thực tế ngành dịch vụ tiệc trà (Catering). | Loại bỏ và viết lại Out-of-Scope thực tế: Không làm sàn đa nhà cung cấp (như PITO), không quản lý công nợ hợp đồng B2B phức tạp, không định vị GPS nhân sự. |
| **Đăng ký, Đăng nhập & Phân quyền (F01)** | Có (Quản lý tài khoản Khách hàng và Admin). | Cần thiết để quản lý đơn đặt tiệc doanh nghiệp và bảo mật trang quản trị. | Giữ lại, bổ sung kiểm soát phân quyền bằng Middleware (RBAC) và băm mật khẩu (`bcrypt`). |
| **Chức năng tìm kiếm & lọc sản phẩm (F02)** | Có (Lọc theo tên, danh mục, khoảng giá, sắp xếp tiêu chí cơ bản). | Chưa giải quyết hết bài toán kinh doanh; khách đặt tiệc cần lọc theo ngân sách/người và quy mô khách. | Giữ lại và nâng cấp: Lọc gói tiệc theo Loại hình sự kiện, Ngân sách/đầu người, Quy mô số lượng khách và Ngày tổ chức. |
| **Xem chi tiết sản phẩm / Gói tiệc (F03)** | Có (Hiển thị mô tả, hình ảnh, giá, "thông số kỹ thuật" và đánh giá). | Thuật ngữ "thông số kỹ thuật" không phù hợp với tiệc trà; thiếu thông tin định lượng thực đơn và điều kiện đặt tiệc. | Hiển thị hình ảnh bàn tiệc thực tế, Thực đơn chi tiết (Menu), Giá/khách, Số khách tối thiểu (`min_pax`), thời gian chuẩn bị ($\ge 24h$) và dịch vụ đi kèm. |
| **Quản lý giỏ hàng & Tùy chỉnh gói tiệc (F04)** | Có (Chỉ thêm, sửa số lượng hoặc xóa sản phẩm đơn lẻ). | Cần cho quy trình mua hàng nhưng thiếu tính năng tùy chỉnh món lẻ và nhân đơn giá theo số khách. | Giữ lại và mở rộng: Cho phép chọn gói tiệc sẵn, nhập số lượng khách ($\ge min\_pax$), thêm/bớt món phụ (Add-ons) và tự động cập nhật tổng chi phí tức thì. |
| **Đặt lịch dịch vụ (Chọn ngày, giờ & địa điểm setup)** | Không đề xuất (Chỉ nhập địa chỉ nhận hàng thông thường ở bước thanh toán). | Thiếu chức năng cốt lõi giải quyết vấn đề chốt thời gian setup tiệc trước giờ sự kiện bắt đầu. | Bổ sung bắt buộc vào luồng đặt tiệc (F05): Khách chủ động chọn Ngày tổ chức, Khung giờ hoàn tất setup (cách thời điểm đặt tối thiểu 24h) và Quận/Huyện tại TP.HCM. |
| **Thanh toán trực tuyến & Phí vận chuyển/setup** | Có (Mô tả chung là thanh toán trực tuyến cơ bản). | Cần xem xét tích hợp cổng Sandbox cụ thể, quy tắc tính phí vận chuyển/setup và xác thực lại giá ở Backend. | Đưa vào kế hoạch triển khai Giai đoạn 4: Tích hợp VNPay/MoMo Sandbox, tính phí setup cố định theo Quận/Huyện và bắt buộc tính lại tổng tiền ở Server chống sửa giá F12. |
| **Module Mã giảm giá (Voucher)** | Không đề xuất. | Thiếu chức năng đã được phân công trong kế hoạch của nhóm để kích cầu khách hàng B2B/B2C. | Bổ sung vào hệ thống: Cho phép khách áp mã giảm giá hợp lệ ở bước thanh toán và Admin quản lý mã giảm giá. |
| **Theo dõi trạng thái đơn đặt tiệc (F06)** | Có (Theo dõi lịch sử mua hàng và trạng thái xử lý đơn chung chung). | Cần cụ thể hóa chuỗi thư viện phục vụ sự kiện tại chỗ để khách hàng B2B kiểm soát tiến độ. | Giữ lại và chuẩn hóa quy trình 4 bước:<br>`Chờ xác nhận` ➔ `Đã phân công` ➔ `Đang setup` ➔ `Hoàn thành` (kèm trạng thái `Đã hủy`). |
| **Quản lý Gói tiệc, Duyệt đơn & Lịch trống (Admin - F07)** | Có Quản lý sản phẩm (F07), nhưng bỏ quên chức năng Admin duyệt đơn ở bảng F01-F08. | Thiếu quy trình Admin duyệt đơn tiệc, phân công setup và khóa lịch khi quá tải khung giờ phục vụ. | Bổ sung đầy đủ cho Admin Dashboard: Quản lý danh mục gói tiệc/món lẻ, Duyệt & cập nhật tiến độ đơn tiệc, và Quản lý lịch trống dịch vụ. |
| **Thống kê & Báo cáo doanh thu (Admin - F08)** | Có (Xếp mức ưu tiên Thấp / Nice-to-have). | Cần thiết cho Admin Dashboard theo yêu cầu đề tài để theo dõi doanh thu và gói tiệc bán chạy. | Giữ lại, nâng mức ưu tiên lên Trung bình (Medium), hiển thị biểu đồ thống kê doanh thu và số lượng đơn theo thời gian. |
| **Chatbot AI tư vấn thực đơn (Innovation - F09)** | Không đề xuất trong bảng chức năng. | Là chức năng sáng tạo (Innovation) của đề tài nhưng có thể vượt phạm vi nếu huấn luyện mô hình phức tạp. | Đưa vào nhóm chức năng Sáng tạo (Giai đoạn 5): Tích hợp AI Chatbot qua API có giới hạn ngữ cảnh (System Prompt) để gợi ý gói tiệc theo ngân sách và số lượng khách. |
| **Cam kết Uptime 99% & Tự động Backup định kỳ** | Có (Đưa vào yêu cầu phi chức năng). | Vượt phạm vi hạ tầng của đồ án sinh viên chạy trên môi trường thử nghiệm. | Lược bỏ cam kết SLA 99%: Thay bằng cung cấp tệp cấu trúc & dữ liệu mẫu (`.sql` / seed data) để dễ dàng khôi phục và kiểm thử. |

---

## 3. Kết luận rút ra từ quá trình sử dụng AI

* **AI có thể đề xuất và phản biện, nhưng quyết định cuối cùng thuộc về nhóm thực hiện:** Công cụ AI thứ nhất giúp khởi tạo nhanh khung tài liệu nhưng mắc lỗi áp dụng rập khuôn mô hình bán lẻ hàng hóa cho dịch vụ đặt tiệc trà. Công cụ AI thứ hai giúp rà soát chéo, phát hiện các lỗ hổng về quy trình nghiệp vụ (đặt lịch setup, tính giá theo đầu người, duyệt đơn) và bảo mật (lộ khóa `.env` trên GitHub Public, thao túng giá phía Client).
* **Định hướng thực thi của nhóm TEAVENTO:** Nhóm chỉ giữ lại các chức năng giải quyết trực tiếp 3 vấn đề của khách hàng đặt tiệc (báo giá tức thì theo số khách, tùy chỉnh thực đơn linh hoạt, chủ động chọn lịch và theo dõi tiến độ setup), đồng thời cắt giảm các yêu cầu hạ tầng vượt quá sức của sinh viên để đảm bảo hoàn thành đúng tiến độ 6 giai đoạn của học phần.
