# KỊCH BẢN THUYẾT TRÌNH (PHIÊN BẢN RÚT GỌN)

## Đề tài: Phân tích cảm xúc người dùng dựa trên bình luận trực tuyến

**Thời lượng:** 30 phút | **Thực hiện:** Đỗ Mai Anh & Nguyễn Hoàng Quyên | **GVHD:** TS. Phan Tấn Quốc

---

## PHẦN 1: KHỞI ĐỘNG & GIỚI THIỆU (3 phút)

### [Slide 1: Trang mở đầu]
Kính chào quý thầy cô! Hôm nay chúng em xin trình bày đồ án chuyên ngành:
**"Phân tích cảm xúc người dùng dựa trên bình luận trực tuyến"**

---

### [Slide 2: Lý do chọn đề tài]

**Ba lý do chính:**

1. **Khoa học:** Sentiment Analysis là bài toán thú vị trong NLP, kết hợp ngôn ngữ học + học máy + AI
2. **Thực tiễn:** Ứng dụng rộng rãi — kinh doanh (nắm bắt phản hồi), giáo dục (đánh giá tâm lý), chăm sóc khách hàng...
3. **Thách thức:** Tiếng Việt có nhiều đặc thù — tiếng lóng, từ viết tắt, emoji — khiến phương pháp truyền thống chưa hiệu quả

**Mục tiêu:** Đóng góp góc nhìn thực nghiệm về hiệu quả các mô hình phân tích cảm xúc tiếng Việt

---

## PHẦN 2: TỔNG QUAN LÝ THUYẾT (6 phút)

### [Slide 3: Khái niệm & Mức độ]
**Sentiment Analysis** = xác định cảm xúc qua văn bản (NLP)

**3 mức độ:**
- Tài liệu: toàn bộ văn bản
- Câu: từng câu cụ thể ← *Chúng em tập trung*
- Khía cạnh: từng đặc điểm sản phẩm

**3 nhãn:** Positive / Negative / Neutral

---

### [Slide 4: Quy trình chung]
```
Dữ liệu → Tiền xử lý → Biểu diễn → Huấn luyện → Đánh giá
```

Bài toán được mô hình hóa là **phân loại có giám sát**: Tìm hàm f: văn bản → nhãn cảm xúc

---

### [Slide 5: Thách thức tiếng Việt]
1. **Ngôn ngữ đơn lập:** khoảng trắng phân tách âm tiết, không phải từ → **tách từ** là bước bắt buộc
2. **Dữ liệu mạng xã hội:** viết tắt ("kho", "sp"), tiếng lóng ("keo lỳ"), lỗi chính tả, emoji 😂😢😡

→ Cần quy trình tiền xử lý phù hợp

---

### [Slide 6: Các nghiên cứu liên quan]
**3 giai đoạn phát triển:**

| Giai đoạn | Thuật toán | Ưu điểm | Hạn chế |
|-----------|------------|---------|---------|
| 1. ML truyền thống | NB, SVM, LR | Đơn giản, nhanh | Không hiểu ngữ nghĩa sâu |
| 2. Deep Learning | CNN, LSTM, BiLSTM | Học đặc trưng tự động | Cần dữ liệu lớn |
| 3. Transformer | BERT, PhoBERT | Hiểu ngữ cảnh sâu | Tốn tài nguyên |

**Nghiên cứu của chúng em:** Giai đoạn 3 — đánh giá so sánh từ truyền thống → hiện đại

---

### [Slide 7: Độ đo đánh giá]
- **Accuracy:** Tỷ lệ đúng tổng thể
- **Precision:** Độ chính xác mỗi lớp
- **Recall:** Khả năng phát hiện mỗi lớp
- **F1-score:** Trung bình điều hòa (quan trọng nhất với dữ liệu mất cân bằng)

---

## PHẦN 3: PHƯƠNG PHÁP NGHIÊN CỨU (10 phút)

### [Slide 8: Mô hình hóa bài toán]
- **Input:** x = văn bản bình luận
- **Output:** y ∈ {Positive, Negative, Neutral}
- **Mục tiêu:** Tìm f sao cho sai lệch ŷ - y nhỏ nhất

