# Web Bán Sách Trực Tuyến

## 1. Khách Hàng

- **1.1. Đăng nhập**
  - **Front-end**:
    - Hiển thị form đăng nhập với các trường (username, password).
    - Người dùng nhập thông tin và nhấn nút "Đăng nhập".
    - Khi nhấn, Front-end gửi thông tin người dùng (username, password) đến **Back-end** qua một POST request.
  - **Tham số truyền/nhận**: Không có tham số truyền.
  - **Back-end**:
    - Nhận thông tin từ Front-end và thực hiện truy vấn để kiểm tra tài khoản (kiểm tra trong bảng `users`).
    - Nếu tài khoản hợp lệ, tạo một session hoặc token và trả về cho Front-end.
    - **SQL**: `SELECT * FROM users WHERE username = ? AND password = ?`
    - Trả về thông tin đăng nhập thành công hoặc lỗi nếu không hợp lệ.
  - **Kết quả**:
    - Nếu thành công: Cung cấp session/token để người dùng duy trì trạng thái đăng nhập.
    - Nếu thất bại: Gửi thông báo lỗi về Front-end (ví dụ: "Sai username hoặc password").

- **1.2. Đăng ký**
  - **Front-end**:
    - Hiển thị form đăng ký yêu cầu nhập (username, email, password).
    - Kiểm tra validation dữ liệu đầu vào (kiểm tra username chưa tồn tại, email hợp lệ, mật khẩu đủ mạnh).
    - Sau khi kiểm tra, Front-end gửi thông tin tới **Back-end** qua một POST request.
  - **Tham số truyền/nhận**: 
    - **Truyền**: username, password, email.
  - **Back-end**:
    - Nhận thông tin từ Front-end và kiểm tra sự tồn tại của username trong cơ sở dữ liệu.
    - Nếu chưa tồn tại, lưu thông tin người dùng mới vào cơ sở dữ liệu và trả về kết quả.
    - **SQL**: `INSERT INTO users (username, password, email) VALUES (?, ?, ?)`
  - **Kết quả**:
    - Nếu thành công: Trả về thông báo đăng ký thành công và có thể tự động đăng nhập hoặc yêu cầu người dùng đăng nhập.
    - Nếu thất bại: Gửi lỗi về Front-end (ví dụ: "Username đã tồn tại").

- **1.3. Tìm kiếm sản phẩm**
  - **Front-end**:
    - Hiển thị thanh tìm kiếm cho phép người dùng nhập từ khóa.
    - Khi người dùng nhập từ khóa và nhấn tìm kiếm, Front-end gửi từ khóa (search_query) đến **Back-end** qua một GET request.
  - **Tham số truyền/nhận**: 
    - **Truyền**: search_query (từ khóa tìm kiếm).
  - **Back-end**:
    - Nhận từ khóa từ Front-end và thực hiện truy vấn để tìm các sản phẩm phù hợp.
    - **SQL**: `SELECT * FROM products WHERE name LIKE ?`
    - Trả về danh sách sản phẩm phù hợp với từ khóa tìm kiếm.
  - **Kết quả**:
    - Nếu thành công: Trả về danh sách các sản phẩm tìm thấy để hiển thị trên giao diện người dùng.
    - Nếu không có kết quả: Hiển thị thông báo "Không tìm thấy sản phẩm".

- **1.4. Thêm sản phẩm vào giỏ hàng**
  - **Front-end**:
    - Hiển thị nút "Thêm vào giỏ hàng" bên cạnh mỗi sản phẩm.
    - Khi người dùng nhấn nút, Front-end gửi thông tin sản phẩm (product_id, quantity) đến **Back-end** qua một POST request.
  - **Tham số truyền/nhận**: 
    - **Truyền**: product_id, quantity.
  - **Back-end**:
    - Nhận thông tin sản phẩm và người dùng từ Front-end.
    - Kiểm tra nếu sản phẩm tồn tại và thêm sản phẩm vào giỏ hàng của người dùng trong cơ sở dữ liệu.
    - **SQL**: `INSERT INTO cart (user_id, product_id, quantity) VALUES (?, ?, ?)`
  - **Kết quả**:
    - Nếu thành công: Trả về thông báo thành công và cập nhật giỏ hàng.
    - Nếu thất bại: Gửi lỗi (ví dụ: sản phẩm không tồn tại hoặc giỏ hàng đầy).

