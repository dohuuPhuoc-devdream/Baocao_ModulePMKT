# PicoCorp Accounting

Ứng dụng kế toán và báo cáo trên ASP.NET Framework Web Forms, C# và SQL Server.

## Phân hệ và chức năng

- **Hệ thống:** thông tin chung, đơn vị cơ sở, tài khoản và phân quyền.
- **Tổng hợp:** phiếu kế toán tổng hợp, bảng cân đối kế toán.
- **Phải thu:** hóa đơn bán hàng, khách hàng, báo cáo công nợ khách hàng.
- **Phải trả:** hóa đơn mua hàng trong nước, nhà cung cấp, báo cáo công nợ nhà cung cấp.
- **Bán hàng:** đơn hàng và hóa đơn bán hàng, báo cáo bán hàng và phân tích doanh thu.
- **Mua hàng:** đơn hàng mua, phiếu nhập mua, báo cáo nhập/mua hàng và phân tích mua hàng.
- **Tồn kho:** phiếu nhập/xuất, danh mục hàng hóa, báo cáo nhập, xuất và nhập-xuất-tồn.

Chứng từ hỗ trợ lưu nháp và ghi sổ theo nghiệp vụ. Phiếu nhập cập nhật tồn kho; hóa đơn mua liên kết phiếu nhập và cập nhật công nợ. Hóa đơn bán liên kết xuất kho. Hệ thống kiểm tra số lượng tồn và xử lý ghi sổ trong giao dịch cơ sở dữ liệu. Báo cáo truy vấn dữ liệu theo đơn vị, khoảng thời gian và điều kiện lọc; kết quả có thể in hoặc kết xuất PDF/Excel. Danh mục hỗ trợ nhập và xuất Excel.

Mỗi đơn vị sử dụng kho mặc định `KHO01`. Số dư, chứng từ và báo cáo được quản lý theo đơn vị đang chọn.

## Yêu cầu

- Windows với .NET Framework 4.8 Developer Pack.
- SQL Server và tiện ích dòng lệnh `sqlcmd`.
- Visual Studio 2022 với công cụ phát triển ASP.NET và IIS Express.
- Kết nối NuGet để khôi phục các thư viện được khai báo trong `packages.config`.

## Cài đặt lần đầu

Mở PowerShell tại thư mục này và chạy:

```powershell
.\tools\restore-packages.ps1
sqlcmd -S '.\SQLEXPRESS' -E -C -b -l 10 -f 65001 -i database\setup.sql
.\tools\provision-admin.ps1
```

Lệnh SQL tạo cơ sở dữ liệu `ReportingModuleDemo`, áp dụng schema và dữ liệu khởi tạo. Script provisioning yêu cầu nhập tên đăng nhập, tên hiển thị và mật khẩu quản trị; mật khẩu được nhập trực tiếp, không lưu trong thư mục sản phẩm.

Nếu SQL Server dùng tên instance hoặc tài khoản khác, truyền chuỗi kết nối vào script provisioning:

```powershell
.\tools\provision-admin.ps1 -ConnectionString 'Data Source=SERVER\INSTANCE;Initial Catalog=ReportingModuleDemo;Integrated Security=True;Encrypt=True;TrustServerCertificate=True;Connect Timeout=10'
```

## Chạy ứng dụng

```powershell
.\tools\run-local.ps1
```

Mở `http://localhost:8080/Default.aspx` trong trình duyệt. Đăng nhập bằng tài khoản quản trị vừa tạo. Nhấn `Q` trong cửa sổ PowerShell để dừng IIS Express. Script nhận tùy chọn cổng, ví dụ `.\tools\run-local.ps1 -Port 8090`.

