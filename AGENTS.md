# Agent / Codex instructions — FMCG Distribution


**Baseline đang sử dụng:** xem [BASELINE-v1.0.md](BASELINE-v1.0.md) và tham chiếu commit cố định cho business v1.0; không coi nhãn candidate thời điểm biên soạn B01/B02 là bản chưa thể dùng để phát triển. Freeze thuộc DOC/MODEL, không đồng nghĩa Product Verification/Go-Live.
Mục tiêu: hỗ trợ **solo developer** xây sản phẩm bằng vertical slices theo đặc tả nghiệp vụ, không tạo thêm tầng quy trình/hạ tầng khi chưa cần.

## Quy tắc đọc

1. Đọc business/README.md, business/scope.md và nhóm quy tắc, luồng liên quan tới yêu cầu hiện tại.
2. Khi triển khai, đọc business/calculations.md, business/acceptance.md và golden data nếu các file đã tồn tại; nếu chưa thì ghi thiếu rõ ràng.
3. Các link nguồn ở business/provenance.md chỉ phục vụ truy xuất lịch sử; tuyệt đối không yêu cầu người thực hiện mở lại R001–R010 để hiểu behavior thông thường.
4. Ưu tiên phạm vi A Online trước, sau đó B_ONLINE và Mixed; chỉ mở offline/mode production khi đạt gate tương ứng.

## Quyền thay đổi

- business/ là **normative business contract** khi được Owner chấp nhận. Không sửa quy tắc chỉ để khiến code/test PASS.
- Mọi thay đổi ngữ nghĩa cần nêu ID quy tắc liên quan, trước/sau, lý do, ảnh hưởng oracle và yêu cầu Owner review.
- Trạng thái quyết định nguồn phải giữ nguyên; không tự nâng DRAFT thành APPROVED, MODEL_ONLY thành VERIFIED hoặc cấp Go-Live.
- Không tự chọn tech stack, kiến trúc, nhà cung cấp, môi trường production hoặc tự mở security gate khi chưa có lựa chọn rõ ràng.
- Không tự merge PR, tạo approval, ký chuyên môn hoặc thay đổi repository nghiên cứu.

## Workflow gọn

Business rule → scenario/expected → đề xuất implementation → code/test → PR/evidence. Mỗi vertical slice ghi: scope, ID quy tắc, acceptance, negative cases, kết quả actual/expected, pending. Bất cứ thứ gì chưa chạy trên hệ thật phải được gọi đúng tên **NOT_RUN/MODEL_ONLY**.

## Thuật ngữ quan trọng

Một người bán/tenant; Customer chịu công nợ, Outlet tùy chọn, ShipTo chụp theo chứng từ; chuyển kho→xe không phải bán; A giữ hàng riêng B quota; công nợ Customer, tiền nhân viên giữ hộ, tạm ứng là ba sổ khác nhau. P0 của stock/cutover/idempotency/ledger/invoice không được miễn trừ để Go-Live.

## Chất lượng tài liệu

Tài liệu bằng tiếng Việt; ID ổn định (D-xx, PADR-xx, EVQ-xx, BR-xx, POL-xx, SOP-xx, AC-xx). Số liệu giả lập ghi rõ SYNTHETIC. Dùng đường dẫn nội bộ tương đối; UTF-8/LF; sửa tối thiểu, không tạo nhiều file rỗng. Không đặt giá trị VAT/tỷ lệ thị trường/độ trễ/SLO giả định thành mặc định áp dụng thực.
