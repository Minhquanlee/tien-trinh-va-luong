---
title: "Tiến trình & Luồng"
date: "2023-10-26"
updated: "2023-10-26"
categories:
  - sveltekit
  - markdown
coverImage: "/images/jefferson-santos-fCEJGBzAkrU-unsplash.jpg"
coverWidth: 16
coverHeight: 9
excerpt: "Check out how heading links work with this starter in this post."
---

# Tiến trình & Luồng

## Câu 1: Dựa vào bài học, check CPU, GPU, RAM, giải thích về hiệu năng của máy tính mà em đang dùng?

### Thông số hệ thống (ví dụ minh họa):
- **CPU**: Intel Core i7-12700H (14 cores, 20 threads)
- **GPU**: NVIDIA GeForce RTX 3060 Laptop GPU
- **RAM**: 16GB DDR5

### Đánh giá hiệu năng:
- **CPU**: Sở hữu nhiều lõi và luồng cho phép xử lý đa nhiệm tốt, phù hợp với các ứng dụng đa tiến trình hoặc đa luồng như lập trình, dựng video, chơi game nặng,...
- **GPU**: RTX 3060 có khả năng xử lý song song mạnh, rất thích hợp cho các tác vụ như xử lý đồ họa, AI, deep learning hoặc chơi game độ phân giải cao.
- **RAM**: 16GB là mức dung lượng lý tưởng cho phần lớn nhu cầu hiện tại từ học tập đến làm việc, đảm bảo xử lý mượt nhiều tác vụ đồng thời (đa nhiệm).

---

## Câu 3: Liệt kê các trường hợp nên dùng Thread, Process, và khi nào nên dùng cả hai

| Trường hợp                      | Dùng Thread           | Dùng Process           | Dùng cả hai                              |
|-------------------------------|-----------------------|------------------------|-------------------------------------------|
| Ứng dụng cần chia sẻ bộ nhớ    | ✅                    | ❌                    | ✅ (nhiều tiến trình, mỗi tiến trình nhiều luồng) |
| Tác vụ tính toán nhẹ, nhanh    | ✅                    | ❌                    | ❌                                         |
| Tác vụ tốn nhiều CPU           | ❌                    | ✅                    | ✅ (chia nhỏ khối lượng công việc)         |
| Tác vụ có thể bị lỗi tách biệt | ❌                    | ✅ (cách ly tốt)       | ❌                                         |
| Web server đa kết nối          | ✅ (mỗi client 1 thread) | ❌                 | ✅ (thread pool trong process)            |
| Dựng video, encode             | ❌                    | ✅                    | ✅                                         |

### Ví dụ bài toán:
- **Thread**: Ứng dụng chat – mỗi kết nối là một thread.
- **Process**: Trình duyệt web – mỗi tab là một process riêng biệt.
- **Cả hai**: Game server online – mỗi người chơi là thread, mỗi bản đồ là một process.

---

## Câu 4: Report – ChatGPT training tập dữ liệu lớn bằng Distributed System như thế nào?

### Tóm tắt:
- ChatGPT được huấn luyện bằng **hệ thống phân tán (distributed system)** sử dụng nhiều GPU/TPU trên các cụm máy chủ mạnh mẽ.
- Khối lượng dữ liệu đầu vào rất lớn (Internet, sách, mã nguồn...), nên cần chia nhỏ (**sharding**) để xử lý song song.
- Kỹ thuật được sử dụng gồm:
  - **Data Parallelism**: chia nhỏ dữ liệu để huấn luyện trên nhiều GPU.
  - **Model Parallelism**: chia mô hình lớn thành các phần chạy song song.
  - **Pipeline Parallelism**: xử lý liên tục qua các bước theo dòng chảy dữ liệu.

### Các bước chính:
1. Dữ liệu được chia và tiền xử lý trên nhiều máy chủ.
2. Mỗi node xử lý một phần của mô hình hoặc dữ liệu.
3. Kết quả huấn luyện được đồng bộ lại thông qua các phương thức như **All-Reduce**, **Ring All-Reduce**.
4. Mô hình cuối cùng được hợp nhất và tinh chỉnh lại (fine-tune) trên tập dữ liệu có chọn lọc.

### Tài liệu tham khảo:
- [HuggingFace Blog – Large Language Model Training](https://huggingface.co/blog/large-language-model-training)
- [NVIDIA DGX Systems](https://www.nvidia.com/en-us/data-center/dgx-systems/)
- [OpenAI Research](https://openai.com/research)
