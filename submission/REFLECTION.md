# Reflection — Lab 19

**Tên:** Đỗ Quốc An  
**MSSV:** 2A202600952  
**Path đã chạy:** lite

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

Trên golden set 50 queries (lite, `bge-small-en-v1.5`), hybrid P@10 cao nhất (78.6% > BM25 77.8% > vector 73.2%). **`exact`**: BM25 ≈ hybrid (~96.7%) vì từ khóa verbatim khớp corpus; vector ~88.7%. **`paraphrase`**: cả ba thấp (BM25 33.3%, hybrid 32%, vector 24%) — embedding EN không bắt paraphrase VN không trùng từ gốc. **`mixed`**: hybrid thắng (100% vs ~97–98.5%) nhờ RRF gộp tín hiệu exact + ngữ nghĩa.

**Không dùng hybrid** khi: query là mã/SKU chính xác → pure BM25 (rẻ, nhanh); tác vụ “tìm tương tự” → pure vector; ngân sách latency chặt — fusion chạy hai retriever tốn gấp đôi; metadata filter đã thu hẹp kết quả đủ tốt.

---

## Điều ngạc nhiên nhất khi làm lab này

Paraphrase query tiếng Việt không có chữ “cloud” vẫn trả về đúng cluster `cloud` trong NB1 — nhưng trên golden set P@10 paraphrase lại rất thấp, cho thấy **chọn embedding model quan trọng hơn** việc có hybrid hay không.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _<tên đồng đội nếu có>_
