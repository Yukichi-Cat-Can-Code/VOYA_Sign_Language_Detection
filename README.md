# 🌊 Action Detection for Sign Language

**Hướng dẫn sử dụng & Cài đặt môi trường**

---

## 📖 Mục lục

1. [📌 Giới thiệu](#-giới-thiệu)
2. [🖥️ Yêu cầu hệ thống](#-yêu-cầu-hệ-thống)
3. [⚙️ Cài đặt môi trường](#-cài-đặt-môi-trường)
   - [🔹 Anaconda/Miniconda](#-anacondaminiconda)
   - [🔹 Tạo và kích hoạt môi trường ảo](#-tạo-và-kích-hoạt-môi-trường-ảo)
   - [🔹 Cài đặt thư viện](#-cài-đặt-thư-viện)
4. [📂 Cấu trúc chương trình](#-cấu-trúc-chương-trình)
5. [🧠 Callback Training](#-callback-training)
6. [🚀 Hướng dẫn sử dụng](#-hướng-dẫn-sử-dụng)
7. [🛠️ Tùy chỉnh tham số](#-tùy-chỉnh-tham-số)
8. [❓ Câu hỏi thường gặp](#-câu-hỏi-thường-gặp)
9. [📬 Liên hệ & Đóng góp](#-liên-hệ--đóng-góp)

---

## 📌 Giới thiệu

Dự án **Action Detection for Sign Language** tập trung vào việc nhận diện hành động trong ngôn ngữ ký hiệu bằng học máy. Hệ thống sử dụng:

- 🖐 **MediaPipe** để trích xuất keypoints từ video
- 🎥 **OpenCV** cho xử lý hình ảnh và video
- 🤖 **TensorFlow** để xây dựng và huấn luyện mô hình LSTM

Các chức năng chính:

- Thu thập dữ liệu từ webcam
- Huấn luyện mô hình phân loại chuỗi động tác
- Thực hiện nhận diện thời gian thực

---

## 🖥️ Yêu cầu hệ thống

- **Hệ điều hành:** Windows 10/11 (khuyến nghị)
- **Python:** 3.11
- **RAM:** ≥ 8GB
- **Webcam:** để thu thập và kiểm thử dữ liệu
- **GPU:** (tùy chọn) hỗ trợ tăng tốc huấn luyện TensorFlow

---

## ⚙️ Cài đặt môi trường

### 🔹 Anaconda/Miniconda

- Tải và cài đặt [Anaconda](https://www.anaconda.com/products/distribution) hoặc [Miniconda](https://docs.conda.io/en/latest/miniconda.html).

### 🔹 Tạo và kích hoạt môi trường ảo

```powershell
cd e:\CTU_ProjectOutside\AI_HandSignLanguageModel\ActionDetectionforSignLanguage
conda create -n signlang python=3.11
conda activate signlang
```

### 🔹 Cài đặt thư viện

```bash
pip install tensorflow opencv-python mediapipe scikit-learn matplotlib numpy pandas tqdm
```

---

## 📂 Cấu trúc chương trình

```
📁 ActionDetectionforSignLanguage
│── 📓 Action Detection Refined.ipynb   # Notebook chính
│── 📂 MP_Data/                         # Lưu dữ liệu keypoints
│── 📄 latest_action.h5                 # Trọng số mô hình
│── 📂 .conda/                          # Môi trường Python (nếu dùng)
│── 📄 README.md                        # Tài liệu hướng dẫn
```

---

## 🧠 Callback Training

```python
from tensorflow.keras.callbacks import EarlyStopping, ReduceLROnPlateau

early_stop = EarlyStopping(monitor='val_loss', patience=100, restore_best_weights=True)
reduce_lr = ReduceLROnPlateau(monitor='val_loss', factor=0.5, patience=50, min_lr=1e-6)

history = model.fit(
    X_train, y_train,
    epochs=2000,
    validation_data=(X_val, y_val),
    callbacks=[early_stop, reduce_lr]
)
```

---

## 🚀 Hướng dẫn sử dụng

1. **Thu thập dữ liệu:**

   - Chạy phần _Collect Keypoint Values_ trong notebook
   - Chọn hành động bằng phím số hoặc thêm hành động mới bằng phím `n`
   - Dữ liệu được lưu trong thư mục `MP_Data/`

2. **Tiền xử lý dữ liệu:**

   - Xóa hoặc sửa các sequence lỗi
   - Chuẩn bị dữ liệu dưới dạng `X, y` để huấn luyện

3. **Huấn luyện mô hình:**

   - Chạy phần _Build and Train LSTM_
   - Trọng số mô hình được lưu tại `latest_action.h5`

4. **Đánh giá mô hình:**

   - Sử dụng _Confusion Matrix_ và _Accuracy_ để đánh giá hiệu quả

5. **Nhận diện thời gian thực:**
   - Chạy phần _Test in Real Time_
   - Đưa tay trước webcam để kiểm tra kết quả dự đoán

---

## 🛠️ Tùy chỉnh tham số

- `sequence_length`: số frame mỗi sequence (mặc định 100)
- `no_sequences`: số sequence cho mỗi hành động (mặc định 30)
- `threshold`: ngưỡng xác suất dự đoán (mặc định 0.8)
- `batch_size, epochs`: điều chỉnh trong `model.fit`
- `DATA_PATH`: đường dẫn dữ liệu

---

## ❓ Câu hỏi thường gặp

- **Không nhận diện được webcam?**  
  Kiểm tra thiết bị và đổi `cv2.VideoCapture(0)` thành `cv2.VideoCapture(1)`

- **Thiếu thư viện?**  
  Đảm bảo cài đúng môi trường ảo và thư viện cần thiết

- **Muốn thêm nhiều hành động?**  
  Bổ sung tên hành động vào mảng `actions` và thu thập dữ liệu mới

---

## 📬 Liên hệ & Đóng góp

- **Tác giả:** Mai Nhật Minh
- **Email:** minhb2203567@student.ctu.edu.vn
- **Đóng góp:** Pull request hoặc liên hệ qua email
