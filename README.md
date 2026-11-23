# PCB-8bit

Dự án thiết kế mạch in (PCB) cho bộ cộng 8-bit, được xây dựng từ các khối **full adder 1-bit** ghép nối tiếp, kèm theo mạch **giao tiếp (interface)** để nhập dữ liệu và hiển thị kết quả.

## Mục lục

- [Giới thiệu](#giới-thiệu)
- [Cấu trúc thư mục](#cấu-trúc-thư-mục)
- [Nguyên lý hoạt động](#nguyên-lý-hoạt-động)
- [Công cụ sử dụng](#công-cụ-sử-dụng)

- [Hướng dẫn sử dụng](#hướng-dẫn-sử-dụng)
- [Hình ảnh](#hình-ảnh)
- [Tác giả](#tác-giả)


## Giới thiệu

Mục tiêu của dự án là thiết kế và chế tạo một bộ cộng 8-bit trên PCB, theo hướng đi từ khối nhỏ đến hệ thống hoàn chỉnh:

1. Thiết kế và kiểm tra khối full adder 1-bit.
2. Ghép 8 khối full adder thành bộ cộng 8-bit (kiểu ripple-carry).
3. Thiết kế mạch interface để nhập hai toán hạng và quan sát kết quả.

## Cấu trúc thư mục

```
PCB-8bit/
├── fulladder1bit/
│   └── 1bit/          # Thiết kế schematic + PCB của khối full adder 1-bit
└── interface/         # Thiết kế mạch giao tiếp (nhập liệu / hiển thị)
```

| Thư mục | Mô tả |
| --- | --- |
| `fulladder1bit/1bit` | Khối full adder 1-bit, là đơn vị cơ bản để xây dựng bộ cộng 8-bit |
| `interface` | Mạch giao tiếp giữa người dùng và bộ cộng |

## Nguyên lý hoạt động

Mỗi khối full adder 1-bit nhận vào 3 tín hiệu: `A`, `B` và `Cin` (số nhớ từ bit trước), cho ra `Sum` và `Cout` (số nhớ sang bit sau).

**Công thức logic:**

```
Sum  = A ⊕ B ⊕ Cin
Cout = (A · B) + (Cin · (A ⊕ B))
```

**Bảng chân trị:**

| A | B | Cin | Sum | Cout |
|:-:|:-:|:---:|:---:|:----:|
| 0 | 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 | 0 |
| 0 | 1 | 0 | 1 | 0 |
| 0 | 1 | 1 | 0 | 1 |
| 1 | 0 | 0 | 1 | 0 |
| 1 | 0 | 1 | 0 | 1 |
| 1 | 1 | 0 | 0 | 1 |
| 1 | 1 | 1 | 1 | 1 |

**Bộ cộng 8-bit (ripple-carry):** `Cout` của khối thứ *i* được nối vào `Cin` của khối thứ *i+1*. `Cin` của khối đầu tiên nối mức 0.

```
A7 B7      A1 B1      A0 B0
 │  │       │  │       │  │
┌▼──▼┐     ┌▼──▼┐     ┌▼──▼┐
│ FA │ ... │ FA │◄────│ FA │◄── Cin = 0
└┬──┬┘     └┬──┬┘     └┬──┬┘
 │  │       │  │       │  │
Cout S7     C1 S1      C0 S0
```

## Công cụ sử dụng

- Phần mềm thiết kế PCB: `KiCad `

## Hướng dẫn sử dụng

**1. Tải mã nguồn**

```bash
git clone https://github.com/giatan0601/PCB-8bit.git
cd PCB-8bit
```

**2. Mở thiết kế**

- Khối full adder 1-bit: mở project trong thư mục `fulladder1bit/1bit`.
- Mạch giao tiếp: mở project trong thư mục `interface`.

**3. Xuất file sản xuất (Gerber)**

Xuất file Gerber và file khoan từ phần mềm thiết kế, sau đó gửi cho nhà sản xuất PCB.

**4. Kiểm tra mạch**

Cấp nguồn `5V`, đặt các giá trị `A`, `B`, `Cin` và đối chiếu `Sum`, `Cout` với bảng chân trị ở trên.

## Hình ảnh

<img width="1042" height="712" alt="image" src="https://github.com/user-attachments/assets/d1c37849-01e5-43aa-9d49-cc9269abf98b" />
<img width="758" height="761" alt="image" src="https://github.com/user-attachments/assets/35310305-00a8-441f-8e3e-143a06df89a1" />
<img width="1057" height="687" alt="image" src="https://github.com/user-attachments/assets/d9d7dcc1-ff8f-411c-8e08-64e951ebb69b" />
<img width="546" height="542" alt="image" src="https://github.com/user-attachments/assets/874212eb-3796-4561-b1ee-938f2d943d16" />


## Tác giả

- **giatan0601** – [GitHub](https://github.com/giatan0601)

