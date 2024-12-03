# Hệ thống quản lý bán sách

## Khách hàng

### Đăng ký/Đăng nhập
- **Mô tả**: Người dùng có thể tạo tài khoản mới hoặc đăng nhập vào hệ thống.
- **Luồng dữ liệu**:
  1. **Front-end**: Gửi yêu cầu qua form đăng ký/đăng nhập.
  2. **Back-end**: Xử lý xác thực tài khoản.
  3. **Database**: Truy vấn lưu trữ hoặc kiểm tra tài khoản.
- **API**:
  - Đăng ký:
    - `POST /api/auth/register`
    - **Body**:
      ```json
      {
        "username": "example",
        "email": "example@gmail.com",
        "password": "password123"
      }
      ```
  - Đăng nhập:
    - `POST /api/auth/login`
    - **Body**:
      ```json
      {
        "email": "example@gmail.com",
        "password": "password123"
      }
      ```
- **SQL Query**:
  - Kiểm tra tài khoản:
    ```sql
    SELECT * FROM users WHERE email = 'example@gmail.com';
    ```
  - Lưu tài khoản mới:
    ```sql
    INSERT INTO users (username, email, password) VALUES ('example', 'example@gmail.com', 'hashed_password');
    ```

---

### Tìm kiếm sách
- **Mô tả**: Người dùng có thể tìm kiếm sách theo tên, thể loại, hoặc tác giả.
- **Luồng dữ liệu**:
  1. **Front-end**: Form tìm kiếm gửi từ khóa lên back-end.
  2. **Back-end**: Truy vấn database để lấy kết quả phù hợp.
  3. **Database**: Trả về danh sách sách phù hợp.
- **API**:
  - `GET /api/books/search`
    - **Query Params**:
      ```json
      {
        "keyword": "Từ khóa tìm kiếm"
      }
      ```
- **SQL Query**:
  ```sql
  SELECT * FROM books WHERE title LIKE '%keyword%' OR author LIKE '%keyword%';
### Thêm sách vào giỏ hàng
- **Mô tả**: Người dùng có thể thêm sách vào giỏ hàng để mua sau.
- **Luồng dữ liệu**:
  1. **Front-end**: Người dùng chọn sách và nhấn "Thêm vào giỏ".
  2. **Back-end**: Xử lý yêu cầu thêm sách vào giỏ hàng.
  3. **Database**: Cập nhật giỏ hàng của người dùng.
- **API**:
  - `POST /api/cart/add`
    - **Body**:
      ```json
      {
        "userId": "12345",
        "bookId": "67890",
        "quantity": 1
      }
      ```
- **SQL Query**:
  ```sql
  INSERT INTO cart (user_id, book_id, quantity) VALUES ('12345', '67890', 1);

### Xóa sản phẩm khỏi giỏ hàng

- **Mô tả**: Khách hàng có thể xóa sản phẩm khỏi giỏ hàng khi không muốn tiếp tục mua sản phẩm đó.
- **Luồng dữ liệu**:

    1. **Front-end**: Khách hàng bấm nút "Xóa" bên cạnh sản phẩm trong giỏ hàng.

    2. **Back-end**: xử lý xóa sản phẩm khỏi giỏ hàng và cập nhật giỏ hàng trong cơ sở dữ liệu.

    3. **Database**: Cập nhật bảng `cart_items` để xóa sản phẩm đã chọn khỏi giỏ hàng của khách hàng.