- **1.5. Cập nhật giỏ hàng**
  - **Front-end**:
    - Hiển thị giỏ hàng với các sản phẩm và số lượng.
    - Người dùng có thể thay đổi số lượng sản phẩm trong giỏ hàng.
    - Sau khi thay đổi, Front-end gửi yêu cầu cập nhật số lượng đến **Back-end** qua một PUT request.
  - **Tham số truyền/nhận**: 
    - **Truyền**: cart_id, new_quantity.
  - **Back-end**:
    - Nhận yêu cầu từ Front-end và cập nhật số lượng sản phẩm trong giỏ hàng.
    - **SQL**: `UPDATE cart SET quantity = ? WHERE user_id = ? AND product_id = ?`
  - **Kết quả**:
    - Nếu thành công: Cập nhật giỏ hàng và trả về thông báo thành công.
    - Nếu không thành công: Gửi lỗi (ví dụ: giỏ hàng không tồn tại).

- **1.6. Xóa sản phẩm trong giỏ hàng**
  - **Front-end**:
    - Hiển thị danh sách sản phẩm trong giỏ hàng với nút "Xóa" cạnh mỗi sản phẩm.
    - Khi người dùng nhấn nút "Xóa", Front-end gửi yêu cầu xóa sản phẩm tới **Back-end** qua một DELETE request.
  - **Tham số truyền/nhận**: 
    - **Truyền**: product_id.
  - **Back-end**:
    - Nhận yêu cầu xóa sản phẩm và xóa sản phẩm khỏi giỏ hàng của người dùng.
    - **SQL**: `DELETE FROM cart WHERE user_id = ? AND product_id = ?`
  - **Kết quả**:
    - Nếu thành công: Xóa sản phẩm khỏi giỏ hàng và trả về thông báo thành công.
    - Nếu thất bại: Gửi lỗi (ví dụ: sản phẩm không tồn tại trong giỏ hàng).
## 2. Quản Trị Viên

### 2.1. **Đăng nhập**
  - **Front-end**:
    - Hiển thị form đăng nhập với các trường (username, password).
    - Khi người quản trị nhập thông tin và nhấn "Đăng nhập", Front-end gửi thông tin đến **Back-end** qua một POST request.
  - **Tham số truyền/nhận**: Không có tham số truyền.
  - **Back-end**:
    - Kiểm tra tài khoản và mật khẩu quản trị viên.
    - Nếu tài khoản hợp lệ, trả về session hoặc token để quản trị viên duy trì đăng nhập.
    - **SQL**: `SELECT * FROM users WHERE username = ? AND password = ? AND role = 'admin'`
  - **Kết quả**:
    - Nếu thành công: Quản trị viên được cấp quyền truy cập vào hệ thống.
    - Nếu thất bại: Gửi lỗi về Front-end (ví dụ: "Sai username hoặc password").
