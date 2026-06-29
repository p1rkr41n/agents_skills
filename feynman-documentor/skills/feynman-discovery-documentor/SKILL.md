---
name: feynman-discovery-documentor
description: Trình biên soạn và xác thực tài liệu học tập theo cấu trúc Vòng lặp Khám phá Feynman (FDL), biến tài liệu nông cạn thành tài liệu thấu hiểu sâu sắc.
---

# Skill: Feynman Discovery Documentor (FDL)

Skill này hướng dẫn Agent biên soạn, cấu trúc và xác thực tài liệu học tập kỹ thuật theo phương pháp **Vòng lặp Khám phá Feynman (Feynman Discovery Loop - FDL)**, đảm bảo chất lượng thấu hiểu thực chất và chống lại việc lãng phí chữ nghĩa sáo rỗng (Cargo Cult).

---

## 1. Quy tắc Khởi động & Kiểm tra tham số (Startup & Parameters Validation)

Khi Agent được gọi bằng lệnh `/feynman-discovery-documentor`, Agent **bắt buộc phải thực hiện bước kiểm tra đầu vào** trước khi chạy:

*   **Điều kiện chạy**: Người dùng phải cung cấp đầy đủ bối cảnh nhiệm vụ tối thiểu gồm:
    1.  Chủ đề cần viết hoặc Nguồn dữ liệu gốc (ví dụ: từ thư mục `advanced-sql`).
    2.  Thư mục đích để xuất bản tài liệu mới (ví dụ: `feynman-drill-sql`).
*   **Hành vi khi thiếu thông tin**: Nếu thông tin đầu vào bị thiếu, trống hoặc quá mơ hồ, Agent **tuyệt đối không được phép chạy** tự ý đoán mò. Agent phải **dừng lại ngay lập tức** và phản hồi bằng cách hiển thị **Khung Prompt mẫu (Meta-Prompt)** dưới đây để yêu cầu người dùng cung cấp đầy đủ bối cảnh:

```markdown
> [!WARNING]
> Bạn đã gọi lệnh `/feynman-discovery-documentor` nhưng chưa cung cấp đầy đủ thông tin bối cảnh (Chủ đề, Thư mục gốc, Thư mục đích). Vui lòng điền và gửi lại yêu cầu theo mẫu sau:

```markdown
Hãy đọc và áp dụng nghiêm ngặt các hướng dẫn vận hành của skill cục bộ sau đây:
- Đường dẫn file: E:\huydq\DailyData\skills\buffer\syde\.agents\skills\feynman-discovery-documentor\SKILL.md

Nhiệm vụ của bạn:
1. Sử dụng skill /feynman-discovery-documentor để biên soạn/tinh chỉnh bộ tài liệu [TÊN BỘ TÀI LIỆU MỚI].
2. Nguồn dữ liệu gốc lấy từ: [ĐƯỜNG DẪN THƯ MỤC GỐC].
3. Thư mục đích lưu tài liệu mới: [ĐƯỜNG DẪN THƯ MỤC ĐÍCH].

Yêu cầu thực thi:
- Quét hiện trạng thư mục để kích hoạt chế độ "Biên biên tập cộng dồn" (Incremental Editing).
- Tuyệt đối tuân thủ quy tắc 2 Pha (Lập khung outline trước, sau đó chèn nội dung chi tiết tối đa 2 tệp mỗi lượt gọi công cụ).
- Đảm bảo đầy đủ các nâng cấp mới của skill: Gắn số đo lường vật lý lên sơ đồ Tầng 3, chèn khối code đối chiếu ORM Before/After cụ thể ở Tầng 4, và lập bảng Nhật ký Self-Grill ở cuối mỗi file.
\```
```

---

## 2. Cấu trúc bắt buộc của một tài liệu FDL (4 Tầng tích hợp)

Mỗi chuyên đề tài liệu kỹ thuật được biên soạn bằng skill này bắt buộc phải đi qua 4 tầng nhận thức theo đúng trình tự sau, nằm chung trong một tệp tin duy nhất:

### ## Tầng 1: Trực giác vật lý (Physical Intuition & Analogy)
*   **Ràng buộc**: Tuyệt đối cấm sử dụng thuật ngữ chuyên môn phức tạp (như B+Tree, Băm, Phân trang).
*   **Nhiệm vụ**: Giải thích bản chất cơ chế bằng một phép so sánh (analogy) cơ học hoặc tình huống đời sống cụ thể. Người học phải hình dung được "mô hình vật lý" trong đầu trước khi viết code.

