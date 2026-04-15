[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23574120&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** cuong111103hd@gmail.com
**Name:** Nguyễn Đức Cường
**Student ID:** cuong111103hd

---

## Mo ta

Tôi đã hoàn thành ETL pipeline gồm 4 bước Extract -> Validate -> Transform -> Load.
Pipeline đọc dữ liệu từ `raw_data.json`, loại bỏ record lỗi (price <= 0 hoặc category rỗng),
chuẩn hóa category về Title Case, tính thêm `discounted_price` (giảm 10%),
và ghi kết quả ra `processed_data.csv` kèm cột timestamp `processed_at`.
Ngoài ra, tôi đã chạy stress test Agent với clean data và garbage data
để đánh giá tác động của chất lượng dữ liệu đến kết quả trả lời.

---

## Cach chay (How to Run)

### Prerequisites
```bash
python3 -m venv venv
source venv/bin/activate
pip install pandas pytest
```

### Chay ETL Pipeline
```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)
```bash
python agent_simulation.py
```

Script trên sẽ tự động chạy 2 scenario:
- Clean Data: `processed_data.csv`
- Garbage Data: `garbage_data.csv`

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Ket qua

- Tổng record đầu vào (`raw_data.json`): 5
- Record hợp lệ sau validate: 3
- Record bị loại: 2
	- ID 3: `price <= 0`
	- ID 4: `category` rỗng
- File output tạo thành công: `processed_data.csv` với 3 dòng dữ liệu
- Agent simulation:
	- Clean Data: Agent chọn Laptop ($1200) là sản phẩm electronics tốt nhất
	- Garbage Data: Agent chọn Nuclear Reactor ($999999), cho thấy dữ liệu rác có thể dẫn đến khuyến nghị sai lệch
