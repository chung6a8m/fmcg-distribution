# Agent / Codex instructions — Canonical FMCG Business

## Vai trò và giới hạn repository

Repository `chung6a8m/fmcg-distribution` là **nguồn chuẩn của Business Baseline**, độc lập với công nghệ. Không dùng repository này làm nơi triển khai ứng dụng hoặc quản lý delivery.

- **Baseline hiện hành:** `BUSINESS-v1.0`, `BUSINESS_V1_FROZEN_FOR_IMPLEMENTATION` ở mức **DOC/MODEL**; xem [BASELINE-v1.0.md](BASELINE-v1.0.md).
- **Snapshot cố định:** commit `88d70b3be72f34011b49b0de265ad2c43202492f`, Git tree `business/` = `c9a4164a99ea57e1d5f9bc8711285c6d3705f8e3`.
- **Không tạo ở đây:** `src/`, `tests/` ứng dụng, `delivery/`, thiết kế/cấu hình tech stack, cơ sở hạ tầng, ứng dụng chạy thử hoặc roadmap implementation.
- **Không diễn giải lại v1.0:** nhãn `candidate` trong file thuộc lịch sử biên soạn. Freeze để làm đầu vào không phải kiểm chứng E2E, duyệt pháp lý/provider hoặc Tenant Go-Live.

## Khi đọc hợp đồng nghiệp vụ

1. Bắt đầu từ [business/README.md](business/README.md), [business/scope.md](business/scope.md), rồi đọc đúng BR/POL/SOP/AC liên quan.
2. Dùng [business/calculations.md](business/calculations.md), [business/acceptance.md](business/acceptance.md) và [business/reference-data/](business/reference-data/) làm expected độc lập với implementation.
3. [business/provenance.md](business/provenance.md) chỉ để tra cứu lịch sử; không yêu cầu mở repo nghiên cứu để hiểu hành vi v1.0.
4. Khi cần code, làm việc ở **repository ứng dụng khác** có snapshot của baseline được ghim bằng source commit và business tree SHA. Không tạo phụ thuộc Git submodule hoặc đồng bộ tự động nếu chưa được Owner chọn.

## Thay đổi nghiệp vụ có kiểm soát

- **V1.0 bất biến:** không sửa `business/**` của snapshot v1.0 chỉ để khiến tests hoặc code PASS.
- Mọi đề xuất thay đổi ngữ nghĩa cần chỉ rõ ID D/PADR/EVQ/BR/POL/SOP/AC, nội dung trước/sau, lý do, impact lên scenario/golden results và quyết định Owner.
- Thay đổi có hiệu lực phải có version baseline mới, được review/acceptance riêng. Không mặc định thay đổi canonical sẽ tự áp vào các implementation.
- Chỉ sửa các file ngoài `business/` để làm rõ chỉ dẫn/manifest nếu không thay đổi nghĩa và vẫn giữ snapshot đã freeze.
- Không tự merge PR, giả lập approval, ký chuyên môn, nâng `MODEL_ONLY` thành `VERIFIED`, mở mode/security gate hay sửa repository nghiên cứu.

## Kiểm tra và chất lượng

- Chạy `python3 tools/validate_business.py` cho mọi PR thay đổi tài liệu; CI hiện tại **chỉ** là kiểm tra DOC/MODEL.
- Kiểm tra Git tree `business/` vẫn khớp snapshot khi chỉ sửa tài liệu quản trị tại root.
- Giữ tiếng Việt, ID ổn định, UTF-8/LF, link tương đối, số liệu mẫu gắn `SYNTHETIC`.
- Không suy VAT, threshold, SLO, seller/provider hay bằng chứng production từ fixture; P0 G-STOCK/G-CUT/G-IDEMP/G-LEDGER/G-INV không được miễn trừ khi Go-Live.