### ## Tầng 2: Thực nghiệm chủ động (Active Sandbox Experiment)
*   **Ràng buộc**: Bắt buộc phải chèn câu hỏi dự đoán **"Hãy đoán xem..."** trước mỗi đoạn mã thực thi để kích hoạt tư duy giả thuyết của người học.
*   **Đa dạng hóa câu hỏi**: Tránh lặp lại duy nhất một mẫu câu hỏi về số lượng dòng quét/block đĩa. Hãy thay đổi linh hoạt các câu hỏi dự đoán dựa trên bản chất bài học (ví dụ: dự đoán thứ tự dữ liệu trả về, lỗi cú pháp, tính đúng sai logic khi so khớp NULL, hành vi rẽ nhánh của Query Optimizer khi dữ liệu bị lệch phân phối...).
*   **Nhiệm vụ**: Cung cấp đoạn code sandbox tối giản. Yêu cầu người học chạy lệnh và tự đối chiếu kết quả thực tế với giả thuyết ban đầu.

### ## Tầng 3: Mổ xẻ cơ học (Mechanical Breakdown)
*   **Ràng buộc**: Giải thích lý thuyết dựa trên giới hạn vật lý của phần cứng (RAM, Disk, CPU).
*   **Sơ đồ trực quan hóa (Mermaid vs. ASCII/Table)**: 
    *   Đối với các thuật toán hoặc quy trình động (như các bước Hash Join, luồng thực thi), Agent bắt buộc phải thiết kế sơ đồ trực quan bằng cú pháp Mermaid (`mermaid`).
    *   Đối với cấu trúc dữ liệu tĩnh chi tiết (như cấu trúc nút lá B+Tree, phân vùng đĩa), nếu cú pháp Mermaid quá phức tạp làm sơ đồ bị phình to rối mắt, Agent được phép thay thế bằng **sơ đồ ASCII gọn nhẹ** kết hợp với **bảng dữ liệu cấu trúc**.
    *   **Quy tắc gắn số thực chứng (Number Overlay)**: Trên các sơ đồ Mermaid hoặc ASCII, bắt buộc phải đính kèm các con số đo lường vật lý tương đối hoặc cụ thể lấy từ thực nghiệm ở Tầng 2 (Ví dụ: gắn nhãn `[Đọc 100.000 dòng / tốn 15ms]` vào luồng Seq Scan, và nhãn `[Đọc 3 block đĩa / dưới 0.2ms]` vào luồng Index Scan) để hình ảnh hóa sự chênh lệch hiệu năng vật lý một cách trực quan nhất.
*   **Nhiệm vụ**: Giải thích tại sao hiện tượng ở Tầng 2 lại xảy ra. Liên kết trực tiếp lý thuyết với các con số quan sát được.
*   **Bổ sung tri thức**: Nếu tài liệu gốc nông cạn, Agent **bắt buộc** phải sử dụng tri thức pre-trained sâu sắc của mình về hệ quản trị cơ sở dữ liệu để tự bổ sung các thông số kỹ thuật thực tế.

### ## Tầng 4: Nghịch phá & Thử thách cực hạn (Stress Test & Play)
*   **Ràng buộc**: Phải kích thích tư duy độc lập và hành vi phá vỡ giới hạn.
*   **Khối code đối chiếu ORM (Before/After ORM Code)**: Bắt buộc phải chèn một khối mã đối chiếu dạng `// BAD (Code ORM gây Seq Scan / lỗi hiệu năng)` và `// GOOD (Code ORM đã tối ưu hóa)` sử dụng cú pháp của các thư viện phổ biến (như Prisma, Hibernate, Sequelize, TypeORM...) để lập trình viên có thể copy-paste sửa lỗi ngay trong code ứng dụng của họ.
*   **Nhiệm vụ**: Đưa ra các thử thách bắt người học tự tìm cách bẻ gãy lý thuyết, ép database đi theo các kế hoạch chạy tồi tệ hoặc tối ưu hóa cực hạn.

---

## 3. Quản lý trạng thái và Khả năng tái sử dụng (State & Resumability)

Khi được gọi vào một thư mục tài liệu đang phát triển dở dang, Agent bắt buộc phải thực hiện các bước phát hiện bối cảnh để tiếp tục công việc thay vì viết lại từ đầu:

### Bước 1: Khảo sát hiện trạng thư mục (Context Discovery)
*   Quét cấu trúc thư mục hiện tại để tìm tệp tin điều hướng chính (`README.md`) và tệp theo dõi nhiệm vụ (`task.md`).
*   Đọc `README.md` để xác định danh sách các chuyên đề/bài học và trạng thái hoàn thành của chúng.
*   Đọc `task.md` để biết nhiệm vụ nào đang làm dở (`[/]`), nhiệm vụ nào chưa bắt đầu (`[ ]`).

