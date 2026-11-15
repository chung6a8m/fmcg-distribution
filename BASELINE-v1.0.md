# Business Baseline v1.0 — bản đóng băng tài liệu nghiệp vụ

**Baseline ID:** `BUSINESS-v1.0` · **Ngày ghi nhận:** 15/11/2026 (theo ngày yêu cầu của Owner) · **Phạm vi:** đặc tả nghiệp vụ, tính toán và dữ liệu mẫu, *không bao gồm tech stack*.

## 1. Snapshot bất biến — nguồn sử dụng cho triển khai

- **Commit được chọn làm baseline:** [`88d70b3be72f34011b49b0de265ad2c43202492f`](https://github.com/chung6a8m/fmcg-distribution/commit/88d70b3be72f34011b49b0de265ad2c43202492f).
- **Git tree của thư mục `business/` ở commit trên:** `c9a4164a99ea57e1d5f9bc8711285c6d3705f8e3`. Toàn bộ 25 file của `business/` thuộc snapshot này; hồ sơ meta này nằm *ngoài* thư mục để không thay đổi snapshot khi ghi nhận freeze.
- **Hai PR đã merge, theo thứ tự:** [B01 #1](https://github.com/chung6a8m/fmcg-distribution/pull/1) → [B02 #2](https://github.com/chung6a8m/fmcg-distribution/pull/2).
- **Kiểm tra tại merged main:** [GitHub Actions DOC/MODEL SUCCESS](https://github.com/chung6a8m/fmcg-distribution/actions/runs/43680999677), exact commit `88d70b3be72f34011b49b0de265ad2c43202492f`.
- **Nguồn chính sách lịch sử:** [Product Contract C′ `eb9c4b04`](https://github.com/chung6a8m/research-sme-phan-phoi-hang-tieu-dung/commit/eb9c4b04e334530367b80ea4178edb4dd4a07491), Owner Acceptance tại PR #2 ở phạm vi **PRODUCT_POLICY_AND_CONTRACT_ONLY**.

**Cách truy cập phiên bản cố định:** các link tới `business/**` tại commit `88d70b3be72f34011b49b0de265ad2c43202492f`, không dựa vào `main` sau này. Nếu `main` phát triển tiếp, v1.0 vẫn trỏ đúng snapshot này.

## 2. Kết quả review theo ủy quyền của Owner

Người dùng đã yêu cầu thực hiện chuỗi **review B01 → merge → retarget/review B02 → merge → chốt Business Baseline v1.0** trong hội thoại ngày 15/11/2026. Trợ lý đã thực hiện review và lưu [disposition B01](https://github.com/chung6a8m/fmcg-distribution/pull/1#issuecomment-6889714469) cùng [disposition B02](https://github.com/chung6a8m/fmcg-distribution/pull/2#issuecomment-6889725309). Không có P0/P1 tài liệu còn mở được xác định trong phạm vi review này.

**Trạng thái:** `BUSINESS_V1_FROZEN_FOR_IMPLEMENTATION` ở cấp **DOC/MODEL**; đây là freeze do Owner yêu cầu thực hiện qua trợ lý, **không phải bằng chứng Owner đã đọc/ký riêng từng file hoặc có đánh giá độc lập của sáu chuyên gia**. Các nhãn `candidate` trong chính file `business/**` là dấu trạng thái khi biên soạn B01/B02; record v1.0 này chốt snapshot để triển khai. Mọi đề xuất thay đổi ngữ nghĩa về sau cần được Owner xem xét riêng.

**Không được suy:** `BUSINESS_V1_FROZEN_FOR_IMPLEMENTATION` ⇒ `PRODUCT_VERIFIED` ⇒ `TENANT_GO_LIVE_ACCEPTED`. Hai cổng cuối vẫn độc lập và cần test/evidence thực, duyệt theo mode.

## 3. Hợp đồng v1.0 bao gồm

- **Product scope & constraints:** A, B_ONLINE và Mixed A+B_ONLINE; Customer có 0..n Outlet; ShipTo snapshot; một người bán/tenant; nhu cầu người dùng và ranh giới nghiệp vụ.
- **Decision/policy:** D-01..15, PADR-01..09, EVQ-01..07, BR-01..24, POL-01..24, 10 approval classes, maker-checker.
- **SOP:** SOP-01..12 bao gồm A/B/Mixed, hàng–tiền–nợ, returns, invoice/accounting, quyền/offline/recovery, cutover và visit không đơn.
- **Calculations:** UoM, tồn/kho, bình quân di động SKU×location, quà ròng/waiver, pricing/rounding/VAT giả lập, due dates, ba sổ và credit/grant.
- **Reference scenarios & expected:** 21 AC, seed giả lập, 4 golden oracle nguồn AC-03/19/20/21 giữ nguyên, thêm oracle AC-06/07/08/09; F-01..10 negative scenarios.
- **Traceability & independent validation:** script DOC/MODEL standard library; không chọn application runtime, database, framework, UI, cloud hay provider.

## 4. Giới hạn phải bảo toàn trong delivery

- Tất cả những gì đã chạy là **synthetic/data/model/docs validation**. Các AC còn **NOT_RUN** trên application; EV-01..15 real evidence pending hoặc MODEL_ONLY real pending.
- **P0 không miễn:** G-STOCK, G-CUT, G-IDEMP, G-LEDGER, G-INV. B_NO_CHANNEL **BLOCKED**; offline write và production cutover chưa được admitted.
- Quyết định **database-per-tenant và PWA** trước đây là bối cảnh kỹ thuật lịch sử cần đối chiếu nếu đề xuất stack khác; freeze business **không tự hủy** quyết định cũ.
- VAT, profile seller/provider, chứng cứ pháp lý, threshold/SLO, pilot NPP thực không được suy từ dữ liệu giả lập.
- Các hồ sơ phê duyệt Product Verification và Tenant Go-Live phải được tạo riêng khi có hệ thống và bằng chứng thật.

## 5. Quy tắc phát triển sau freeze

1. Khi bắt đầu VS-01 **tại repository ứng dụng độc lập**, Codex dùng **snapshot v1.0** này để suy business acceptance. Các thư mục `delivery/`, `src/`, `tests/` và quyết định tech stack chỉ được tạo tại repository ứng dụng, **không** tại repository canonical này.
2. Thay đổi câu chữ không ảnh hưởng ngữ nghĩa có thể là docs patch; thay đổi BR/SOP/AC/expected phải có change record và version mới, không sửa ngầm golden v1.0.
3. Golden oracle ở v1.0 là nguồn expected độc lập; không lấy kết quả code làm chuẩn để thay lại test.
4. Có thể tạo Git tag `business-v1.0.0` trỏ trực tiếp `88d70b3be72f34011b49b0de265ad2c43202492f` bằng Git sau khi đối chiếu; **hồ sơ này không tuyên bố tag đã tồn tại**.
