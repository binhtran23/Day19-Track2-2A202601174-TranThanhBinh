# Reflection — Lab 19

**Tên:** Trần Thanh Bình
**Cohort:** A20-K4
**Path đã chạy:** lite

---

## Câu hỏi (≤ 200 chữ) — **bắt buộc, đây là phần được chấm điểm**

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

Trong golden set 50 queries, ở query “exact” BM25 và hybrid bằng nhau (96.7%), ở “paraphrase” BM25 thắng với 33.3%, còn “mixed” thì hybrid thắng rõ nhất 100%. Lí do BM25 và hybrid gần như nhau là semantic search đang bị lỗi embedding, do bge-small-en train tiếng Anh trong khi dữ liệu là tiếng Việt. Hybrid có lợi thế về ngữ nghĩa và vẫn giữ được các keyword quan trọng, nhưng tradeoff là latency. Từ NB03, P50 wall của hybrid là 9.8ms so với 3.6ms của keyword, còn P99 wall lên tới 20.6ms. Vậy nên không nên dùng hybrid khi cần retrieval nhanh và độ chính xác tương đối là đủ. Trong trường hợp này, nếu người dùng ưu tiên tốc độ thì có thể đổi sang pure BM25, vì accuracy chỉ giảm nhẹ (78.6% → 77.8%) nhưng P50 wall giảm khá nhiều (9.8ms → 3.6ms). Ở đây dùng wall latency vì nó phản ánh trực tiếp hơn thời gian phản hồi mà người dùng cảm nhận.

---

## Điều ngạc nhiên nhất khi làm lab này

Ở notebook 2. Độ chính xác của keyword (77.8%) > semactic search (73.2%). Đồng thời ở mod paraphase BM25 lại thắng trong khi đây là điểm mạnh của vector.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _<tên đồng đội nếu có>_
