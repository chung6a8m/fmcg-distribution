# FMCG Distribution — Business-first


**Business Baseline v1.0 (tài liệu, cố định theo commit):** [BASELINE-v1.0.md](BASELINE-v1.0.md). Business v1.0 được freeze để dùng làm đầu vào implementation, không phải Product Verification hoặc Tenant Go-Live.

**Một nơi làm việc cho solo developer:** đặc tả nghiệp vụ là nguồn yêu cầu; công nghệ, kiến trúc và mã nguồn chỉ được bổ sung khi bắt đầu triển khai.

## Bắt đầu từ đâu?

1. [Bộ Business Specification](business/README.md) — phạm vi, thuật ngữ, dữ liệu, quy trình, quy tắc và ràng buộc.
2. [Phạm vi MVP](business/scope.md) — A, B_ONLINE và Mixed A+B_ONLINE.
3. [Quy tắc nghiệp vụ](business/business-rules.md) và [quy trình](business/workflows/) — nền tảng cho vertical slices.
4. [Nguồn gốc và mức độ chấp nhận](business/provenance.md) — cách bảo toàn quyết định được phê duyệt.
5. [AGENTS.md](AGENTS.md) — cách Codex/AI làm việc với baseline.

**Trạng thái repository:** đang biên tập **Business Baseline v1 candidate**, chưa phê duyệt bản diễn giải mới; chưa có tech stack, source ứng dụng hay bằng chứng kiểm thử ứng dụng. B02 bổ sung [công thức](business/calculations.md), [21 ca nghiệm thu](business/acceptance.md) và [golden data](business/reference-data/README.md) trong PR kế tiếp.

## Nguyên tắc

- **Business-first, technology-neutral:** mô tả cái gì phải đúng trước khi chọn cách xây.
- **Một nguồn sử dụng hằng ngày:** không cần mở repository nghiên cứu để hiểu nghiệp vụ trong phạm vi v1; provenance chỉ để truy xuất.
- **Không tự nâng trạng thái:** Owner policy approved trong nguồn không có nghĩa application verified hoặc tenant go-live.
- **Chuyển đổi kiểm soát:** khi có thay đổi nghiệp vụ, thay đổi business docs và golden oracles trước hoặc cùng với code, có review riêng.
- **Công nghệ có thể thay:** cùng bộ business behavior/expected results áp dụng được cho các cách triển khai khác nhau.

Kho lịch sử (không phải phụ thuộc khi đọc tài liệu): https://github.com/chung6a8m/research-sme-phan-phoi-hang-tieu-dung