### 2.2. **Quản lý sách**
  - **Thêm sách**
    - **Front-end**:
      - Hiển thị form nhập thông tin sách (title, author, price, category).
      - Người quản trị nhập thông tin và nhấn "Thêm sách".
      - Gửi thông tin sản phẩm (title, author, price, category_id) đến **Back-end** qua POST request.
    - **Tham số truyền/nhận**: 
      - **Truyền**: title, author, price, category_id.
    - **Back-end**:
      - Lưu thông tin sách mới vào cơ sở dữ liệu.
      - **SQL**: `INSERT INTO books (title, author, price, category_id) VALUES (?, ?, ?, ?)`
    - **Kết quả**:
      - Nếu thành công: Trả về thông báo "Sách đã được thêm".
      - Nếu thất bại: Gửi lỗi (ví dụ: thông tin không hợp lệ).

  - **Sửa sách**
    - **Front-end**:
      - Hiển thị form sửa thông tin sách đã có với các trường đã điền sẵn.
      - **Link truyền ID**: `/edit-book?id=book_id`
      - Sau khi chỉnh sửa, người quản trị nhấn "Cập nhật", Front-end gửi thông tin cập nhật (book_id, title, author, price, category_id) đến **Back-end**.
    - **Tham số truyền/nhận**: 
      - **Truyền**: book_id, title, author, price, category_id.
    - **Back-end**:
      - Cập nhật thông tin sách trong cơ sở dữ liệu.
      - **SQL**: `UPDATE books SET title = ?, author = ?, price = ?, category_id = ? WHERE book_id = ?`
    - **Kết quả**:
      - Nếu thành công: Trả về thông báo "Sách đã được cập nhật".
      - Nếu thất bại: Gửi lỗi (ví dụ: thông tin không hợp lệ).

  - **Xóa sách**
    - **Front-end**:
      - Hiển thị danh sách sách với nút "Xóa" bên cạnh mỗi sách.
      - Khi người quản trị nhấn nút "Xóa", Front-end gửi yêu cầu xóa sản phẩm (book_id) tới **Back-end** qua một DELETE request.
    - **Tham số truyền/nhận**: 
      - **Truyền**: book_id.
    - **Back-end**:
      - Xóa sách khỏi cơ sở dữ liệu.
      - **SQL**: `DELETE FROM books WHERE book_id = ?`
    - **Kết quả**:
      - Nếu thành công: Trả về thông báo "Sách đã được xóa".
      - Nếu thất bại: Gửi lỗi (ví dụ: sản phẩm không tồn tại).

### 2.3. **Quản lý danh mục sản phẩm**
  - **Thêm danh mục**
    - **Front-end**:
      - Hiển thị form nhập thông tin danh mục (category_name).
      - Người quản trị nhập thông tin và nhấn "Thêm danh mục".
      - Gửi thông tin danh mục (category_name) đến **Back-end** qua POST request.
    - **Tham số truyền/nhận**: 
      - **Truyền**: category_name.
    - **Back-end**:
      - Lưu thông tin danh mục mới vào cơ sở dữ liệu.
      - **SQL**: `INSERT INTO categories (category_name) VALUES (?)`
    - **Kết quả**:
      - Nếu thành công: Trả về thông báo "Danh mục đã được thêm".
      - Nếu thất bại: Gửi lỗi (ví dụ: tên danh mục đã tồn tại).

  - **Sửa danh mục**
    - **Front-end**:
      - Hiển thị danh sách các danh mục và nút "Sửa" bên cạnh mỗi danh mục.
      - Khi người quản trị nhấn "Sửa", hiển thị form chỉnh sửa và gửi thông tin danh mục mới (category_id, new_category_name) tới **Back-end** qua PUT request.
    - **Tham số truyền/nhận**: 
      - **Truyền**: category_id, new_category_name.
    - **Back-end**:
      - Cập nhật thông tin danh mục trong cơ sở dữ liệu.
      - **SQL**: `UPDATE categories SET category_name = ? WHERE category_id = ?`
    - **Kết quả**:
      - Nếu thành công: Trả về thông báo "Danh mục đã được cập nhật".
      - Nếu thất bại: Gửi lỗi (ví dụ: tên danh mục không hợp lệ).

  - **Xóa danh mục**
    - **Front-end**:
      - Hiển thị danh sách các danh mục với nút "Xóa" bên cạnh mỗi danh mục.
      - Khi người quản trị nhấn nút "Xóa", Front-end gửi yêu cầu xóa danh mục (category_id) tới **Back-end** qua DELETE request.
    - **Tham số truyền/nhận**: 
      - **Truyền**: category_id.
    - **Back-end**:
      - Xóa danh mục khỏi cơ sở dữ liệu.
      - **SQL**: `DELETE FROM categories WHERE category_id = ?`
    - **Kết quả**:
      - Nếu thành công: Trả về thông báo "Danh mục đã được xóa".
      - Nếu thất bại: Gửi lỗi (ví dụ: danh mục không tồn tại).
