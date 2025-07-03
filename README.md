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
## Kiểm thử
### Kiểm thử đa dạng hóa đối tượng người dùng
- Chữ cái O:
- ![image](https://github.com/user-attachments/assets/df0bc6ba-d929-43dc-899c-91ea5a28596c)
- ![image](https://github.com/user-attachments/assets/4a85dc2e-c843-4a6f-84ed-f887035a30aa)
- Chữ cái B:
- ![image](https://github.com/user-attachments/assets/2e83d81c-49ff-4c23-b425-584200556fb6)
- ![image](https://github.com/user-attachments/assets/77f4a5cb-d733-4c5a-a266-ad7820e3516d)
## Kiểm thử dưới điều kiện ánh sáng khác nhau
- Nơi có ánh sáng mạnh:
- ![image](https://github.com/user-attachments/assets/fe9724df-dae3-4f4a-af7c-c3f28a6ea867)
- Nơi có ánh sáng yếu:
- ![image](https://github.com/user-attachments/assets/a861bc9c-90c3-4f54-a426-a11328603def)
## Kiểm thử biến đổi khoảng cách giữa Camera và đối tượng
- Khi tay ở gần camera:
- ![image](https://github.com/user-attachments/assets/8c464262-ac31-4760-bac3-baff612ae220)
- Khi tay ở xa camera:
- ![image](https://github.com/user-attachments/assets/05a30487-3583-43c0-9a2b-49d993143987)
## Kiểm thử phân biệt các ký hiệu tay có hình dáng tương đồng
- Chữ cái K:
- ![image](https://github.com/user-attachments/assets/fa971314-6c7b-440d-911f-cbd0e6338762)
- Chữ cái V:
- ![image](https://github.com/user-attachments/assets/ee99ec9d-8638-44fe-9804-7e36d8485e46)
## Kiểm thử khả năng nhận diện sau khi tách nền:
![image](https://github.com/user-attachments/assets/dad4088d-d8c8-46b6-849c-aa9a5bfa91e3)
![image](https://github.com/user-attachments/assets/cfd2ea55-ca44-4fd7-a38a-b0c2a0b5e094)
![image](https://github.com/user-attachments/assets/8b4371eb-e63b-47ec-879b-3fee6313962a)

