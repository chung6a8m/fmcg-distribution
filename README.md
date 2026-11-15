# FMCG Distribution — Canonical Business Baseline

**Vai trò repository:** nguồn chuẩn độc lập công nghệ (**canonical business contract**) cho sản phẩm DMS phân phối hàng tiêu dùng tại Việt Nam. Repository này lưu yêu cầu, thuật ngữ, quy trình, quy tắc, công thức, dữ liệu mẫu và expected results; **không phải repository triển khai ứng dụng**.

## Trạng thái hiện tại

- **Business Baseline:** `BUSINESS-v1.0` — `BUSINESS_V1_FROZEN_FOR_IMPLEMENTATION` ở cấp **DOC/MODEL**.
- **Commit được đóng băng:** [`88d70b3be72f34011b49b0de265ad2c43202492f`](https://github.com/chung6a8m/fmcg-distribution/commit/88d70b3be72f34011b49b0de265ad2c43202492f).
- **Git tree của `business/`:** `c9a4164a99ea57e1d5f9bc8711285c6d3705f8e3` (25 file).
- **Manifest và giới hạn phê duyệt:** [BASELINE-v1.0.md](BASELINE-v1.0.md).
- Hai PR [B01 #1](https://github.com/chung6a8m/fmcg-distribution/pull/1) và [B02 #2](https://github.com/chung6a8m/fmcg-distribution/pull/2) đã merge. Công thức, 21 AC, golden data và validator **đã có trong baseline**; không còn là hạng mục của PR tương lai.

Các nhãn `candidate` hoặc `NOT_RUN` trong `business/**` là trạng thái tại thời điểm biên soạn hoặc tình trạng kiểm thử ứng dụng; **không phủ định việc snapshot v1.0 đã được freeze để làm đầu vào triển khai**. Freeze chỉ chứng minh cấp tài liệu/model, **không** phải Product Verification, kiểm chứng pháp lý/provider hay Tenant Go-Live.

## Đọc và sử dụng baseline

1. [Phạm vi MVP](business/scope.md), [thuật ngữ](business/glossary.md), [mô hình miền](business/domain-model.md).
2. [Business Rules](business/business-rules.md), [chính sách](business/policies.md) và [workflows](business/workflows/).
3. [Công thức](business/calculations.md), [21 tiêu chí nghiệm thu](business/acceptance.md) và [golden oracles](business/reference-data/README.md).
4. [Hướng dẫn kiểm chứng](business/validation-guide.md), [provenance](business/provenance.md) và [AGENTS.md](AGENTS.md).

Kiểm tra tài liệu/model: `python3 tools/validate_business.py`. GitHub Actions `business-contract` chỉ xác nhận tài liệu, JSON và các bất biến số mẫu; không chạy hoặc nghiệm thu ứng dụng.

## Ranh giới với các implementation

- **Tại repository này:** quản lý canonical business, version, thay đổi quy tắc và golden expected. Không thêm `src/`, `tests/` ứng dụng, `delivery/`, lựa chọn tech stack hoặc roadmap triển khai.
- **Tại repository ứng dụng riêng:** đưa vào một **snapshot đầy đủ** của `business/` và golden data, ghi `baselineId` + source commit + tree SHA. Có thể build/test/làm việc hằng ngày mà không cần checkout repository canonical.
- **Hướng truyền thay đổi:** canonical → implementation **theo lần nâng baseline được lựa chọn**, không tự đồng bộ hai chiều. Code hoặc test của một stack không được tự sửa expected của canonical.
- **Nhiều implementation:** có thể khởi tạo độc lập từ cùng một snapshot/version; thay stack không tự thay đổi nghiệp vụ.

## Thay đổi sau freeze

1. Phân biệt lỗi implementation với việc cần thay đổi nghiệp vụ. Vấn đề thuần kỹ thuật xử lý tại repo ứng dụng.
2. Nếu thay đổi nghĩa của BR/POL/SOP/AC/công thức/golden oracle: lập PR tại đây, nêu ID liên quan, trước/sau, lý do, ảnh hưởng scenario/expected và quyết định Owner. Không chỉnh ngầm snapshot `BUSINESS-v1.0`.
3. Chỉ công bố version baseline mới sau khi review/acceptance đúng phạm vi; giữ bản v1.0 truy xuất được bằng commit/tree cố định. Repository ứng dụng tự quyết định thời điểm nâng và chạy regression.
4. Không tự nâng `MODEL_ONLY`/`NOT_RUN` thành `VERIFIED`; các P0 và mode gates vẫn bắt buộc trước vận hành thực tế.

Repository nghiên cứu lịch sử (chỉ dùng khi cần đối chiếu xuất xứ, **không phải phụ thuộc khi đọc hoặc sử dụng v1.0**): https://github.com/chung6a8m/research-sme-phan-phoi-hang-tieu-dung