---

### [Slide 9: Tiền xử lý dữ liệu]
**Quy trình 6 bước:**
1. **Chuẩn hóa:** chữ thường, khoảng trắng
2. **Loại bỏ:** URL, HTML, email, số điện thoại
3. **Tách từ:** VnCoreNLP / underthesea + RDRSegmenter
4. **Tiếng lóng:** "kho" → "không", "j" → "gì"
5. **Emoji:** Chuyển thành text (😂 → "vui vẻ, tích cực")
6. **Stopwords:** Loại bỏ từ không mang nghĩa, **giữ lại phủ định/nhấn mạnh**

---

### [Slide 10-13: Các mô hình]

**Baseline (ML truyền thống):**
- **Naive Bayes:** Đơn giản, nhanh, hiệu quả với dữ liệu lớn
- **SVM:** Tốt trong không gian nhiều chiều + TF-IDF
- **Random Forest:** Ensemble, giảm overfitting

**Deep Learning:**
- **CNN:** Phát hiện đặc trưng cục bộ (n-gram: "rất tốt", "không hài lòng")
- **LSTM:** Giải quyết vanishing gradient, ghi nhớ phụ thuộc dài hạn
- **BiLSTM:** Xử lý hai hướng — hiểu ngữ cảnh từ trước + sau

---

### [Slide 14: PhoBERT]
Mô hình tiền huấn luyện riêng cho tiếng Việt:
- Huấn luyện trên ~20GB dữ liệu VN
- BPE tokenizer + RDRSegmenter tích hợp
- Self-attention hai chiều sâu

→ Phù hợp nhất cho tiếng Việt (so với mBERT, BERT-base)

---

### [Slide 15: Mô hình đề xuất - PhoBERT-CNN-LSTM]
**Ý tưởng:** Kết hợp ưu điểm 3 kiến trúc

| Thành phần | Vai trò |
|------------|---------|
| PhoBERT | Mã hóa ngữ nghĩa sâu |
| CNN | Phát hiện đặc trưng cục bộ |
| LSTM/BiLSTM | Mô hình hóa tuần tự |

→ Hiệu quả đặc biệt với bình luận ngắn, dữ liệu mạng xã hội nhiều nhiễu

---

### [Slide 16: Kiến trúc tổng thể]
```
Dữ liệu → Tiền xử lý → Biểu diễn → Mô hình → Đánh giá
                    ↓
            - TF-IDF (ML)
            - PhoBERT embedding (DL)
```

**Mô hình so sánh:** NB, SVM, RF, CNN, LSTM, BiLSTM, PhoBERT, PhoBERT-CNN-LSTM

---

## PHẦN 4: ĐÓNG GÓP & KẾT LUẬN (6 phút)

### [Slide 17: Đóng góp mới]
1. **Nghiên cứu thực nghiệm có hệ thống:** So sánh trực tiếp nhiều mô hình trên cùng dataset
2. **Pipeline tiền xử lý:** Khai thác emoji + tiếng lóng thay vì loại bỏ
3. **Nguồn tham chiếu:** Dataset công khai + kết quả chi tiết cho nghiên cứu sau

---

### [Slide 18: Kết luận]
- **Chương 1:** Cơ sở lý thuyết, đặc thù tiếng Việt, nghiên cứu liên quan
- **Chương 2:** Phương pháp, tiền xử lý, các mô hình từ ML → Hybrid

**Mục tiêu:** Xác định mô hình phù hợp nhất — cân bằng độ chính xác và chi phí tính toán

---

### [Slide 19: Hạn chế & Hướng phát triển]
**Hạn chế:**
- Chỉ tiếng Việt đơn ngữ
- Chưa có hệ thống hoàn chỉnh
- Chưa tối ưu hyperparameter

**Hướng phát triển:**
- Triển khai hệ thống thực tế
- Mở rộng aspect-based SA
- Áp dụng lĩnh vực cụ thể

---

## PHẦN 5: KẾT THÚC (5 phút)

### [Slide 20: Kính mời đóng góp ý kiến]
Kính mời quý thầy cô góp ý để đề tài được hoàn thiện hơn.

