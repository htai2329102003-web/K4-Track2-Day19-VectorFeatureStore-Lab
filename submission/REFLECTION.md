# Reflection — Lab 19

**Tên:** Hoàng Văn Tài
**Cohort:** A20-K4 (MSSV: 2A202602400)
**Path đã chạy:** Lite

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

Trên 50 golden queries, hybrid RRF đạt Precision@10 trung bình cao nhất
(78,6%), so với BM25 (77,8%) và vector (73,2%). Với `exact`, BM25 và hybrid
cùng đạt 96,7% vì thuật ngữ xuất hiện nguyên văn. Với `mixed`, hybrid thắng rõ
(100,0%) nhờ kết hợp tín hiệu từ khóa và ngữ nghĩa. Riêng `paraphrase`, BM25
đạt 33,3%, hybrid 32,0% và vector 24,0%: `bge-small-en-v1.5` nhẹ nhưng không
tối ưu cho diễn đạt lại tiếng Việt, nên dense retrieval chưa phát huy lợi thế.

Tôi không dùng hybrid khi truy vấn là mã lỗi, ID hoặc thuật ngữ cần khớp chính
xác (BM25 đơn giản, nhanh hơn), hoặc khi dùng embedding đa ngữ tốt và dữ liệu
chủ yếu là câu hỏi diễn đạt tự nhiên không có keyword ổn định (vector-only có
thể đủ tốt và giảm chi phí vận hành). Hybrid phù hợp nhất khi lưu lượng thực tế
trộn cả exact, paraphrase và mixed.

---

## Điều ngạc nhiên nhất khi làm lab này

Điều bất ngờ nhất là hybrid thắng toàn cục nhưng không thắng mọi lát cắt; chất
lượng embedding theo ngôn ngữ có thể đảo ngược kết luận ở nhóm paraphrase.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _<tên đồng đội nếu có>_