### 2.4. **Quản lý đơn hàng**
  - **Hiển thị danh sách đơn hàng**
    - **Front-end**:
      - Hiển thị danh sách đơn hàng bao gồm thông tin khách hàng, sản phẩm đã đặt, số lượng, trạng thái đơn hàng.
      - Khi người quản trị chọn một đơn hàng, Front-end gửi yêu cầu lấy chi tiết đơn hàng tới **Back-end** qua GET request.
    - **Tham số truyền/nhận**: 
      - **Truyền**: order_id.
    - **Back-end**:
      - Truy vấn cơ sở dữ liệu để lấy thông tin chi tiết đơn hàng.
      - **SQL**: `SELECT * FROM orders WHERE order_id = ?`
    - **Kết quả**:
      - Trả về thông tin chi tiết đơn hàng, bao gồm các sản phẩm và số lượng.
  
  - **Cập nhật trạng thái đơn hàng**
    - **Front-end**:
      - Hiển thị trạng thái đơn hàng (chưa xử lý, đang vận chuyển, đã hoàn tất).
      - Người quản trị có thể thay đổi trạng thái và nhấn "Cập nhật".
      - Gửi trạng thái mới (order_id, new_status) tới **Back-end** qua PUT request.
    - **Tham số truyền/nhận**: 
      - **Truyền**: order_id, new_status.
    - **Back-end**:
      - Cập nhật trạng thái đơn hàng trong cơ sở dữ liệu.
      - **SQL**: `UPDATE orders SET status = ? WHERE order_id = ?`
    - **Kết quả**:
      - Nếu thành công: Trả về thông báo "Trạng thái đơn hàng đã được cập nhật".
      - Nếu thất bại: Gửi lỗi (ví dụ: không tìm thấy đơn hàng).

  - **Hủy đơn hàng**
    - **Front-end**:
      - Hiển thị danh sách đơn hàng và nút "Hủy" bên cạnh mỗi đơn hàng chưa xử lý.
      - Khi người quản trị nhấn "Hủy", Front-end gửi yêu cầu hủy đơn hàng (order_id) tới **Back-end** qua DELETE request.
    - **Tham số truyền/nhận**: 
      - **Truyền**: order_id.
    - **Back-end**:
      - Cập nhật trạng thái đơn hàng thành "Đã hủy" trong cơ sở dữ liệu.
      - **SQL**: `UPDATE orders SET status = 'Canceled' WHERE order_id = ? AND status = 'Pending'`
    - **Kết quả**:
      - Nếu thành công: Trả về thông báo "Đơn hàng đã được hủy".
      - Nếu thất bại: Gửi lỗi (ví dụ: đơn hàng đã được xử lý).
