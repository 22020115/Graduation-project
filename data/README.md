# 📦 Bộ Dữ Liệu Đám Mây Điểm 3D Cây Lúa ST25

Tài liệu mô tả chi tiết quy trình thu thập, tiền xử lý và cấu trúc bộ dữ liệu phục vụ nghiên cứu theo dõi sinh trưởng và trích xuất kiểu hình cây lúa.

---

## 🌾 1. Mẫu Sinh Học & Quy Trình Trồng Thực Nghiệm

- **Giống lúa:** ST25 (thu thập tại Vĩnh Phúc).
- **Thời gian thực nghiệm:** Từ tháng 11/2025 đến tháng 05/2026 trong phòng thí nghiệm (PTN).
- **Giá thể & Dinh dưỡng:** Sỏi nhẹ kết hợp giá thể tổng hợp, nuôi cấy theo phương pháp thủy canh cải tiến với công thức dinh dưỡng Hoagland chuẩn hóa; chế độ chiếu sáng LED 12h/ngày.
- **Bố trí thí nghiệm:** 3 mức mật độ (1, 2, 3 cây/chậu) trên 13 chậu, tổng cộng 26 cá thể cây.

---

## 🔬 2. Thiết Bị & Phương Pháp Thu Thập Dữ Liệu 3D

- **Thiết bị quét:** Máy quét LiDAR cầm tay **FARO Freestyle 2**.
  - **Độ chính xác:** $\pm 1\text{ mm}$.
  - **Dải quét hiệu dụng:** $0,4 - 5\text{ m}$.
- **Phương pháp thu thập:** Quét theo quỹ đạo vòng tròn $360^\circ$ quanh chậu cây kết hợp hệ thống bia mục tiêu (targets) cố định hệ tọa độ.
- **Quy mô dữ liệu:** 
  - Gồm **255 mẫu đám mây điểm** định dạng `.ply` (mỗi mẫu chứa khoảng 50.000 – 200.000 điểm).
  - Thu thập qua **20 phiên quét** trong 30 ngày (17/04 – 17/05/2026) bao phủ 3 giai đoạn sinh trưởng then chốt:
    1. **Kỳ 1 (17/04 - 27/04):** Ra hoa – Thụ phấn hoàn tất (88 mẫu) — Chiều cao đạt đỉnh, lá cờ phát triển.
    2. **Kỳ 2 (28/04 - 07/05):** Hạt vào chắc sữa / Milk stage (89 mẫu) — Bông bắt đầu ngả cong, chiều cao ổn định.
    3. **Kỳ 3 (08/05 - 17/05):** Chín sáp / Dough stage (78 mẫu) — Bông cong rõ, lá bắt đầu ngả vàng.

---

## 📏 3. Dữ Liệu Đối Chứng Thực Tế (Ground Truth)

- **Chiều cao cây:** Đo bằng thước thủ công từ mép chậu đến đỉnh lá cao nhất.
- **Số nhánh (dảnh lúa):** Đếm trực tiếp từng nhánh bằng mắt thường.
- **Tính nhất quán:** Toàn bộ dữ liệu đối chứng được thực hiện bởi **1 người duy nhất** ngay sau mỗi phiên quét LiDAR để loại bỏ sai số chủ quan giữa các người đo.

---

## 🏷️ 4. Tiền Xử Lý & Gán Nhãn Ngữ Nghĩa

1. **Khử nhiễu sơ bộ:** Xử lý bằng phần mềm chuyên dụng đi kèm FARO.
2. **Gán nhãn bằng CloudCompare:**
   - **Lớp 0 (POT):** Chậu nhựa, giá thể sỏi nhẹ.
   - **Lớp 1 (PLANT):** Toàn bộ thân, lá, bông của cây lúa.
3. **Đặc trưng đầu vào (7 chiều):**
   - Tọa độ không gian: $(X, Y, Z)$
   - Chiều cao chuẩn hóa: $h\_rel$ (tính từ gốc chậu)
   - Vector pháp tuyến bề mặt: $(n_x, n_y, n_z)$ ước lượng qua lân cận k-NN ($k=20$).

---

## 📥 5. Hướng Dẫn Tải & Cấu Trúc Thư Mục

Bộ dữ liệu được lưu trữ tại Kaggle:
- **Link tải:** [Rice 3D Segmentation Dataset (Label_Pot_Plant)](https://www.kaggle.com/datasets/haquanghung/rice-3d-segmentation-dataset)

Sau khi giải nén, đặt thư mục `Label_Pot_Plant` vào trong thư mục `data/`:
```text
data/
└── Label_Pot_Plant/
    ├── C1.1_26410.ply
    ├── C1.1_26416.ply
    ├── C1.1_26423.ply
    └── ...
```
