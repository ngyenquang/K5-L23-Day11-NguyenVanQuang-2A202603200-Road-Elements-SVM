# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): phamtienphat        Người kiểm (học viên): quang  
Ngày: 2026-11-21                          Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): phamtienphat-front.zip, phamtienphat-fisheye.zip (revision 1; sha256 khớp manifest)  
Số ảnh kiểm: 6 (A05, A06, A09, A12, B04, B06) (+ 0 ảnh thêm, ghi riêng)   Số nhãn đã kiểm (shape + tag): 60  

Chi tiết số nhãn: A05 = 6, A06 = 16, A09 = 9, A12 = 12, B04 = 9, B06 = 8 (mỗi ảnh gồm 4 tag).

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 12 | 0 (4 ca chờ coach, xem "Ca mơ hồ") | nặng |
| QC1-03 position | sai thuộc tính / thừa | 6 | 1 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 8 | 1 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 6 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 6 | 1 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 7 | 2 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 9 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 16 | 1 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 7 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 9 | 0 | chính |
| QC1-12 file | lỗi file | 2 | 0 | nhẹ / nặng |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-03 | B06 | lane (position = other, polyline dọc chân dải bê tông giữa đường) | nặng | Polyline bám mép dải bê tông, giống mép đường hơn là vạch sơn. Nếu là mép đường thì phải là road_curb, lane này là nhãn thừa. |
| 2 | QC1-07 | A05 | drivable (area_type = direct) | chính | Polygon direct mở sang phải tới khoảng x = 1150 sát dải xe đỗ ven lề; guideline loại dải đỗ khỏi direct. |
| 3 | QC1-07 | A12 | drivable (area_type = direct) | chính | Polygon dừng ở vạch ngựa vạn, thiếu đoạn đường phía xa; ở A06 direct đi qua vạch ngựa vạn nên không nhất quán. |
| 4 | QC1-06 | A12 | lane (position = L1) | chính | Polyline bám vạch màu vàng/cam nhưng gán color = white. |
| 5 | QC1-09 | A12 | traffic_sign (mép trái ảnh, mũi tên một chiều) | chính | Gán group = prohibitory; biển một chiều cùng loại bên phải ảnh gán mandatory, nên phải là mandatory. |
| 6 | QC1-04 | B04 | lane (position = R1) | chính | Polyline chỉ là đoạn ngắn ở xa, không kéo về phía gần xe; vạch làn bus ở rìa trái còn dài hơn và trông là vạch liền chứ không phải đứt. |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A05, A06, A09, A12 | QC1-02 ở 4 ảnh này (A05 thiếu L1 và R1, A06 thiếu L1, A09 và A12 thiếu R1): có xác nhận miễn vì ảnh không thấy vạch bên đó không? Lint báo 7 cảnh báo trên cả lô. | |
| A06 | Polyline R1 ở góc dưới phải có phải là vạch sơn không, hay là mép đường? | |
| B04 | Hộp biển (edge_zone = true) và hộp đèn người đi bộ (edge_zone = false) nằm sát nhau gần ngưỡng 80 % bán kính; cần tính từ tâm vòng ảnh để chốt. | |

## Quyết định
Lỗi nặng: 1   Lỗi chính: 6 / 60 nhãn = 10 %   Lỗi nhẹ: 0   Ca chờ lead: 3  
Quyết định (Release / Hold / Rework): Rework  
Lý do (theo luật của phiếu): Có 1 lỗi nặng (QC1-03 ở B06) nên Rework. Ngoài ra tỉ lệ lỗi chính 6 / 60 = 10 % vượt ngưỡng 5 %, nên dù lỗi nặng ở B06 được xác nhận là nhãn đúng thì lô vẫn Rework. Ba ca mơ hồ không làm đổi kết luận.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](docs/qc_severity_road_v1.0.md).