Xin chân thành cảm ơn!

---

## PHỤ LỤC: CÂU HỎI THƯỜNG GẶP

### Câu 1: Em tóm tắt lại những gì đã làm?
**Trả lời:**

**Về nghiên cứu lý thuyết:**
- Nghiên cứu tổng quan về phân tích cảm xúc và xử lý ngôn ngữ tự nhiên
- Khảo sát các phương pháp từ ML truyền thống (Naive Bayes, SVM, Random Forest) đến Deep Learning (CNN, LSTM, BiLSTM) và Transformer (PhoBERT)
- Phân tích đặc thù ngôn ngữ tiếng Việt và thách thức khi xử lý dữ liệu mạng xã hội

**Về thiết kế phương pháp:**
- Đề xuất quy trình tiền xử lý dữ liệu tiếng Việt: tách từ, xử lý tiếng lóng, chuyển đổi emoji
- Thiết kế kiến trúc mô hình lai PhoBERT-CNN-LSTM kết hợp ưu điểm ba kiến trúc
- Xác định các độ đo đánh giá: Accuracy, Precision, Recall, F1-score

**Về tài liệu:**
- Hoàn thiện Chương 1: Cơ sở lý thuyết và tổng quan nghiên cứu
- Hoàn thiện Chương 2: Phương pháp và mô hình nghiên cứu
- Thu thập và đọc 7+ bài báo khoa học liên quan

---

**CHI TIẾT CHƯƠNG 1 & 2:**

**Chương 1: Cơ sở lý thuyết và tổng quan nghiên cứu**
- *Các khái niệm cơ bản:* Định nghĩa Sentiment Analysis, 3 mức độ phân tích (tài liệu, câu, khía cạnh)
- *Vai trò trong NLP:* Bài toán được mô hình hóa là phân loại văn bản có giám sát
- *Đặc thù tiếng Việt:* Ngôn ngữ đơn lập, cần tách từ, nhiều biến thể ngôn ngữ mạng (viết tắt, tiếng lóng, emoji)
- *Lịch sử phát triển:* 3 giai đoạn — ML truyền thống → Deep Learning → Transformer
- *Độ đo đánh giá:* Accuracy, Precision, Recall, F1-score (F1 quan trọng nhất với dữ liệu mất cân bằng)

**Chương 2: Phương pháp và mô hình nghiên cứu**
- *Mô hình hóa bài toán:* Input là văn bản bình luận, Output là {Positive, Negative, Neutral}, tìm hàm f(x) → ŷ
- *Quy trình tiền xử lý 6 bước:* Chuẩn hóa → Loại bỏ ký tự đặc biệt → Tách từ (VnCoreNLP) → Xử lý tiếng lóng → Chuyển emoji thành text → Loại bỏ stopwords (giữ lại từ phủ định)
- *7 mô hình baseline:* Naive Bayes, SVM, Random Forest, CNN, LSTM, BiLSTM, PhoBERT
- *Mô hình đề xuất:* PhoBERT-CNN-LSTM kết hợp 3 kiến trúc: PhoBERT (ngữ nghĩa sâu) + CNN (đặc trưng cục bộ) + LSTM (tuần tự)
- *Kiến trúc hệ thống:* Dữ liệu → Tiền xử lý → Biểu diễn (TF-IDF/PhoBERT embedding) → Huấn luyện → Đánh giá

---

### Câu 2: Kế hoạch tiếp theo?
**Trả lời:**
- **2-4 tuần:** Hoàn thiện Chương 3 + tiền xử lý dữ liệu
- **1-2 tháng:** Implement các mô hình + chạy thực nghiệm
- **2-3 tháng:** Phân tích kết quả + hoàn thiện báo cáo

---

### Câu 3: Tại sao chọn PhoBERT thay vì BERT/mBERT?
**Trả lời:** PhoBERT được thiết kế riêng cho tiếng Việt với 20GB dữ liệu VN + RDRSegmenter tích hợp — mBERT có dữ liệu VN ít, không tách từ → kết quả thấp hơn 5-10%

---

