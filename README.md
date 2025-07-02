# Nhận diện bảng chữ cái ngôn ngữ kí hiệu theo thời gian thực sử dụng mô hình mạng Nơ-ron tích chập CNN 
## 📌 Giới thiệu
Dự án này sử dụng **Google Teachable Machine** để xây dựng một mô hình học máy nhằm **Nhận diện bảng chữ cái trong thủ ngữ**. Mô hình được huấn luyện với hình ảnh đã qua tiền xử lý và được triển khai trên nền tảng web Google Colab
## Tiền Xử Lý Dữ Liệu
- Dữ liệu được gán **nhãn khung giới hạn (bounding boxes)** thủ công bằng phần mềm **LabelImg**.
- Ảnh gốc và thông tin nhãn được đưa qua pipeline xử lý ảnh bằng thư viện **Albumentations**:
  - Chuyển đổi ảnh sang định dạng RGB.
  - Resize ảnh về kích thước 224x224 pixels.
  - Chuyển sang mảng NumPy, chuẩn hóa giá trị pixel.
  - Tạo batch đầu vào cho mô hình học máy.
![image](https://github.com/user-attachments/assets/e0905f97-556e-4a1b-ab62-0871d32edc9d)
## Huấn Luyện Mô Hình với Teachable Machine
### Quy Trình:
1. **Chuẩn Bị Dữ Liệu**: Ảnh đã xử lý được đưa vào và phân loại theo từng nhãn (ký tự thủ ngữ).
2. **Thiết Lập Tham Số**:
   - `Epoch`: số vòng lặp học.
   - `Batch size`: số lượng ảnh trong mỗi batch.
   - `Learning rate`: tốc độ cập nhật trọng số.
3. **Tiến Hành Huấn Luyện**: Teachable Machine tự động huấn luyện và tối ưu mô hình.
![image](https://github.com/user-attachments/assets/f629830e-0e04-4e34-b165-c612effb4e1a)
## Đánh Giá Kết Quả Huấn Luyện
###  Ma Trận Nhầm Lẫn (Confusion Matrix):
- Giúp xác định những cặp lớp thường bị nhầm lẫn để cải thiện chất lượng dữ liệu và khả năng phân loại.
![image](https://github.com/user-attachments/assets/2f362964-15a3-4527-bb38-811f9ed5b338)
###  Accuracy per Epoch:
- Biểu đồ cho biết mức độ chính xác của mô hình sau mỗi epoch. Độ chính xác cao (gần 1) cho thấy mô hình học tốt.
![image](https://github.com/user-attachments/assets/c00d4fd6-2bc0-4d85-bdb8-0895991f4d2c)
###  Loss per Epoch:
- Cho biết độ sai lệch giữa dự đoán và nhãn thực tế. Loss thấp → mô hình hiệu quả hơn.
![image](https://github.com/user-attachments/assets/9df03c1a-a585-43c7-84e7-3d2ff6f37d1d)
###  Accuracy per Class:
- Đánh giá khả năng phân loại theo từng ký tự/thủ ngữ riêng biệt. Phát hiện lớp có độ chính xác thấp để bổ sung dữ liệu.
![image](https://github.com/user-attachments/assets/541899d1-099b-4e00-9e86-ea44b242a002)
### 🔹 Training vs Test Samples:
- **85% dữ liệu** dùng huấn luyện.
- **15% dữ liệu** dùng kiểm tra.
- Phân chia giúp tránh hiện tượng **overfitting** hoặc **underfitting**.
##  Xuất và Triển Khai Mô Hình
### 💾 Các định dạng mô hình:
- **`.h5`**: Dành cho triển khai trên web/server Python (Keras/TensorFlow).
- **`.tflite`**: Dành cho ứng dụng di động, nhẹ và tối ưu hóa hiệu suất.

### 🛠️ Quy Trình Tích Hợp:
1. **Tải mô hình vào ứng dụng**:
   - `.h5`: Dùng TensorFlow/Keras.
2. **Kiểm thử & tối ưu**:
   - Đánh giá hiệu năng, độ chính xác.
   - Tối ưu mức tiêu thụ tài nguyên, đặc biệt trên thiết bị di động.
3. **Triển khai sản phẩm cuối**:
   - `.h5`: Web apps / APIs.


## Công Nghệ Sử Dụng
- [Teachable Machine](https://teachablemachine.withgoogle.com/)
- Python (TensorFlow, Keras)
- TensorFlow Lite (cho di động)
- LabelImg (gán nhãn thủ công)
- Albumentations (tiền xử lý ảnh)
- NumPy

## Cấu Trúc Dự Án
```
├── Dữ liệu huấn luyện/
│   ├── A/...
│   └── ...Z/
├── Nhận_diện_cử_chỉ_bàn_tay.ipynb
├── Source/
│   ├── keras_model.h5
│   └── labels.txt
├── README.md
```

