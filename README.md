# 🚨 AI Incident Detector – Hệ thống phát hiện và tường thuật tai nạn giao thông bằng AI

Một hệ thống AI thông minh có khả năng phân tích video từ camera giao thông, phát hiện các sự cố như va chạm, dừng đột ngột, và tự động sinh bản tường thuật sự kiện bằng ngôn ngữ tự nhiên.

---

## 📌 Mục lục

- [🧠 Giới thiệu tổng quan](#-giới-thiệu-tổng-quan)
- [🎯 Tính năng nổi bật](#-tính-năng-nổi-bật)
- [📐 Kiến trúc hệ thống](#-kiến-trúc-hệ-thống)
- [🛠️ Công nghệ sử dụng](#-công-nghệ-sử-dụng)
- [📂 Dataset sử dụng](#-dataset-sử-dụng)
- [⚙️ Cách hoạt động](#-cách-hoạt-động)
- [📊 Kết quả & Demo](#-kết-quả--demo)
- [🚧 Hướng phát triển tương lai](#-hướng-phát-triển-tương-lai)
- [👨‍💻 Thông tin tác giả](#-thông-tin-tác-giả)

---

## 🧠 Giới thiệu tổng quan

**AI Incident Detector** là một dự án tích hợp **Computer Vision**, **Object Tracking**, **Phát hiện bất thường (Anomaly Detection)** và **Natural Language Generation (NLG)**.

Mục tiêu:
- Phát hiện tai nạn hoặc va chạm giao thông trong video.
- Theo dõi và phân tích hành vi phương tiện.
- Sinh bản tường thuật sự kiện một cách tự động bằng tiếng Việt (hoặc tiếng Anh).

---

## 🎯 Tính năng nổi bật

| Tính năng | Mô tả |
|----------|--------|
| 🎥 Phân tích video | Nhận input từ camera giao thông hoặc video có sẵn |
| 🚗 Nhận diện & theo dõi phương tiện | Sử dụng YOLOv8 và DeepSORT để theo dõi các xe trong video |
| ⚠️ Phát hiện bất thường | Dừng đột ngột, va chạm, thay đổi hướng bất thường |
| 📝 Sinh bản tin sự kiện | Dùng mô hình ngôn ngữ lớn (LLM) để tạo bản tường thuật tự động |
| 📊 Giao diện hiển thị | Hiển thị video, thông tin sự cố, bản tin và log thời gian thực |
| 📤 Tùy chọn cảnh báo | Có thể mở rộng gửi Telegram, Email cảnh báo tự động |

---

## 📐 Kiến trúc hệ thống

[Video đầu vào]
↓
[YOLOv8 Object Detection]
↓
[DeepSORT Object Tracking]
↓
[Phát hiện bất thường]
↓
[Sinh JSON dữ kiện sự cố]
↓
[Prompt GPT / Mistral sinh bản tin]
↓
[Giao diện Streamlit hiển thị + log]


---

## 🛠️ Công nghệ sử dụng

- **Computer Vision**: YOLOv8, OpenCV
- **Tracking**: DeepSORT
- **NLP**: Gemini-2.5-flash
- **Frontend**: Streamlit hoặc Gradio
- **Backend**: Python, FastAPI
- **Dữ liệu**: Postgre
- **Khác**: Docker (tuỳ chọn triển khai), Git, ffmpeg

---

## 📂 Dataset sử dụng

- [AI City Challenge Dataset](https://www.aicitychallenge.org/)
- [UA-DETRAC](https://detrac-db.rit.albany.edu/)
- Video dashcam tai nạn từ YouTube (trích thủ công)

---

## ⚙️ Cách hoạt động

1. **Phân tích video đầu vào**
   - Sử dụng YOLOv8 để phát hiện phương tiện giao thông.
   - DeepSORT để theo dõi các xe qua nhiều frame.

2. **Phát hiện va chạm hoặc bất thường**
   - Dựa trên vector chuyển động, vận tốc, khoảng cách giữa bounding boxes.
   - Có thể kết hợp rule-based hoặc AutoEncoder anomaly detection.

3. **Tạo metadata sự kiện**
```json
{
  "timestamp": "15:42",
  "location": "Ngã tư Tôn Thất Tùng - Trường Chinh",
  "vehicles": ["ô tô", "xe máy"],
  "event": "va chạm",
  "note": "xe máy ngã, ô tô dừng đột ngột"
}
```
Sinh bản tin bằng AI

Prompt đưa vào LLM như GEMINI-2.5-flash

“Hãy viết một bản tường thuật tai nạn giao thông dựa trên dữ kiện sau...”

Kết quả:

"Vào lúc 15:42 tại ngã tư Tôn Thất Tùng – Trường Chinh, đã xảy ra va chạm giữa xe máy và ô tô. Xe máy ngã ra đường, ô tô dừng đột ngột. Chưa ghi nhận thương vong."

Giao diện người dùng

Hiển thị video + khung sự cố + log + bản tin sinh ra.
