# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 2A202600147
**Name:** Nguyen Duc Cuong
**Date:** 2026-04-15

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200. | 9/10 | Kết quả hợp lý: Laptop có giá cao nhất trong nhóm Electronics (Laptop 1200, Monitor 300). |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 1/10 | Dữ liệu bất thường (outlier giá cực lớn, duplicate ID, kiểu dữ liệu sai) gây khuyến nghị vô lý. |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Khi sử dụng garbage data, Agent vẫn dùng logic tìm sản phẩm electronics có `price` lớn nhất,
nhưng dữ liệu đầu vào đã bị nhiễm lỗi nên kết quả bị lệch nghiêm trọ ng. Cụ thể,
record "Nuclear Reactor" có giá 999999 là một outlier phi thực tế, làm model ưu tiên chọn sai.
Bộ dữ liệu cũng có duplicate ID (ID=1 lặp lại), kiểu dữ liệu sai (`price = ten dollars`),
và giá trị thiếu (ID rỗng, category rỗng, price = 0). Các vấn đề này làm giảm độ tin cậy của
knowledge base, gây nhiều noise trong retrieval và suy luận. Kết quả là Agent có thể đưa ra
khuyến nghị "có vẻ đúng theo công thức" nhưng sai theo ngữ cảnh thực tế kinh doanh.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** (Dong y hay khong? Giai thich ngan gon.)

Tôi đồng ý. Prompt tốt không thể bù đắp cho dữ liệu kém chất lượng.
Trong thí nghiệm này, cùng một câu hỏi và cùng một logic Agent, nhưng kết quả khác nhau rõ rệt
chỉ vì chất lượng dữ liệu đầu vào. Vì vậy, data validation và data observability là điều kiện
bắt buộc trước khi tối ưu prompt hoặc mô hình.