### Câu 4: Tại sao không dùng XGBoost/LightGBM?
**Trả lời:** Boosting mạnh nhưng không tận dụng sequence information như LSTM. Em muốn so sánh ML truyền thống với DL/Transformer để thấy rõ sự tiến hóa.

---

### Câu 5: Điểm mới so với nghiên cứu trước?
**Trả lời:**
1. **Mô hình lai:** PhoBERT + CNN + LSTM (thường dùng riêng lẻ)
2. **Emoji processing:** Chuyển thành text thay vì loại bỏ
3. **So sánh toàn diện:** ML → DL → Transformer trên cùng dataset

---

### Câu 6: Em đã implement gì chưa?
**Trả lời:** Đang giai đoạn thiết kế và chuẩn bị dữ liệu. Implement sẽ được trình bày chi tiết trong Chương 3.

---

### Câu 7: Dataset nào? Tên trên Kaggle?
**Trả lời:**

| Dataset | Tên trên Kaggle | Nguồn | Nhãn |
|---------|-----------------|-------|------|
| **UIT-VSFC** | `uit-vn-sentiment-analysis` | UIT | Pos, Neg, Neu |
| **Vietnamese E-commerce** | `vietnamese-e-commerce-reviews` | Shopee/Lazada | 1-5 sao → Pos/Neu/Neg |
| **VLSP Sentiment** | `vlsp-2021-sentiment` | VLSP 2021 | Pos, Neg |

Dataset chính sẽ dùng: **UIT-VSFC** — có 3 nhãn cân bằng, phù hợp nhất cho bài toán phân loại 3 lớp.

---

### Câu 8: Tại sao phải tách từ tiếng Việt?
**Trả lời:** Tiếng Việt là ngôn ngữ đơn lập — khoảng trắng tách âm tiết, không phải từ. Ví dụ: "sinh viên" = 2 âm tiết = 1 từ. Không tách → mất nghĩa.

---

### Câu 9: Naive Bayes với giả định độc lập có phù hợp?
**Trả lời:** Hạn chế lớn nhưng vẫn hoạt động tốt trong thực tế — đơn giản, nhanh, baseline tốt để so sánh.

---

### Câu 10: Accuracy hay F1-score quan trọng hơn?
**Trả lời:** **F1-score** vì dữ liệu có thể mất cân bằng, cần đánh giá công bằng giữa 3 classes.

---

### Câu 11: Quy trình đề xuất của em là gì?
**Trả lời:**
```
1. Thu thập dữ liệu → Kaggle (Vietnamese Student Feedback, E-commerce Reviews, UIT-VSFC)
2. Tiền xử lý → Chuẩn hóa, tách từ, xử lý tiếng lóng + emoji
3. Biểu diễn → TF-IDF (ML) / PhoBERT embedding (DL)
4. Huấn luyện → Implement 8 mô hình, fine-tune hyperparameters
5. Đánh giá → So sánh Accuracy, Precision, Recall, F1-score
```

---

### Câu 12: Em dự định test bao nhiêu mô hình?
**Trả lời:** Tổng cộng **8 mô hình**:

| Loại | Mô hình | Số lượng |
|------|---------|----------|
| ML truyền thống | Naive Bayes, SVM, Random Forest | 3 |
| Deep Learning | CNN, LSTM, BiLSTM | 3 |
| Transformer | PhoBERT, PhoBERT-CNN-LSTM | 2 |

Tất cả được chạy trên **cùng tập dữ liệu** để so sánh công bằng.

---

## MẸO TRÌNH BÀY

1. Không đọc slide, chỉ nói điểm chính
2. Nhấn mạnh các từ khóa
3. Dừng ở các điểm quan trọng
4. Khi chưa có kết quả: "Dựa trên lý thuyết và nghiên cứu liên quan..."
5. Thừa nhận hạn chế một cách chân thành

---

## THỜI GIAN PHÂN BỔ

| Phần | Thời gian |
|------|-----------|
| Giới thiệu | 3 phút |
| Lý thuyết | 6 phút |
| Phương pháp | 10 phút |
| Kết luận | 6 phút |
| Hỏi đáp | 5 phút |
