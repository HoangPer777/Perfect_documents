# Project Audit Report: Perfect Market Platform

**Date:** April 18, 2026  
**Auditor:** Senior Software Architect + Technical Auditor

---

## 1. Executive Summary
Dự án **Perfect Market** hiện đang ở giai đoạn **Structural Foundation (Initial Skeleton)**. Toàn bộ cấu trúc thư mục, cấu hình Docker, và các thực thể dữ liệu cốt lõi đã được thiết lập cho cả Frontend (Next.js) và Backend (Spring Boot). Tuy nhiên, hầu hết các logic nghiệp vụ, xử lý bảo mật, và tích hợp bên thứ ba (Stripe, Cloudinary, S3) mới dừng lại ở mức **Placeholder/TODO**.

---

## 2. Current Folder Structure

### Backend (Spring Boot - Modular Monolith)
- `src/main/java/com/perfectmarket/modules/`: Đây là trái tim của hệ thống. 
    - `auth/`: Quản lý User, Role, và JWT Security.
    - `product/`: Quản lý danh mục (Category) và sản phẩm (Product).
    - `order/`: Quản lý quy trình Task Lifecycle (Task, TaskService).
    - `payment/`: Quản lý ví (Wallet) và giao dịch.
    - `service/`: Định nghĩa các gói dịch vụ (Basic, Pro, VIP).
    - `review/`: Hệ thống đánh giá và khiếu nại (Review, Dispute).
- `src/main/resources/db/migration/`: Thư mục trống chờ SQL scripts (Flyway).

### Frontend (Next.js - Feature-based App Router)
- `app/(auth)/`: Nhóm các trang đăng nhập/đăng ký (không hiện trong URL).
- `app/(dashboard)/`: Layout cho trang quản trị của Designer và Customer.
- `app/products/`: Listing và chi tiết sản phẩm.
- `components/shared/`: Các UI dùng chung như Navbar, Footer.
- `store/`: Quản lý state toàn cục bằng Zustand.

---

## 3. Architecture Intent Detected
Hệ thống được định hướng theo kiến trúc **Modular Monolith**:
- **Tư duy chia module**: Mỗi module trong backend (auth, order, product) được thiết kế để có thể tách ra thành Microservices trong tương lai.
- **Database**: Sử dụng PostgreSQL với quan hệ chặt chẽ (ERD 35 bảng), đảm bảo tính toàn vẹn dữ liệu cho marketplace.
- **Frontend Isolation**: Tách biệt hoàn toàn repository để có thể deploy độc lập (Vercel/Docker).

---

## 4. Completed Modules
Các phần sau đây đã được hoàn thiện về mặt **Cấu trúc & Định nghĩa**:
- **Project Scaffold**: Maven (Java 21) & Next.js 14.
- **Entity Domain Model**: Toàn bộ các Class Entity (User, Task, Product, v.v.) đã được map đúng theo yêu cầu database.
- **Infrastructure**: Dockerfile và docker-compose cho cả 2 repo.
- **Routing & State**: Hệ thống route Next.js và Zustand store (Auth).

---

## 5. TODO / Placeholder Findings

| File Path | Ghi chú | Ưu tiên |
| :--- | :--- | :--- |
| `TaskService.java` | Toàn bộ logic workflow (Accept, Revision, Dispute) đang là rỗng. | **High** |
| `AuthController.java` | JWT Login/Register chưa có logic xử lý thực sự. | **High** |
| `application.yml` | Thiếu API Key cho Cloudinary, Stripe, S3. | **Medium** |
| `Navbar.tsx` | Thanh tìm kiếm chưa được kết nối API. | **Medium** |
| `Designer Dashboard (page.tsx)` | Các con số thống kê đang là hardcode "0". | **Medium** |

---

## 6. Legacy Code To Replace
- **Mock Auth**: Cần thay thế logic register rỗng bằng mã hóa mật khẩu (BCrypt) và trả về JWT token.
- **Fake Layout Stats**: Các dashboard cần fetch dữ liệu từ Repository thay vì hiển thị tĩnh.
- **File System**: Hiện tại file-upload repository chưa được implement, cần tích hợp Cloudinary (cho ảnh) và S3 (cho source files).

---

## 7. Risks & Technical Debt
1. **Security**: Hiện tại chưa có cấu hình `SecurityFilterChain` cụ thể, các API đang để mở hoàn toàn.
2. **Validation**: Thiếu kiểm tra dữ liệu đầu vào (Bean Validation `@Valid`).
3. **Transaction**: Các quy trình thanh toán và cập nhật ví cần sử dụng `@Transactional` để tránh mất mát dữ liệu.
4. **Error Handling**: Hệ thống chưa có `GlobalExceptionHandler` để trả về lỗi chuẩn cho Frontend.

---

## 8. Recommended Next Steps (Roadmap)
1. **Phase 1 (MVP)**: Hoàn thiện tính năng Register/Login và Designer đăng tải Product/Service.
2. **Phase 2 (Transaction)**: Triển khai quy trình Order -> Payment (Stripe) -> Task Creation.
3. **Phase 3 (Engagement)**: Hệ thống Chat WebSockets, Review, và Dispute Resolution.

---

## 9. Final Verdict
Cấu trúc hiện tại rất **Vững chắc (Solid)** và đúng chuẩn Senior. Dự án đã sẵn sàng để các developer nhảy vào triển khai logic nghiệp vụ mà không cần lo lắng về việc tổ chức code.

---
