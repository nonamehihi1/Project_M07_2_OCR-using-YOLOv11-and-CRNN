# Project_M07_2_OCR-using-YOLOv11-and-CRNN
Trong project xây dựng dự án OCR dùng YOLOv11 để text dectect và dùng CRNN để nhận dạng chuỗi ký tự

I. Lý thuyết
I.1 Text dectec với YOLO
- Cơ chế cốt lõi YOLO sẽ trả về 3 thành phần chính:
  1. Bounding box: khung chứa văn bản
  2. Object score: Xác suất trong khung hình đó chứa vật thể là bao nhiêu (P(obj))
  3. Class Probabilities: Các giá trị xác định vật thể đó thuộc loại nào (C(Text))
- Tuy nhiên nếu với bài toán 1 lớp thì thành phần thứ 3 có vẻ hơi dư thừa, vì vật thể đó luôn là vật thể trong 1 lớp đó. Ví dụ: Nếu bài toán của bạn chỉ có 1 lớp duy nhất (Text), thì rõ ràng nếu P(obj) báo "Có vật thể", vật thể đó HIỂN NHIÊN phải là Text. Việc tính thêm C(text) có vẻ như bị thừa thãi và lãng phí toán học. Do đó với YOLO v11 đã thay thế bằng điểm tin cậy, mô hình không còn hỏi "Có vật gì ở đây không?" nữa mà nó trực tiếp đánh giá trên nhánh phân loại (Classification Head) để trả lời thẳng câu hỏi: "Xác suất khung này chứa lớp A là bao nhiêu? Lớp B là bao nhiêu?"

I.2 Text recognition: CRNN
- Mô hình CRNN sẽ bao gồm:
  1. Feature Extraction: Trích xuất đặc trưng
  2. Sequence Modeling: sử dụng mạng RNN để feature map để nắm bắt mqh ngữ cảnh các ký tự
  3. Decoding: Sử dụng lớp CTC để dự đoán chuỗi ký tự đầu ra mà không cần căn chỉnh thời gian chính xác
 
<img width="493" height="391" alt="{7DF36148-41BA-434C-9F6E-984379F70BBA}" src="https://github.com/user-attachments/assets/0d5bdd5b-1ae4-4dd6-86ed-30786bb17f06" />
Hình 1: Kiến trúc CRNN với luồng xử lý từ trích xuất đặc trưng đến giải mã ký tự

