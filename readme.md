# Nguyễn Văn An - 24810320020

# I. PHẦN LÝ THUYẾT VÀ CÂU HỎI NGẮN

## Câu 1. Trình bày sự khác nhau giữa Value Types và Reference Types trong C# về cơ chế lưu trữ vùng nhớ

Trong C#, **Value Types (kiểu giá trị)** là các kiểu dữ liệu mà biến lưu trực tiếp giá trị của nó. Khi một biến kiểu giá trị được gán cho biến khác, giá trị sẽ được sao chép sang một vùng dữ liệu riêng, vì vậy việc thay đổi biến mới không ảnh hưởng đến biến ban đầu.

Các kiểu giá trị thường gặp gồm: `int`, `float`, `double`, `bool`, `char`, `struct`, `enum`,...

**Reference Types (kiểu tham chiếu)** là các kiểu dữ liệu mà biến lưu tham chiếu đến một đối tượng trong bộ nhớ. Khi một biến tham chiếu được gán cho biến khác, tham chiếu được sao chép, vì vậy hai biến có thể cùng tham chiếu đến một đối tượng. Khi đối tượng thay đổi thì cả hai biến đều quan sát được sự thay đổi đó.

Các kiểu tham chiếu thường gặp gồm: `class`, `array`, `string`, `object`, `interface`, `delegate`,...

Về vùng nhớ, biến cục bộ kiểu giá trị thường liên quan đến **Stack**, trong khi các đối tượng của kiểu tham chiếu thường được cấp phát trên **Heap**. Stack có tốc độ truy xuất nhanh và thường được giải phóng khi phương thức kết thúc. Heap dùng để lưu các đối tượng và được quản lý bởi **Garbage Collector** của .NET.

Tuy nhiên, không nên hiểu tuyệt đối rằng Value Type luôn nằm trên Stack. Nếu một Value Type là thành phần của một đối tượng thì nó sẽ được lưu cùng đối tượng đó trên Heap.

### Tóm lại

- **Value Type:** lưu trực tiếp giá trị và sao chép giá trị khi gán.
- **Reference Type:** lưu tham chiếu đến đối tượng và sao chép tham chiếu khi gán.

---

## Câu 2. Tính năng Init-only Properties (`init`) trong C# 9/10 khác gì so với thuộc tính có `set` thông thường?

Trong C#, thuộc tính sử dụng `set` cho phép giá trị được thay đổi sau khi đối tượng đã được khởi tạo. Điều này phù hợp với những dữ liệu có thể thay đổi trong quá trình sử dụng chương trình.

Trong khi đó, `init` được giới thiệu từ C# 9 và chỉ cho phép gán giá trị cho thuộc tính trong quá trình khởi tạo đối tượng. Sau khi đối tượng đã được tạo xong, thuộc tính sử dụng `init` không thể được gán lại theo cách thông thường.

### Sự khác nhau chính

- `set`: cho phép thay đổi giá trị trong suốt vòng đời của đối tượng.
- `init`: chủ yếu cho phép gán giá trị tại thời điểm khởi tạo đối tượng.

`init` thường được sử dụng đối với những thông tin cần được cố định sau khi tạo, chẳng hạn như mã sinh viên, mã nhân viên, mã đơn hàng, ID hoặc ngày tạo dữ liệu.

Việc sử dụng `init` giúp hạn chế việc thay đổi những dữ liệu quan trọng ngoài ý muốn.

---

## Câu 3. Phân biệt phương thức `virtual` ở lớp cha và phương thức `override` ở lớp con khi triển khai tính đa hình

Trong C#, `virtual` và `override` được sử dụng để hỗ trợ tính đa hình trong lập trình hướng đối tượng.

### `virtual`

Từ khóa `virtual` được khai báo ở **lớp cha**. Nó cho phép một phương thức của lớp cha có thể được lớp con ghi đè và thay đổi cách thực hiện.

### `override`

Từ khóa `override` được khai báo ở **lớp con**. Nó dùng để định nghĩa lại phương thức đã được khai báo là `virtual` ở lớp cha.

### Tóm lại

- `virtual`: cho phép lớp con ghi đè phương thức.
- `override`: thực hiện việc ghi đè phương thức tại lớp con.

Nhờ cơ chế này, cùng một phương thức có thể có cách thực hiện khác nhau tùy theo đối tượng thực tế được sử dụng. Đây là một biểu hiện của tính đa hình lúc chạy (**Runtime Polymorphism**) trong C#.

Có thể ghi nhớ ngắn gọn:

> **virtual = cho phép ghi đè**  
> **override = thực hiện ghi đè**

---

## Câu 4. Tại sao một thành phần được khai báo là `static` trong lớp lại không thể truy xuất thông qua một thể hiện được tạo bằng toán tử `new`?

Trong C#, một thành phần được khai báo với từ khóa `static` là thành phần thuộc về **lớp**, không thuộc riêng về từng đối tượng được tạo ra từ lớp đó.

Các thành phần thông thường không có `static` được gọi là thành phần của đối tượng. Mỗi đối tượng có dữ liệu riêng và muốn truy cập các thành phần này thì cần tạo đối tượng bằng toán tử `new`.

Ngược lại, thành phần `static` chỉ tồn tại **một bản dùng chung cho toàn bộ lớp**. Do đó, việc truy cập thành phần `static` được thực hiện thông qua **tên lớp** thay vì thông qua một đối tượng cụ thể.

### Cú pháp đúng

```csharp
TenLop.TenThanhPhan