### 2.6. **Báo cáo thống kê**
  - **Thống kê doanh thu theo ngày/tháng/năm**
    - **Front-end**:
      - Hiển thị các biểu đồ hoặc bảng thông tin thống kê doanh thu trong một khoảng thời gian cụ thể (chọn từ ngày, tháng, năm).
      - Người quản trị chọn khoảng thời gian cần thống kê và nhấn "Xem báo cáo".
      - Gửi yêu cầu thống kê (start_date, end_date) tới **Back-end** qua GET request.
    - **Tham số truyền/nhận**: 
      - **Truyền**: start_date, end_date (ngày bắt đầu và kết thúc).
    - **Back-end**:
      - Truy vấn tổng doanh thu trong khoảng thời gian đã chọn.
      - **SQL**: `SELECT SUM(total_amount) FROM orders WHERE order_date BETWEEN ? AND ?`
    - **Kết quả**:
      - Trả về tổng doanh thu trong khoảng thời gian yêu cầu.
      - Có thể hiển thị dưới dạng biểu đồ hoặc bảng.

  - **Thống kê số lượng sản phẩm bán được**
    - **Front-end**:
      - Hiển thị số lượng sản phẩm bán được theo từng loại sản phẩm hoặc theo danh mục.
      - Người quản trị chọn một khoảng thời gian và nhấn "Xem thống kê".
      - Gửi yêu cầu thống kê số lượng sản phẩm (start_date, end_date) tới **Back-end** qua GET request.
    - **Tham số truyền/nhận**: 
      - **Truyền**: start_date, end_date.
    - **Back-end**:
      - Truy vấn số lượng sản phẩm đã bán trong khoảng thời gian đã chọn.
      - **SQL**: 
        ```sql
        SELECT product_id, SUM(quantity) AS total_sold 
        FROM order_items 
        WHERE order_date BETWEEN ? AND ? 
        GROUP BY product_id
        ```
    - **Kết quả**:
      - Trả về danh sách các sản phẩm cùng số lượng đã bán được.

  - **Thống kê đơn hàng theo trạng thái**
    - **Front-end**:
      - Hiển thị tổng số đơn hàng theo từng trạng thái (chưa xử lý, đang vận chuyển, đã hoàn tất).
      - Người quản trị có thể chọn trạng thái đơn hàng và xem báo cáo.
      - Gửi yêu cầu thống kê trạng thái đơn hàng (status) tới **Back-end** qua GET request.
    - **Tham số truyền/nhận**: 
      - **Truyền**: status (chưa xử lý, đang vận chuyển, đã hoàn tất).
    - **Back-end**:
      - Truy vấn số lượng đơn hàng theo từng trạng thái.
      - **SQL**: `SELECT status, COUNT(*) AS total_orders FROM orders WHERE status = ? GROUP BY status`
    - **Kết quả**:
      - Trả về số lượng đơn hàng theo trạng thái đã chọn.

### 2.7. **Tìm kiếm và lọc báo cáo**
  - **Front-end**:
    - Cho phép người quản trị tìm kiếm báo cáo theo từ khóa, danh mục hoặc ngày tháng.
    - Gửi thông tin tìm kiếm (keywords, category_id, date_range) tới **Back-end** qua GET request.
  - **Tham số truyền/nhận**:
    - **Truyền**: keywords, category_id, date_range.
  - **Back-end**:
    - Truy vấn dữ liệu báo cáo theo các tham số tìm kiếm.
    - **SQL**: 
      ```sql
      SELECT * FROM orders 
      WHERE product_name LIKE ? 
      AND category_id = ? 
      AND order_date BETWEEN ? AND ?
      ```
    - **Kết quả**:
      - Trả về danh sách đơn hàng hoặc sản phẩm theo yêu cầu tìm kiếm.
### 2.5. **Quản lý người dùng**
  - **Hiển thị danh sách người dùng**
    - **Front-end**:
      - Hiển thị danh sách người dùng, bao gồm thông tin cá nhân (username, email, vai trò).
    - **Back-end**:
      - Truy vấn cơ sở dữ liệu để lấy thông tin người dùng.
      - **SQL**: `SELECT * FROM users`
    - **Kết quả**:
      - Trả về danh sách người dùng.

  - **Cập nhật quyền người dùng**
    - **Front-end**:
      - Hiển thị danh sách người dùng với nút "Cập nhật quyền" bên cạnh mỗi người dùng.
      - Khi người quản trị nhấn "Cập nhật quyền", Front-end hiển thị form chọn quyền (admin, user) và gửi thông tin người dùng mới tới **Back-end** qua PUT request.
    - **Tham số truyền/nhận**: 
      - **Truyền**: user_id, new_role.
    - **Back-end**:
      - Cập nhật quyền người dùng trong cơ sở dữ liệu.
      - **SQL**: `UPDATE users SET role = ? WHERE user_id = ?`
    - **Kết quả**:
      - Nếu thành công: Trả về thông báo "Quyền người dùng đã được cập nhật".
      - Nếu thất bại: Gửi lỗi (ví dụ: người dùng không tồn tại).