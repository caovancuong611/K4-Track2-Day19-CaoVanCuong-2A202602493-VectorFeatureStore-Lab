# Reflection — Lab 19

**Tên:** Cao Văn Cường
**Cohort:** A20-K4
**Path đã chạy:** lite

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

Trên 50 golden queries, hybrid (RRF k=60) thắng trung bình: 78.6% so với BM25 77.8% và vector 73.2%.

Với exact, BM25 và hybrid hòa nhau (96.7%) vì query chứa đúng thuật ngữ trong doc. Với paraphrase, kết quả ngược kỳ vọng: vector chỉ đạt 24.0%, thua BM25 (33.3%). Nguyên nhân là bge-small-en được huấn luyện cho tiếng Anh, không hiểu tiếng Việt diễn đạt lại; cần bge-m3 để vector phát huy. Với mixed, hybrid đạt 100% vì RRF kết hợp tín hiệu từ khóa và ngữ nghĩa, bù điểm yếu của mỗi bên.

Không nên dùng hybrid khi: (1) tra mã lỗi, ID, SKU, tức khớp chính xác, thì BM25 đủ và nhanh hơn (P99 2.8ms so với 16.7ms); (2) latency là ràng buộc cứng; (3) có embedding đa ngôn ngữ tốt và query chủ yếu là câu tự nhiên, khi đó vector thuần đơn giản hơn.

---

## Điều ngạc nhiên nhất khi làm lab này

Embedding model quan trọng hơn thuật toán: model sai ngôn ngữ khiến semantic thua cả BM25. Ngoài ra PIT join ở NB4 loại bỏ một dòng vì feature chưa tồn tại tại thời điểm đó, nghĩa là PIT join chạy đúng chứ không phải lỗi.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _<tên đồng đội nếu có>_
