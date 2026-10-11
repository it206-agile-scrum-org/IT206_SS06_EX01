# Bài làm: Acceptance Criteria & Definition of Done (Mượn sách trực tuyến)

**Các giả định (mỗi giả định đều có câu hỏi làm rõ tương ứng bên dưới):**
- Giả định 1: Thời gian giữ chỗ là 48 giờ, tính từ lúc đặt mượn thành công (Story 1) hoặc từ lúc độc giả nhận thông báo (Story 2).
- Giả định 2: Tối đa 5 cuốn/độc giả, tính cả sách đang mượn và sách đang được giữ chỗ chưa nhận.
- Giả định 3: Khi sách đang hết, độc giả được vào danh sách đặt trước theo thứ tự đặt (ai đặt trước nhận trước).
- Giả định 4: Thông báo được gửi qua email và trong ứng dụng, trong vòng 5 phút kể từ khi sách có sẵn.

## 1. Bảng Acceptance Criteria

| Story | AC# | Loại | Given | When | Then |
|---|---|---|---|---|---|
| 1 | 1.1 | Happy | Độc giả đã đăng nhập, đang mượn/giữ 2 cuốn, và cuốn "Đắc nhân tâm" còn 1 bản có sẵn | Độc giả bấm "Đặt mượn" cuốn đó | Hiển thị "Đặt mượn thành công, sách được giữ đến [ngày giờ sau 48 giờ]" **And** số bản có sẵn của cuốn đó giảm từ 1 về 0 **And** cuốn sách xuất hiện trong mục "Sách đang giữ chỗ" của độc giả |
| 1 | 1.2 | Negative | Cuốn "Đắc nhân tâm" có 0 bản có sẵn | Độc giả bấm "Đặt mượn" cuốn đó | Hiển thị "Sách hiện đã hết, bạn có thể đặt trước" **And** không có đặt mượn nào được tạo cho độc giả |
| 1 | 1.3 | Edge (đặt đồng thời) | Cuốn "Đắc nhân tâm" còn đúng 1 bản, độc giả A vừa đặt thành công bản cuối cùng | Độc giả B bấm "Đặt mượn" cuốn đó ngay sau A | Độc giả B nhận thông báo "Sách hiện đã hết" **And** chỉ độc giả A có cuốn sách trong mục "Sách đang giữ chỗ" |
| 1 | 1.4 | Edge (giá trị biên 48 giờ) | Độc giả đặt mượn thành công lúc 10:00 thứ Hai và chưa đến nhận sách | Đồng hồ chạm 10:00 thứ Tư (đủ 48 giờ) | Trạng thái đặt mượn chuyển thành "Hết hạn giữ chỗ" **And** sách trở lại trạng thái có sẵn **And** độc giả nhận thông báo giữ chỗ đã hết hạn |
| 2 | 2.1 | Happy | Độc giả A đứng đầu danh sách đặt trước cuốn "Dế Mèn phiêu lưu ký" | Thủ thư xác nhận đã nhận lại cuốn sách đó từ người mượn trước | Trong vòng 5 phút, A nhận thông báo "Sách đã có sẵn, được giữ đến [ngày giờ sau 48 giờ]" **And** cuốn sách được giữ riêng cho A |
| 2 | 2.2 | Negative (không đứng đầu hàng) | A, B, C lần lượt đặt trước cùng một cuốn sách; A đứng đầu | Cuốn sách được trả về thư viện | Chỉ A nhận thông báo **But** B và C không nhận thông báo nào |
| 2 | 2.3 | Edge (hết hạn giữ chỗ) | A đã nhận thông báo và đang được giữ sách 48 giờ; B đứng kế tiếp | Đủ 48 giờ mà A chưa đến nhận | Giữ chỗ của A bị hủy **And** A nhận thông báo giữ chỗ đã hết hạn **And** B nhận thông báo sách đã có sẵn cho mình |
| 2 | 2.4 | Edge (người đã hủy) | A đứng đầu danh sách đặt trước nhưng đã hủy đặt trước từ hôm qua; B đứng kế tiếp | Cuốn sách được trả về thư viện | A không nhận thông báo **And** B nhận thông báo sách đã có sẵn |
| 3 | 3.1 | Happy | Độc giả đang mượn/giữ 4 cuốn (giới hạn 5) | Độc giả đặt mượn cuốn thứ 5 (cuốn đang có sẵn) | Đặt mượn thành công **And** hiển thị "Bạn đã mượn 5/5 cuốn" |
| 3 | 3.2 | Negative + Ràng buộc nghiệp vụ | Độc giả đang mượn/giữ đủ 5 cuốn | Độc giả đặt mượn cuốn thứ 6 (đang có sẵn) | Hệ thống từ chối với thông báo "Bạn đã đạt giới hạn tối đa 5 cuốn, vui lòng trả bớt sách để mượn thêm" **And** số sách của độc giả vẫn là 5 |
| 3 | 3.3 | Edge (sách giữ chỗ cũng tính) | Độc giả có 3 cuốn đang mượn và 2 cuốn đang giữ chỗ chưa nhận | Độc giả đặt mượn thêm 1 cuốn | Hệ thống từ chối với thông báo đã đạt giới hạn 5 cuốn |
| 3 | 3.4 | Edge (giải phóng suất mượn) | Độc giả đang đủ 5 cuốn | Thủ thư xác nhận độc giả đã trả 1 cuốn | Số sách của độc giả là 4/5 **And** độc giả đặt mượn thêm được 1 cuốn |