- **API**:
    - `DELETE /api/customers/cart/:productId`
    - **Request**:
    - **Headers**:
        ```json
        {
        "Authorization": "Bearer {token}"
        }
        ```
    - **Params**:
        - `productId`: ID của sản phẩm cần xóa khỏi giỏ hàng.
    - **Response**:
        ```json
        {
            "message": "Product removed from cart successfully",
            "cart": {
            "total_items": 2,
            "total_price": 300000
            }
        }    


## Quản trị viên

### Quản lý sách
- **Mô tả**: Quản trị viên có thể thêm, cập nhật, hoặc xóa sách.
- **Luồng dữ liệu**:
  1. **Front-end**: Form nhập liệu của quản trị viên.
  2. **Back-end**: Xử lý thêm, cập nhật, hoặc xóa sách.
  3. **Database**: Thực hiện các thay đổi tương ứng.
- **API**:
  - **Thêm sách**:
    - `POST /api/admin/books`
    - **Body**:
      ```json
      {
        "title": "Tên sách",
        "author": "Tên tác giả",
        "price": 20000,
        "category": "Thể loại",
        "stock": 50
      }
      ```
  - **Cập nhật sách**:
    - `PUT /api/admin/books/:bookId`
    - **Body**:
      ```json
      {
        "title": "Tên sách mới",
        "price": 25000
      }
      ```
  - **Xóa sách**:
    - `DELETE /api/admin/books/:bookId`
- **SQL Query**:
  - Thêm sách:
    ```sql
    INSERT INTO books (title, author, price, category, stock) VALUES ('Tên sách', 'Tên tác giả', 20000, 'Thể loại', 50);
    ```
  - Cập nhật sách:
    ```sql
    UPDATE books SET title = 'Tên sách mới', price = 25000 WHERE id = 'bookId';
    ```
  - Xóa sách:
    ```sql
    DELETE FROM books WHERE id = 'bookId';
    ```

---

### Quản lý đơn hàng
- **Mô tả**: Quản trị viên có thể xem và cập nhật trạng thái đơn hàng.
- **Luồng dữ liệu**:
  1. **Front-end**: Gửi yêu cầu hiển thị hoặc cập nhật trạng thái đơn hàng.
  2. **Back-end**: Xử lý yêu cầu từ giao diện.
  3. **Database**: Truy xuất hoặc cập nhật thông tin đơn hàng.
- **API**:
  - **Xem danh sách đơn hàng**:
    - `GET /api/admin/orders`
  - **Cập nhật trạng thái đơn hàng**:
    - `PUT /api/admin/orders/:orderId`
    - **Body**:
      ```json
      {
        "status": "Đã giao"
      }
      ```
- **SQL Query**:
  - Lấy danh sách đơn hàng:
    ```sql
    SELECT * FROM orders ORDER BY order_date DESC;
    ```
  - Cập nhật trạng thái đơn hàng:
    ```sql
    UPDATE orders SET status = 'Đã giao' WHERE id = 'orderId';
    ```

---

### Báo cáo doanh thu
- **Mô tả**: Thống kê doanh thu từ các đơn hàng.
- **Luồng dữ liệu**:
  1. **Front-end**: Quản trị viên chọn khoảng thời gian báo cáo.
  2. **Back-end**: Xử lý tính toán doanh thu.
  3. **Database**: Truy xuất dữ liệu từ các đơn hàng.
- **API**:
  - `GET /api/admin/reports/revenue`
    - **Query Params**:
      ```json
      {
        "startDate": "2024-01-01",
        "endDate": "2024-01-31"
      }
      ```
- **SQL Query**:
  ```sql
  SELECT SUM(total_price) AS revenue FROM orders WHERE order_date BETWEEN '2024-01-01' AND '2024-01-31';

### Quản lý tài khoản khách hàng

#### Xem danh sách tài khoản khách hàng
- **Mô tả**: Quản trị viên có thể xem danh sách tất cả các tài khoản khách hàng trong hệ thống.
- **Luồng dữ liệu**:
  1. **Front-end**: Quản trị viên gửi yêu cầu xem danh sách tài khoản.
  2. **Back-end**: Xử lý yêu cầu và truy xuất danh sách tài khoản từ database.
  3. **Database**: Truy xuất thông tin tài khoản khách hàng.
- **API**:
  - **GET /api/admin/users**
    - **Response**:
      ```json
      [
        {
          "id": "user1",
          "name": "Nguyễn Văn A",
          "email": "nguyenvana@example.com",
          "status": "active"
        },
        {
          "id": "user2",
          "name": "Trần Thị B",
          "email": "tranb@example.com",
          "status": "inactive"
        }
      ]
      ```
