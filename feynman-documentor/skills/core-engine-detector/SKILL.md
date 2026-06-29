---
name: core-engine-detector
description: Bộ dò tìm, phân tích và cô lập kiến trúc lõi/điểm nghẽn hiệu năng vật lý của mã nguồn hoặc tài liệu kỹ thuật.
---

# Skill: Core Engine Detector

Skill này hướng dẫn Agent dò tìm, cô lập và phân tích thuật toán cốt lõi cùng các điểm nghẽn hiệu năng vật lý (RAM, Disk, Network, CPU) của một hệ thống mã nguồn hoặc bộ tài liệu ngẫu nhiên. Đầu ra của skill này phục vụ làm đầu vào tin cậy cho tài liệu học tập FDL hoặc các báo cáo tái cấu trúc hệ thống.

---

## 1. Quy trình dò tìm 4 bước (Feynman Core Auditing)

Khi tiếp cận một mã nguồn hoặc tài liệu mới, Agent bắt buộc phải đi qua 4 bước phân tích nguyên lý gốc để bóc tách hệ thống:

### Bước 1: Khử quy nạp về Giới hạn vật lý (Physical Constraint Reduction)
*   **Mục tiêu**: Xác định tài nguyên đắt đỏ nhất mà hệ thống đang quản lý hoặc cố gắng tối ưu hóa.
*   **Hành động**: Tìm câu trả lời cho các câu hỏi:
    1.  Hệ thống này giao tiếp với ổ cứng (Disk I/O) như thế nào? (Đọc tuần tự hay ngẫu nhiên? Đọc theo trang đĩa kích thước bao nhiêu?).
    2.  Hệ thống quản lý RAM như thế nào? (Có dùng cache, bảng băm, hay hàng đợi bộ nhớ tạm không?).
    3.  Tốc độ xử lý của CPU có bị ảnh hưởng bởi các thuật toán sắp xếp, khóa đồng bộ (mutex/lock) hoặc luồng xử lý không?
    4.  Mạng (Network) có bị giới hạn bởi số lần bắt tay (RTT) hay băng thông truyền tải gói tin không?

### Bước 2: Phân biệt Gốc và Ngọn (Fundamental vs. Customized Engine)
*   **Mục tiêu**: Tránh lỗi nhảy cóc (Cargo Cult) vào các kỹ thuật tối ưu tùy biến mà bỏ quên cấu trúc nền tảng.
*   **Yêu cầu**: Agent bắt buộc phải phân tích và phân định rõ hai tầng kiến trúc:
    1.  **Core Engine Nguyên thủy (Fundamental Core Engine)**: Cấu trúc dữ liệu hoặc thuật toán cơ sở giải quyết bài toán gốc của ngành khoa học máy tính (Ví dụ: B+Tree giải quyết bài toán tìm kiếm khoảng trên đĩa; Hash Table giải quyết bài toán $O(1)$ key-value; DAG giải quyết bài toán lịch sử phiên bản).
    2.  **Core Engine Tùy biến (Customized Core Engine)**: Các cơ chế tối ưu đặc thù được đắp lên cấu trúc nguyên thủy để phục vụ bối cảnh cụ thể của dự án (Ví dụ: Copy-on-Write để tránh dùng WAL và khóa đọc; mmap để đẩy việc quản lý trang cho OS Page Cache).
    3.  **Lối thoát cho hệ thống di sản (Legacy System Fallback)**: Nếu hệ thống là dạng ứng dụng nghiệp vụ thuần túy (Enterprise/CRUD) không có giải thuật toán học hay cấu trúc dữ liệu cơ sở rõ ràng, Agent bắt buộc phải xác định Core Engine Nguyên thủy là **Luồng xử lý dữ liệu chính (Main Pipeline)** và tập trung phân tích các điểm nghẽn tích lũy (Accumulative Bottlenecks) như khóa tranh chấp DB, cấp phát RAM liên tục, hay độ trễ I/O mạng.

