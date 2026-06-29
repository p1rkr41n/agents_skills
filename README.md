# Thư viện Kỹ năng cho Developer Agent

Kho lưu trữ này chứa bộ sưu tập các kỹ năng tùy biến (custom skills), quy tắc hành vi và chỉ dẫn phong cách chuyên sâu cho trợ lý lập trình AI (như Antigravity IDE). Các kỹ năng này giúp Agent thực hiện các tác vụ nghiên cứu kiến trúc hệ thống, phân tích điểm nghẽn hiệu năng vật lý và viết tài liệu kỹ thuật có độ sâu.

---

## Cấu trúc Kho lưu trữ

### 📁 `feynman-documentor/`
Thư mục chứa các kỹ năng và quy chuẩn tư duy dựa trên phương pháp học tập thực chứng và phong cách sư phạm trực quan của nhà vật lý đoạt giải Nobel Richard Feynman.

*   **[`core-engine-detector`](feynman-documentor/skills/core-engine-detector/SKILL.md)**: Kỹ năng tự động quét mã nguồn lạ để cô lập và định vị **Core Engine Nguyên thủy** (thuật toán/cấu trúc dữ liệu nền tảng) đối chiếu với **Core Engine Tùy biến** (các kỹ thuật tối ưu hóa cụ thể), đồng thời phân tích các giới hạn vật lý phần cứng (Disk I/O, RAM, Thread locks).
*   **[`feynman-discovery-documentor`](feynman-discovery-documentor/skills/feynman-discovery-documentor/SKILL.md)**: Kỹ năng biên soạn tài liệu học tập kỹ thuật theo cấu trúc **Vòng lặp Khám phá Feynman (FDL) 4 tầng tích hợp** (Trực giác vật lý, Thực nghiệm sandbox chủ động, Mổ xẻ cơ học phần cứng kèm sơ đồ đính số thực chứng, và Thử thách stress test kèm khối code đối chiếu ORM/API Before/After).
*   **[`feynman-perspective`](feynman-documentor/skills/feynman-perspective/SKILL.md)**: Chỉ dẫn phong cách hành văn và tư duy phản biện Richard Feynman (ưu tiên thực chứng hơn thuật ngữ sáo rỗng).

### 📁 `diataxis/`
Thư mục chứa các kỹ năng biên soạn tài liệu kỹ thuật dựa trên mô hình định hướng tài liệu tiêu chuẩn Diátaxis.

*   **[`tal-documentor`](diataxis/tal-documentor/SKILL.md)**: Kỹ năng và chỉ dẫn viết tài liệu kỹ thuật theo tiêu chuẩn phân tách Diátaxis (Tutorials, How-to Guides, Reference, Explanation).

---

## Cách cài đặt và sử dụng

1.  **Clone kho lưu trữ này về máy**:
    ```bash
    git clone https://github.com/p1rkr41n/agents_skills.git
    ```
2.  **Đăng ký các kỹ năng**:
    *   Sao chép các thư mục kỹ năng mong muốn từ `feynman-documentor/skills/` hoặc `diataxis/` vào thư mục tùy biến của IDE của bạn (ví dụ: `.agents/skills/` trong workspace hiện tại, hoặc `.gemini/config/skills/` trên phạm vi toàn cục).
    *   Các Agent IDE sẽ tự động phát hiện và tải lên các kỹ năng dựa trên tên của chúng.
3.  **Kích hoạt kỹ năng**:
    *   Sử dụng trực tiếp các slash commands tương ứng (ví dụ: `/core-engine-detector`, `/feynman-discovery-documentor` hoặc `/tal-documentor`) trong khung chat của Agent để bắt đầu chạy quy trình.
