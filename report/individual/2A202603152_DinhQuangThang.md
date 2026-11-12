# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202603152
- Ngày / CVAT local: 11/11/2026
- Công cụ đã dùng: CVAT local (Brush/Polygon + Export job dataset)

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | cp1_holes.zip | 1 / 1 | 3 |
| cp2_slice | cp2_slice.zip | 1 / 1 | 3 |
| cp5_occlusion | cp5_occlusion.zip | 1 / 1 | 3 |
| cp3_thin | cp3_thin.zip | 1 / 1 | 3 |
| cp4_curb | cp4_curb.zip | 1 / 1 | 3 |
| cp6_coverage | cp6_coverage.zip | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `hard_panoptic`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Panoptic đầu tiên tự vẽ: hard_panoptic / `000000350023.jpg`, vật ở phía giữa bên trái của ảnh; tôi vẽ một `car` đầu tiên.
- Class và quy tắc dùng để chọn biên: `bus`; chỉ vẽ phần thân xe thật sự nhìn thấy, dừng ở mép đen/bóng và mặt đường, không mở rộng lên phần bị che hay nền không thuộc xe.
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: KHÔNG DÙNG.
- Nếu không dùng gợi ý: ghi “không dùng”; vẫn giải thích một quyết định gán nhãn của mình. 
=> Giải thích: Giữ `car` thay vì `bus`/`truck` vì hình dạng, chiều dài và vị trí của nó phù hợp hơn với một xe nhỏ; ranh của toàn bộ khối xe là rõ nhất trên nền đường, nên không kéo mask sang phần sidewalk hoặc phần bóng lớn để tránh gộp sai class.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: easy_semantic / `81ae7cbb-6bc63a4a.jpg` / ranh giữa `sidewalk` và `building` ở phía phải của ảnh, gần mép cạnh đường.
- Lỗi thuộc loại: biên.
- Bằng chứng tôi nhìn thấy: phần ranh giữa `sidewalk` và tường không trùng với mép vật thể; vùng sát tường có màu/độ sáng trong giống như `building` nhưng thực ra vẫn là `sidewalk`. Vì vậy, nếu kéo mask quá sát tường, sẽ đè vào nền/nhà và mất vùng `sidewalk`.
- Quy tắc và hành động sửa: Áp dụng quy tắc theo chức năng/bó vỉa hè: phần vỉa hè phải theo không gian đi bộ, còn `building` là phần tòa nhà. Dùng brush nhỏ để thu hẹp/đẩy lại biên theo cạnh chức năng, rồi Save và export lại ZIP.
- Sau sửa đã Save và export:
-> ĐÃ Save và export tất cả các ZIP bao gồm: `easy_semantic.zip`, `medium_instance.zip`, và `hard_panoptic.zip`. Và cả các task checkpoint cũng đã được Save và export ZIP về máy.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): 
=> Đã chạy `python scripts/inspect_submissions.py --dir submissions`; kết quả là `easy_semantic`, `medium_instance`, `hard_panoptic` đều `OK`. 
Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1 | easy_semantic / `7ee6d192-89e2408b.jpg`, ranh road–sidewalk ở góc phải | Có thể xem toàn bộ phần gạch bằng là road, hoặc chia theo vỉa hẻ và mặt đường | Quy tắc bó vỉa hè: Giữ đường ranh theo chức năng đi bộ/đi xe, không chỉ theo màu.|
| 2 | medium_instance / `000000373353.jpg`, hai vật cố gần nhau ở giữa ảnh | Có thể là một object lớn hoặc hai instance riêng | Xem khoảng cách, bóng và hình dáng; nếu khoảng trắng/cảnh vật tách rõ thì giữ hai instance. Quyết định tách khi có ranh riêng rõ và không gộp các thân vật thành một mask. |
| 3 | hard_panoptic / `000000350023.jpg`, vật ở cuối đường có che lấp phần thân | Có thể đoán phần ẩn là một object mới, hoặc giữ một instance duy nhất theo phần nhìn thấy | Quy tắc task: chỉ vẽ phần nhìn thấy; không tự đoán biên sau vật che.|