### Bước 3: Bản đồ luồng dữ liệu lõi (Cruft Stripping & Dataflow Mapping)
*   **Mục tiêu**: Loại bỏ 90% "vỏ bọc" của mã nguồn (code log, bắt lỗi, kiểm tra quyền, parse cấu hình) để tìm ra 10% dòng dữ liệu thực sự chảy qua hệ thống.
*   **Hành động**: 
    1.  Quét cấu trúc thư mục và chỉ ra tối đa 3-5 file chứa linh hồn logic của hệ thống.
    2.  Vẽ sơ đồ luồng dữ liệu (Dataflow) từ thời điểm dữ liệu đi vào hệ thống cho đến khi được xử lý xong và ghi xuống thiết bị lưu trữ/phản hồi.

### Bước 4: Tái cấu trúc 100 dòng code (100-Line Core Blueprint)
*   **Mục tiêu**: Trích xuất thuật toán hoặc cấu trúc dữ liệu cơ bản nhất mà nếu thiếu nó, hệ thống sẽ hoàn toàn sụp đổ.
*   **Hành động**: 
    1.  Thiết kế một đoạn giả mã (pseudocode) hoặc code tối giản mô tả cơ chế hoạt động của thuật toán lõi.
    2.  Giải thích ngắn gọn cơ sở toán học hoặc lô-gíc của giả mã đó.

---

## 2. Đầu ra bắt buộc: Bản đồ Cốt tủy Hệ thống (Core Engine Map)

Sau khi chạy bộ dò tìm, Agent bắt buộc phải tạo ra một tài liệu phân tích có tên là `core_engine_map.md` lưu tại thư mục làm việc của dự án, trình bày theo cấu trúc sau:

```markdown
# Bản đồ Cốt tủy Hệ thống: [Tên Hệ Thống / Dự Án]

## 1. Giới hạn Vật lý cốt lõi
- [Nêu rõ tài nguyên vật lý đắt đỏ nhất hệ thống quản lý]
- [Lý do tại sao giới hạn này lại ảnh hưởng đến hiệu năng]

## 2. Phân tách Kiến trúc Lõi
### A. Core Engine Nguyên thủy (Fundamental Core Engine)
- [Nêu rõ cấu trúc toán học/giải thuật cơ bản nhất - Hoặc Main Pipeline nếu là Legacy]
- [Giải thích bài toán gốc mà nó xử lý]

### B. Core Engine Tùy biến (Customized Core Engine)
- [Các cơ chế tối ưu đắp lên - Ví dụ: COW, mmap, Freelist]
- [Tại sao dự án lại lựa chọn sự tùy biến này để đánh đổi hiệu năng]

## 3. Bản đồ Luồng Dữ liệu (Core Dataflow)
- [Liệt kê danh sách 3-5 file chứa logic lõi của hệ thống]
- [Sơ đồ Mermaid mô tả luồng đi của dữ liệu qua các tệp tin này]

## 4. Thuật toán/Cấu trúc dữ liệu tối giản (100-Line Blueprint)
```[Ngôn ngữ phù hợp]
// Giả mã hoặc mã nguồn tối giản mô tả lõi hệ thống
```

## 5. Vết nứt hiệu năng (Fracture Points)
- [Mô tả chi tiết 1-2 kịch bản hệ thống sẽ bị nổ tung/treo khi tải tăng 1000 lần]
- [Nguyên nhân vật lý dẫn đến sự đứt gãy đó]
```

---

## 3. Quy trình tự kiểm tra của Bộ dò tìm (Detector Self-Grill)

Trước khi xuất bản tệp `core_engine_map.md`, Agent phải tự trả lời và ghi nhận câu trả lời cho 3 câu hỏi kiểm định chất lượng:
1.  *Mình đã phân tách rõ ràng giữa thuật toán nguyên thủy (Fundamental) và kỹ thuật tùy biến (Customized) chưa?*
2.  *Sơ đồ luồng dữ liệu đã thể hiện được các bước đọc/ghi vật lý (Disk/RAM/Network) hay mới chỉ mô tả các hàm gọi nhau?*
3.  **Xác thực Ký hiệu Vật lý (Physical Symbol Verification)**: *Mình đã kiểm chứng sự tồn tại vật lý bằng công cụ đọc file đối với 100% đường dẫn tệp tin, tên Class/Struct và tên Hàm được đề cập trong Core Engine Map chưa? (Tuyệt đối cấm tự bịa ra tên file hoặc ký hiệu không có thật).*