## 2. Câu hỏi làm rõ cho Product Owner

**Story 1**
1. Thời gian giữ chỗ là 48 giờ tính từ lúc đặt hay từ lúc thư viện mở cửa tiếp theo? (Nếu đặt lúc đêm khuya hoặc ngày nghỉ thì sao?)
2. Khi sách hết, độc giả có được đặt trước không, hay chỉ hiển thị "đã hết"?
3. Một độc giả có được đặt mượn 2 bản của cùng một đầu sách không?

**Story 2**
1. Thông báo gửi qua kênh nào (email, SMS, trong ứng dụng) và gửi tối đa trong bao lâu?
2. Danh sách đặt trước xếp theo thứ tự nào? Có độc giả được ưu tiên không?
3. Nếu độc giả đứng đầu danh sách đang ở giới hạn mượn thì xử lý thế nào, bỏ qua hay giữ chỗ chờ?

**Story 3**
1. Giới hạn là bao nhiêu cuốn? (Giả định: 5 cuốn/độc giả.)
2. Sách đang giữ chỗ nhưng chưa nhận có tính vào giới hạn không? (Giả định: có.)
3. Giới hạn có khác nhau giữa các nhóm độc giả (sinh viên, giảng viên...) không?

## 3. Definition of Done (áp dụng cho mọi Product Backlog Item)

- [ ] Toàn bộ Acceptance Criteria của item đã được kiểm thử và đạt.
- [ ] Code đã được ít nhất 1 thành viên khác trong nhóm review và được duyệt (approve).
- [ ] Unit test đã được viết và đạt, độ phủ test của phần code mới ≥ 80%.
- [ ] Không còn lỗi mức nghiêm trọng (Critical/High) chưa xử lý; kiểm thử hồi quy không phát hiện lỗi mới.
- [ ] Đã triển khai thành công lên môi trường staging và chạy ổn định.
- [ ] Tài liệu liên quan (hướng dẫn sử dụng, ghi chú phát hành) đã được cập nhật.
- [ ] Product Owner đã xem demo và chấp nhận item trong buổi Sprint Review.

## 4. Story 1 đã Done chưa?

**Chưa.** Một story chỉ được coi là Done khi thỏa cả Acceptance Criteria của riêng nó lẫn Definition of Done chung của nhóm. Story 1 chưa được review code nên chưa thỏa DoD, dù đã đạt đủ AC.