### Bước 2: Biên biên tập cộng dồn (Incremental Editing Mode)
*   Khi cần chỉnh sửa một tệp tin FDL đã tồn tại, Agent **không được phép ghi đè hoàn toàn** tệp tin (trừ khi tệp tin đó trống hoặc được yêu cầu rõ ràng).
*   Agent phải sử dụng công cụ sửa đổi tệp tin theo dòng (`replace_file_content`) để cập nhật hoặc sửa chữa riêng lẻ từng Tầng nhằm bảo toàn phần nội dung tốt đã có của các Tầng khác.

### Bước 3: Cập nhật nhật ký tiến độ (Progress Anchoring)
*   Sau mỗi lần tạo mới hoặc tinh chỉnh thành công một chuyên đề, Agent bắt buộc phải cập nhật ký hiệu trạng thái trong `README.md` và `task.md`.

---

## 4. Quy trình sinh tài liệu chống thiên kiến nén (Compression Bias Prevention)

Khi nhận yêu cầu tạo mới hoặc tinh chỉnh hàng loạt nhiều file, Agent **không được phép** ghi hàng loạt tất cả các file cùng lúc trong một lượt gọi công cụ. Quy trình bắt buộc phải là:

*   **Pha 1 (Lập khung/Outline)**: Chỉ sinh ra cấu trúc thư mục và các tệp tin chứa tiêu đề khung rỗng (nếu tạo mới).
*   **Pha 2 (Mở rộng sâu từng tệp)**: Thực hiện đọc tài liệu gốc và viết chi tiết cho **từng tệp một** hoặc theo từng cụm tối đa 2 tệp trong mỗi lượt gọi công cụ.

---

## 5. Xác minh tự phản biện bắt buộc (Feynman Verification Log)

Để tránh lỗi AI tự thỏa hiệp và viết sáo rỗng (tự lừa dối), Agent **bắt buộc phải chèn một phần mục lục ẩn hoặc một bảng nhỏ ở cuối mỗi file tài liệu** được tạo ra/chỉnh sửa để ghi lại nhật ký tự kiểm định chất lượng:

```markdown
### Xác minh chất lượng (Feynman Self-Grill Log)
1. **Trực giác vật lý**: [Tên phép so sánh đời thường được dùng thay cho thuật ngữ chuyên môn ở Tầng 1]
2. **Giới hạn phép so sánh**: [Nêu rõ điểm mà phép so sánh trên bắt đầu không còn chính xác về mặt vật lý]
3. **Nguồn gốc thực chứng**: [Tên hệ cơ sở dữ liệu và môi trường sandbox dùng để lấy dữ liệu con số thực tế ở Tầng 2]
```

---

## 6. Bảng đối chiếu Chất lượng viết (Bad vs. Good Comparison)

| Khái niệm cần viết | Cách viết sáo rỗng, nông cạn (Cargo Cult) | Cách viết FDL thấu hiểu thực chất (Feynman style) |
| :--- | :--- | :--- |
| **B+Tree** | "B+Tree là một cây tự cân bằng giúp tối ưu hóa truy vấn tìm kiếm với độ phức tạp thời gian là O(log n)." | "Đĩa cứng đọc dữ liệu theo từng trang 8KB cố định. Cây nhị phân thông thường quá cao (~27 tầng) bắt đầu đọc đĩa phải nhảy ngẫu nhiên liên tục làm treo máy. B+Tree nhét đầy hàng trăm khóa dẫn đường vào trang 8KB nên cây cực lùn (3 tầng), chỉ cần nhảy đĩa 2 lần để tìm ra khóa trong 125 triệu dòng." |
| **Composite Index** | "Chỉ mục kép gồm nhiều cột và hoạt động theo quy tắc tiền tố bên trái (Leftmost Prefix)." | "Giống như cuốn danh bạ sắp xếp Họ trước, Tên sau. Nếu bạn chỉ biết Tên mà không biết Họ, cuốn danh bạ trở nên vô dụng, bạn bắt buộc phải quét từng trang từ đầu đến cuối vì các Tên giống nhau nằm rải rác khắp nơi." |

---

## 7. Văn văn phong & Giọng điệu (Feynman Tone Guidelines)
*   Dùng ngôi xưng **"Tôi"** (người hướng dẫn) và **"Bạn"** hoặc **"Chúng ta"** (người cùng thực nghiệm).
*   Sử dụng câu ngắn, từ ngữ khẩu ngữ mang tính hành động (như "nghịch thử", "chạy bộ", "xé trang", "treo hệ thống") thay vì các từ Hán Việt trang trọng ("nghiên cứu", "phân tích", "kết quả không chính xác").
*   Khi kết thúc một phần giải thích, định hình bằng câu khẳng định ngắn gọn: *"Thế thôi."*, *"Mọi chuyện chỉ có vậy."*, *"Nó vận hành thế đấy."*.
