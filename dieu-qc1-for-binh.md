# Phiếu kiểm tra chéo (QC 1) — Bài gán nhãn phần tử đường

- **Người kiểm tra (Reviewer):** NguyenHoangDieu
- **Người được kiểm tra (Annotator):** NguyenTrongBinh
- **Ngày kiểm tra:** 2026-11-21
- **Vòng kiểm tra:** Vòng 1 (Revision 1)
- **Tệp đầu vào được kiểm tra:** `annotations_2.xml` (Task `d11-road-NguyenTrongBinh` — 28 ảnh: `A01–A16`, `B01–B12`)

---

## 1. Bảng đánh giá theo bộ tiêu chí QC 1

| Mã tiêu chí | Nội dung kiểm tra | Mức độ | Kết quả | Chi tiết lỗi & Mã ảnh cụ thể |
| :--- | :--- | :---: | :---: | :--- |
| **QC1-01** | Đủ 2 gói `.zip` (`front` & `fisheye`), không kèm ảnh, đủ 4 tag mỗi ảnh | **Nặng** | **KHÔNG ĐẠT** | 1. Đang gộp chung 28 ảnh (`A01–A16` và `B01–B12`) vào 1 file XML thay vì tách riêng 2 gói `binh-front.zip` (16 ảnh) và `binh-fisheye.zip` (12 ảnh).<br>2. Ảnh `B12_05885_MVR.png` bị bỏ trống hoàn toàn, chưa gán 4 tag (`camera=fisheye_right`, `timeofday`, `weather`, `source`). |
| **QC1-02** | Đủ vạch giới hạn làn xe chạy `L1` và `R1` | **Nặng** | **Đạt (Có ghi chú)** | Ảnh `A05_b2576c8c-2de20b8a.jpg` không có `L1`/`R1` do mặt đường thực tế không có vạch sơn kẻ làn (hợp lệ, cần ghi chú trong báo cáo). |
| **QC1-03** | Phân biệt đúng `drivable`: `direct` (1 làn xe chạy) và `alternative` (làn lân cận) | **Nặng** | **KHÔNG ĐẠT** | Ảnh `A16_b6f77fda-33d2260f.jpg`: Cả 3 polygon `drivable` đều gán `area_type = direct`. Hai polygon làn bên trái và bên phải cần sửa thành `alternative`. |
| **QC1-04** | Gán đúng `position` (`L1, R1, L2, R2, other`) của `lane` | **Chính** | **KHÔNG ĐẠT** | 1. Ảnh `A13_c179d309-b446fda3.jpg`: Vạch đứt nằm bên phải (`x = 1280 -> 751`) bị gán nhầm `position = L2` (phải sửa thành `R2`).<br>2. Ảnh `A16_b6f77fda-33d2260f.jpg`: Đoạn vạch đứt ở xa phía trên (`x = 720 -> 704`) bị gán nhầm `position = L2` (cần sửa thành `other`). |
| **QC1-05** | Không tách rời các nét của cùng 1 vạch đứt (`dashed`) | **Chính** | **Đạt** | Các cặp polyline trùng `position` trên `A04, A07, A08, A09, A11, A12, A14` là vạch kép (`double`) hoặc đoạn chuyển tiếp đổi kiểu (`solid` <-> `dashed`), đúng quy tắc. |
| **QC1-06** | Vạch kép (`double`) vẽ đủ 2 nét song song và đặt `kind = double` | **Chính** | **Đạt** | Các vạch kép trên `A04, A09, A11, A14` đã vẽ đủ 2 polyline song song và gán `kind = double`. |
| **QC1-07** | Vẽ đủ và khớp biên `road_curb` và `crosswalk` | **Chính** | **KHÔNG ĐẠT** | Ảnh `B12_05885_MVR.png` chưa vẽ nhãn `drivable`, `road_curb` và `crosswalk`. Các ảnh từ `A01` đến `B11` đã vẽ đầy đủ. |
| **QC1-08** | Logic `traffic_light`: `facing = side/back` thì `color = unknown` | **Chính** | **KHÔNG ĐẠT** | Đèn quay ngang (`facing = side`) nhưng gán `color = red` thay vì `unknown` tại 2 vị trí:<br>- `A14_ca04d99f-c1282bb7.jpg` (box `xtl=415.30, ytl=119.91`)<br>- `A16_b6f77fda-33d2260f.jpg` (box `xtl=852.50, ytl=244.47`) |
| **QC1-09** | Không vẽ chồng chéo / trùng lặp box `traffic_sign` | **Chính** | **KHÔNG ĐẠT** | Ảnh `A08_c0deebc1-16cfa791.jpg`: Có 2 box `traffic_sign` vẽ đè khít lên nhau tại tọa độ `(698.68, 182.59)` (`group = information` và `group = prohibitory`). Cần xóa bớt 1 box trùng. |
| **QC1-10** | Kích thước box tối thiểu (`width >= 8 px`, `height >= 8 px`) | **Nhẹ** | **KHÔNG ĐẠT** | Có 2 box `traffic_sign` có chiều cao nhỏ hơn 8 px:<br>- `A10_b6ff1331-f6d3fba8.jpg` (`xtl=440.57, ytl=232.03`, cao `7.5 px`)<br>- `A15_be85bd88-d849c034.jpg` (`xtl=651.06, ytl=369.38`, cao `6.0 px`) |
| **QC1-11** | Polyline trên ảnh `fisheye` đặt đủ điểm uốn theo độ cong ống kính | **Chính** | **KHÔNG ĐẠT** | Ảnh `B06_04068_MVL.png`: Polyline `lane` tại tọa độ `(552.53, 47.23)` mới có 3 điểm, chưa đủ điểm uốn theo cung méo fisheye (cần bổ sung >= 4–5 điểm). |
| **QC1-12** | Bật `edge_zone = true` cho đèn/biển nằm sát mép biên ảnh `fisheye` | **Nhẹ** | **Đạt** | Các đối tượng nằm sát biên ảnh fisheye trên `B02, B03, B04, B10` đã được bật `edge_zone = true`. |
| **QC1-13** | Không tự vẽ bịa nhãn khi hình ảnh không có hoặc không nhìn rõ | **Nặng** | **Đạt** | Không tự vẽ bịa vạch làn trên ảnh đường không có vạch (`A05`). |

