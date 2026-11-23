# PCB-8bit

Dự án thiết kế mạch in (PCB) cho bộ cộng 8-bit, được xây dựng từ các khối **full adder 1-bit** ghép nối tiếp, kèm theo mạch **giao tiếp (interface)** để nhập dữ liệu và hiển thị kết quả.

## Mục lục

- [Giới thiệu](#giới-thiệu)
- [Cấu trúc thư mục](#cấu-trúc-thư-mục)
- [Nguyên lý hoạt động](#nguyên-lý-hoạt-động)
- [Công cụ sử dụng](#công-cụ-sử-dụng)
- [Danh sách linh kiện](#danh-sách-linh-kiện)
- [Hướng dẫn sử dụng](#hướng-dẫn-sử-dụng)
- [Hình ảnh](#hình-ảnh)
- [Tác giả](#tác-giả)
- [Giấy phép](#giấy-phép)

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

- Phần mềm thiết kế PCB: `[KiCad / Altium / EasyEDA / ...]`
- Mô phỏng: `[Proteus / LTspice / Multisim / ...]`

> Cập nhật lại mục này theo công cụ bạn thực sự dùng.

## Danh sách linh kiện

| Linh kiện | Số lượng | Ghi chú |
| --- | :---: | --- |
| `[IC / cổng logic]` | `[?]` | `[?]` |
| `[LED hiển thị]` | `[?]` | `[?]` |
| `[Công tắc / DIP switch]` | `[?]` | `[?]` |
| `[Điện trở]` | `[?]` | `[?]` |

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

<!-- Thêm ảnh schematic, layout PCB và mạch thực tế vào đây -->
<!-- ![Schematic](images/schematic.png) -->
<!-- ![PCB layout](images/pcb.png) -->

## Tác giả

- **giatan0601** – [GitHub](https://github.com/giatan0601)

