---
title: "Event 1 - FCAJ Community Day"
date: 2026-06-01
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

## Tổng quan sự kiện

Sự kiện **FCAJ Community Day (Tháng 6/2026)** được tổ chức bởi **AWS Study Group / Cộng đồng FCAJ**. Đây là buổi sinh hoạt tập trung vào việc cập nhật các xu hướng mới nhất trong ngành công nghệ, đặc biệt nhấn mạnh vào xu hướng nghề nghiệp trong lĩnh vực Kỹ sư Đám mây và Trí tuệ Nhân tạo (AI), ứng dụng AI trong FinOps và Bảo mật Đám mây, cũng như kiến trúc của các giải pháp AI doanh nghiệp như Amazon Q Business và Model Context Protocol (MCP) Server.

---

## Mục tiêu tham gia sự kiện

Mục tiêu chính của em khi tham gia buổi sinh hoạt cộng đồng này là:
- Tìm hiểu xem sự phát triển nhanh chóng của các công cụ lập trình AI đang tác động thế nào đến tương lai nghề nghiệp của kỹ sư phần mềm.
- Khám phá các ứng dụng thực tế của AI trong các mảng chuyên sâu như FinOps (quản lý chi phí) và Cloud Security (bảo mật đám mây).
- Nắm bắt các yêu cầu về hạ tầng và bài toán chi phí khi triển khai các giải pháp AI riêng tư (private AI) cho doanh nghiệp.
- Giao lưu, kết nối với các chuyên gia trong ngành và định hướng lộ trình học tập thực tập sát với nhu cầu thực tế của thị trường.

---

## Nội dung chính

Các bài trình bày và thảo luận trong sự kiện xoay quanh ba chủ đề lớn:

### 1. Xu hướng nghề nghiệp trong kỷ nguyên Agentic AI
Ngành công nghệ đang chứng kiến tốc độ ứng dụng AI nhanh chóng. Các tác tử AI (AI agents) và trợ lý lập trình đang cải thiện đáng kể năng suất. Nhờ vậy, nhiều công ty đang nâng cao tiêu chuẩn tuyển dụng đối với ứng viên. Tuy nhiên, khi hệ thống đám mây phát triển, việc quản lý hạ tầng ngày càng phức tạp, và bản thân AI không thể tự hiểu đầy đủ ngữ cảnh của mã nguồn, hạ tầng và logic nghiệp vụ trong các hệ thống doanh nghiệp lớn.

### 2. Ứng dụng AI trong FinOps và Bảo mật đám mây
- **FinOps:** Các đội ngũ tài chính thường thiếu kiến thức kỹ thuật về đám mây, trong khi kỹ sư lại không rành về quản lý chi phí tài chính. AI giải quyết khoảng trống này bằng cách phân tích dữ liệu hóa đơn AWS, phát hiện các mẫu chi tiêu bất thường và đưa ra chiến lược tối ưu hóa.
- **Bảo mật đám mây:** Các vấn đề bảo mật đôi khi bị bỏ qua hoặc phát hiện quá muộn. Các AI Agents có thể tự động hóa nhiều tác vụ bảo mật như: đánh giá cấu hình Infrastructure as Code (IaC), hỗ trợ kiểm thử xâm nhập (penetration testing) và phân tích log hệ thống liên tục để phát hiện mối đe dọa.

### 3. Xem xét chi phí cho hạ tầng AI riêng biệt
Khi triển khai các giải pháp AI cho doanh nghiệp (như Amazon Q Business hay MCP Server) bên trong mạng riêng ảo (VPC), các tổ chức phải tính đến chi phí hạ tầng để duy trì tính bảo mật. Một số chi phí hàng tháng ước tính bao gồm:
- **Route 53 Resolver:** ~180$ (Phân giải DNS cho private endpoints)
- **Application Load Balancer (ALB):** ~32$ (Định tuyến request)
- **EC2 instances:** Tùy thuộc loại instance (Lưu trữ MCP Server)
- **AWS Secrets Manager & Data Transfer:** Trả theo mức sử dụng
Nhìn chung, chi phí hạ tầng cố định ước tính khoảng 250–350 USD/tháng, chưa bao gồm chi phí sử dụng model AI và xử lý dữ liệu.

---

## Kiến thức thu nhận được

Qua việc tích cực tham gia các phiên thảo luận, em đã đúc kết được nhiều góc nhìn quan trọng:
- **AI là cộng sự, không phải sự thay thế:** Các vai trò như Cloud Engineer, DevOps hay Solution Architect vẫn không thể thiếu vì đòi hỏi kinh nghiệm thực tiễn và khả năng ra quyết định kiến trúc. Thay vì lo lắng bị thay thế, kỹ sư nên học cách dùng AI để tự động hóa các tác vụ lặp đi lặp lại.
- **Chi phí hạ tầng ẩn:** Nhiều dự án AI chỉ chú trọng vào giá API của LLM mà bỏ qua chi phí của các hạ tầng hỗ trợ mạng (VPC, Load Balancers, Secrets Manager).
- **Hoạch định dung lượng là bắt buộc:** Chi phí hạ tầng phải được tính toán dựa trên lượng người dùng dự kiến và lưu lượng dữ liệu truyền tải trước khi đưa giải pháp vào môi trường sản xuất (Production).

---

## Ứng dụng vào dự án thực tập

Những góc nhìn từ sự kiện FCAJ Community Day đã ảnh hưởng trực tiếp đến cách em tiếp cận hạ tầng của dự án **Startups Blogs**:
- **Chủ động quản lý chi phí (Tư duy FinOps):** Em sẽ chú ý theo dõi bảng thanh toán AWS (billing dashboard) và tối ưu hóa tài nguyên cho hệ thống Startups Blogs, đảm bảo kiến trúc không chỉ chạy đúng mà còn tối ưu về mặt chi phí.
- **Ưu tiên bảo mật:** Áp dụng tư duy bảo mật vào hệ thống bằng cách rà soát kỹ lưỡng các tệp cấu hình và phân quyền IAM, ngăn chặn các lỗ hổng trước khi triển khai lên môi trường Production.
- **Sẵn sàng cho tương lai:** Việc hiểu rõ các thành phần hạ tầng cần thiết cho Private AI (VPC, ALB, Route 53) giúp em chuẩn bị sẵn sàng cho các kịch bản tương lai nếu dự án Startups Blogs cần tích hợp các AI agents một cách bảo mật.

---

## Hình ảnh

![FCAJ Community Day](/images/events/event3.jpeg)
<p align="center"><i>Hình: FCAJ Community Day</i></p>

<p align="center"><em>Hình 1. Ảnh chụp tập thể tại sự kiện FCAJ Community Day - Tháng 6/2026.</em></p>

---

## Kết luận

Việc tham gia **FCAJ Community Day** là một trải nghiệm vô cùng bổ ích, giúp em mở rộng tầm nhìn về sự giao thoa giữa Điện toán đám mây và Trí tuệ nhân tạo. Sự kiện củng cố một thực tế rằng, dù công cụ AI đang thay đổi cách em viết code, thì những kỹ năng kỹ sư cốt lõi—thiết kế hệ thống, bảo mật và độ tin cậy vận hành—lại càng trở nên quan trọng hơn bao giờ hết. Những bài học về FinOps và hoạch định chi phí hạ tầng mang lại giá trị thực tế to lớn, hỗ trợ trực tiếp cho tư duy ra quyết định của em trong dự án Startups Blogs cũng như trên con đường phát triển sự nghiệp trở thành một Kỹ sư Đám mây.