---

## 2. Tổng hợp lỗi & Kết luận nghiệm thu Vòng 1

- **Tổng số lỗi phát hiện:**
  - **Lỗi Nặng:** 2 (`QC1-01`, `QC1-03`)
  - **Lỗi Chính:** 5 (`QC1-04`, `QC1-07`, `QC1-08`, `QC1-09`, `QC1-11`)
  - **Lỗi Nhẹ:** 1 (`QC1-10`)
- **Kết luận nghiệm thu:** **CHƯA ĐẠT — Yêu cầu Annotator sửa lại và bàn giao Vòng 2.**
- **Hành động yêu cầu đối với Annotator (`NguyenTrongBinh`):**
  1. Gán đầy đủ 4 tag (`camera = fisheye_right`) và toàn bộ nhãn (`drivable`, `road_curb`, `crosswalk`) cho ảnh `B12_05885_MVR.png`.
  2. Sửa toàn bộ các lỗi `Nặng` và `Chính` ở bảng trên (`A16`, `A13`, `A14`, `A08`, `B06`) và xóa 2 box `< 8 px` (`A10`, `A15`).
  3. Xuất file XML (không kèm ảnh), tách thành **2 gói `.zip` riêng biệt** (`binh-front.zip` gồm 16 ảnh `A01–A16` và `binh-fisheye.zip` gồm 12 ảnh `B01–B12`), sau đó chạy lệnh `road_check lint` để xác nhận 0 lỗi nặng trước khi gửi lại kiểm tra vòng 2.