- **SQL Query**:
  ```sql
  SELECT id, name, email, status FROM users WHERE role = 'customer';

#### Vô hiệu hóa tài khoản khách hàng
- **Mô tả**: Quản trị viên có thể vô hiệu hóa tài khoản của khách hàng nếu tài khoản đó không còn hoạt động hoặc vi phạm quy định của hệ thống.

- **Luồng dữ liệu**:
    1. **Front-end**: Quản trị viên chọn tài khoản khách hàng và kích hoạt chức năng vô hiệu hóa.
    2. **Back-end**: Cập nhật trạng thái tài khoản thành `inactive`.
    3. **Database**: Cập nhật trường `status` trong bảng `users`.

- **API**:
    - **PUT /api/admin/customers/:userId**
    - **Body**:
        ```json
        {
        "status": "inactive"
        }
        ```
    - **Response**:
        ```json
        {
        "message": "Customer account deactivated successfully"
        }
        ```

#### Kích hoạt lại tài khoản khách hàng
- **Mô tả**:Quản trị viên có thể kích hoạt lại tài khoản khách hàng nếu tài khoản đã bị vô hiệu hóa.

- **Luồng dữ liệu**:
    1. **Front-end**: Quản trị viên chọn tài khoản khách hàng và kích hoạt chức năng kích hoạt lại.
    2. **Back-end**: Cập nhật trạng thái tài khoản thành `active`.
    3. **Database**: Cập nhật trường `status` trong bảng `users`.

- **API**:
    - **PUT /api/admin/customers/:userId/reactivate**
    - **Body**:
        ```json
        {
        "status": "active"
        }
        ```
    - **Response**:
        ```json
        {
        "message": "Customer account reactivated successfully"
        }
        ```

---

#### Xóa tài khoản khách hàng
- **Mô tả**: Quản trị viên có thể xóa tài khoản khách hàng khỏi hệ thống nếu tài khoản không còn cần thiết hoặc vi phạm các quy định.

- **Luồng dữ liệu**:
    1. **Front-end**: Quản trị viên chọn tài khoản khách hàng và kích hoạt chức năng xóa.
    2. **Back-end**: Hệ thống xóa tài khoản khỏi cơ sở dữ liệu.
    3. **Database**: Xóa khách hàng khỏi bảng `users`.

- **API**:
    - **DELETE /api/admin/customers/:userId**
    - **Response**:
        ```json
        {
        "message": "Customer account deleted successfully"
        }
        ```

---

#### Lọc khách hàng theo trạng thái
- **Mô tả**: Quản trị viên có thể lọc danh sách khách hàng theo trạng thái (hoạt động hoặc vô hiệu hóa).

- **Luồng dữ liệu**:
    1. **Front-end**: Quản trị viên chọn bộ lọc trạng thái (active/inactive).
    2. **Back-end**: Hệ thống trả về danh sách khách hàng với trạng thái đã chọn.
    3. **Database**: Truy vấn bảng `users` theo trạng thái đã lọc.

- **API**:
    - **GET /api/admin/customers?status=active**
    - **Response**:
        ```json
        [
        {
            "id": "user1",
            "name": "Nguyễn Văn A",
            "email": "nguyenvana@example.com",
            "status": "active"
        }
        ]
        ```

---

#### Cập nhật thông tin khách hàng
- **Mô tả**: Quản trị viên có thể cập nhật thông tin tài khoản khách hàng như tên, email, và mật khẩu.

- **Luồng dữ liệu**:
    1. **Front-end**: Quản trị viên chọn tài khoản cần cập nhật thông tin.
    2. **Back-end**: Hệ thống nhận thông tin và cập nhật cơ sở dữ liệu.
    3. **Database**: Cập nhật thông tin trong bảng `users`.

- **API**:
    - **PUT /api/admin/customers/:userId**
    - **Body**:
        ```json
        {
        "name": "Nguyễn Văn C",
        "email": "nguyenvc@example.com"
        }
        ```
    - **Response**:
        ```json
        {
        "message": "Customer information updated successfully"
        }
        ```

