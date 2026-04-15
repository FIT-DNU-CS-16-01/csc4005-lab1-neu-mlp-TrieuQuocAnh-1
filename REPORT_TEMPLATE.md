# CSC4005 – Lab 1 Report Template

## 1. Mục tiêu
Mục tiêu của bài lab là xây dựng một mô hình Multi-Layer Perceptron (MLP) để phân loại ảnh trong bộ dữ liệu NEU Surface Defect (NEU-CLS).
Bộ dữ liệu NEU bao gồm các ảnh bề mặt thép với 6 loại lỗi khác nhau:
Crazing
Inclusion
Patches
Pitted Surface
Rolled-in Scale
Scratches

Nhiệm vụ là huấn luyện mô hình để dự đoán đúng loại lỗi từ ảnh đầu vào.
## 2. Cấu hình thí nghiệm
Ba cấu hình khác nhau đã được thử nghiệm:

🔹 Run 1 – baseline_adamw
Optimizer: AdamW
Learning rate: 0.001
Batch size: 32
Hidden dims: [512, 256]
Dropout: 0.3
🔹 Run 2 – run2_sgd_large_model
Optimizer: SGD
Learning rate: 0.01
Batch size: 64
Hidden dims: [1024, 512, 256]
Dropout: 0.1
🔹 Run 3 – run3_regularized
Optimizer: AdamW
Learning rate: 0.0003
Batch size: 16
Hidden dims: [256, 128]
Dropout: 0.5
## 3. Kết quả
Run	Optimizer | Val Accuracy | Val Loss | Nhận xét
baseline_adamw | AdamW | ~0.42 | ~1.50 (thấp nhất) | Ổn định
run2_sgd_large_model | SGD | ~0.48 (cao nhất) | 1.55 | Dao động mạnh
run3_regularized | AdamW | ~0.35 | ~1.60 | Ít overfit
## 4. Phân tích
- Nếu xét accuracy → run2_sgd_large_model tốt nhất
Nếu xét tổng thể (ổn định + loss thấp) → baseline_adamw tốt nhất
👉 baseline_adamw là lựa chọn cân bằng nhất
- Overfitting (run2):
Train tốt nhưng validation dao động
Khoảng cách giữa train và val lớn
Underfitting (run3):
Accuracy thấp
Model quá nhỏ + dropout cao → học chưa đủ
- Tiêu chí | AdamW | SGD
Tốc độ hội tụ | Nhanh | Chậm hơn
Ổn định | Cao | Dao động
Generalization | Tốt | Phụ thuộc tuning
Kết quả thực nghiệm | Ổn định | Accuracy cao nhưng không ổn định
## 5. Kết luận
Cấu hình tốt nhất : baseline_adamw
