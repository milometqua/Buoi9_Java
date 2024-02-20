
# [JAVA] - BUỔI 9: LUÔN CÓ NGOẠI LỆ, XỬ LÍ NGOẠI LỆ
## Làm quen với Exception
Exception là một sự kiện bất ngờ xảy ra trong quá trình thực thi chương trình làm phá vỡ luồng chạy bình thường của chương trình. Chúng ta có ba loại exception là:
* Checked
* Unchecked
* Error
### Checked Exception
CheckedException là những exception có thể nhìn thấy và kiểm tra tại thời điểm biên dịch. Là ngoại lệ thường xảy ra do người dùng mà không thể lường trước được bởi lập trình viên. Những ngoại lệ này không thể được bỏ qua trong quá trình biên dịch. Checked Exception là các lớp mà kế thừa lớp Throwable ngoại trừ RuntimeException và Error. Ví dụ như IOException, SQLException,…

Các ngoại lệ kiểu Checked Exceptions phổ biến:

* IOException: Ngoại lệ liên quan đến file input / output
* SQLException: Ngoại lệ liên quan đến cú pháp SQL
* DataAccessException: Ngoại lệ liên quan đến việc truy cập CSDL
* ClassNotFoundException: Bị ném khi JVM không thể tìm thấy một lớp mà nó cần, do lỗi dòng lệnh, sự cố đường dẫn hoặc tệp, class bị thiếu...
* InstantiationException: Ngoại lệ khi cố gắng tạo đối tượng của một abstract class hoặc interface
### Unchecked Exception
UncheckedException là các exception không được kiểm tra tại thời điểm biên dịch. Hầu hết các unchecked exception xảy ra do dữ liệu không hợp lệ trong quá trình tương tác với chương trình. Bắt buộc chúng ta phải thêm các điều kiện để kiểm tra dữ liệu nhầm đảm bảo chương trình chạy đúng cho mọi trường hợp. 

Các ngoại lệ kiểu Unchecked Exceptions phổ biến:

* NullPointerException: Ngoại lệ bị ném ra khi cố gắng truy cập một đối tượng có biến tham chiếu có giá trị hiện tại là null
* ArrayIndexOutOfBound: Ngoại lệ khi cố gắng truy cập một phần tử vượt quá độ dài của mảng
* IllegalArgumentException: Ngoại lệ bị ném ra khi một phương thức nhận được một đối số được định dạng khác với phương thức mong đợi.
* IllegalStateException: Ngoại lệ bị ném ra khi trạng thái của môi trường không phù hợp với hoạt động cố gắng thực hiện, ví dụ: Sử dụng Scanner đã bị đóng.
* NumberFormatException: Ngoại lệ bị ném khi một phương thức chuyển đổi một Chuỗi thành số nhưng không thể chuyển đổi.
* ArithmeticException: Lỗi số học, chẳng hạn như chia cho 0.

### Error
Nó không giống các exception, nhưng vấn đề xảy ra vượt quá tầm kiểm soát của lập trình viên hay người dùng. Error được bỏ qua trong code của bạn vì bạn hiếm khi có thể làm gì đó khi chương trình bị error. Ví dụ như OutOfMemoryError, VirtualMachineError, AssertionError, … Nó được bỏ qua trong quá trình Java biên dịch.

## Bắt Exception với try-catch
* Cú pháp của try catch trong Java:
```java
try {
    // code có thể ném ra ngoại lệ
} catch(Exception_class_Name ex) {
    // code xử lý ngoại lệ
}
```
Ví dụ 1:
```java
public class TryCatchDemo {
    public static void main(String[] args) {
        int data = 5 / 0;  
        System.out.println("Phép chia cho 0");
    }
}
```
Kết quả:
```js
Exception in thread "main" java.lang.ArithmeticException: / by zero
at demo.TryCatchDemo.main(TryCatchDemo.java:5)
```
Trình biên dịch đã dừng lại ngay tại dòng *int data = 5 / 0* và ném ra một ngoại lệ (exception) ở trong màn hình console.

Xử lý ví dụ trên bằng try-catch:
```java
public class TryCatchDemo {
    public static void main(String[] args) {

        //Xử lý ngoại lệ bằng try catch trong Java
        try {
            int data = 5 / 0;
        } catch (ArithmeticException e) {
            //In ra màn hình tên ngoại lệ
            System.out.println(e);
        }
        System.out.println("Phép chia cho 0");
    }
}
```
Kết quả:
```js
java.lang.ArithmeticException: / by zero
Phép chia cho 0
```
Ví dụ 2:
```java
public class TryCatchDemo {
    public static void main(String[] args) {
        try {
            int arr[] = new int[5];
            arr[6] = 4;
            System.out.println("arr[6 = " + arr[6]);

            int data = 0;
            int div = 10 / data;
            System.out.println("Average = " + div);

            String obj = null;
            System.out.println(obj.length());
        } catch (NullPointerException ex) {
            System.out.println(ex);
        } catch (ArithmeticException ex) {
            System.out.println(ex);
        } catch (ArrayIndexOutOfBoundsException ex) {
            System.out.println(ex);
        }

        System.out.println("Finished!");
    }
}
```
Kết quả:
```js
java.lang.ArrayIndexOutOfBoundsException: 6
Finished!
```
*Khi bắt gặp một ngoại lệ, trình biên dịch Java sẽ ngay lập tức thực thi xử lý ngoại lệ tương ứng (do đó, nó thoát khỏi khối try và không tìm thấy 2 ngoại lệ khác mà mình đã cố tạo ra)*
## Sử dụng finally
Cấu trúc khối `finally` trong Java
```java
try{
  //Các lệnh có khả năng ném ra ngoại lệ
} catch(Exception1 ex1){
…
} catch(Exception2 ex2){
…
} catch(Exception exn){
…
} finally{
//Mã lệnh dọn dẹp
}
```
Khối `finally` là tuỳ chọn, không bắt buộc phải có. Khối này được đặt sau khối `catch` cuối cùng. Chương trình sẽ thực thi câu lệnh đầu tiên của khối `finally` ngay sau khi gặp câu lệnh `return` hay lệnh `break` trong khối `try`.

Khối `finally` bảo đảm lúc nào cũng được thực thi, bất chấp có ngoại lệ xảy ra hay không. Hình minh họa sự thực hiện của các khối `try`, `catch` và `finally`

![](https://user-images.githubusercontent.com/29374426/126114810-e1c61816-0531-42a8-b493-7232c4d2fcbc.png)

Ví dụ sử dụng khối lệnh finally nơi ngoại lệ không xảy ra.
```java
public class TestFinallyBlock {
    public static void main(String args[]) {
        try {
            int data = 25 / 5;
            System.out.println(data);
        } catch (NullPointerException e) {
            System.out.println(e);
        } finally {
            System.out.println("finally block is always executed");
        }
        System.out.println("rest of the code...");
    }
}
```
Kết quả
```
5

finally block is always executed

rest of the code...
```
Ví dụ sử dụng khối lệnh finally nơi ngoại lệ xảy ra nhưng không xử lý.
```java
public class TestFinallyBlock1 {
    public static void main(String args[]) {
        try {
            int data = 25 / 0;
            System.out.println(data);
        } catch (NullPointerException e) {
            System.out.println(e);
        } finally {
            System.out.println("finally block is always executed");
        }
        System.out.println("rest of the code...");
    }
}
```
Kết quả:
```
finally block is always executed

Exception in thread "main" java.lang.ArithmeticException: / by zero
```
Ví dụ sử dụng khối lệnh finally nơi ngoại lệ xảy ra và được xử lý.

```java
public class TestFinallyBlock2 {
    public static void main(String args[]) {
        try {
            int data = 25 / 0;
            System.out.println(data);
        } catch (ArithmeticException e) {
            System.out.println(e);
        } finally {
            System.out.println("finally block is always executed");
        }
        System.out.println("rest of the code...");
    }
}
```
Kết quả:
```
java.lang.ArithmeticException: / by zero

finally block is always executed

rest of the code...
```
## Cây phân cấp Exception, phân biệt throw và throws
### Mô hình sơ đồ phân cấp của Exception trong java.

Class ở mức cao nhất là Throwable
Hai class con trực tiếp là Error và Exception.
Trong nhánh Exception có một nhánh con RuntimeException là các ngoại lệ sẽ không được java kiểm tra trong thời điểm biên dịch.

![](https://gpcoder.com/wp-content/uploads/2017/11/Exception_Classes.png)

### Từ khóa throws trong java
Nếu một phương thức không xử lý một ngoại lệ đã kiểm tra thì phương thức đó phải khai báo ngoại lệ bằng từ khóa throws. Từ khóa throws được khai báo ở cuối dấu ngoặc ( ) trước khi bắt đầu một phương thức.

Ví dụ:
```java
import java.io.*;
public class DemoJava {
    public static void main(String[] args) throws IOException {
       FileOutputStream fileOutputStream = null;
       fileOutputStream = new FileOutputStream("D://output.txt");
       fileOutputStream.write(65);
    }
}
```
Ở ví dụ trên phương thức main đã khai báo bỏ qua ngoại lệ IOException nên chương trình trên vẫn chạy bình thường.

Có thể khai báo bỏ qua nhiều ngoại lệ bằng cách khai báo các ngoại lệ sau từ khóa throws cách nhau bởi dấu phẩy. Ví dụ:
 ```java
 public void withdraw(int n) throws RemoteException, 
      InsufficientFundsException {
      //khối lệnh
   }
 ```
### Từ khóa throw trong java
Từ khóa throw dùng để ném ra một ngoại lệ cụ thể.

Chúng ta có thể ném một trong hai ngoại lệ checked hoặc unchecked trong java bằng từ khóa throw. Từ khóa throw chủ yếu được sử dụng để ném ngoại lệ tùy chỉnh (ngoại lệ do người dùng tự định nghĩa).

Cú pháp từ khóa throw:
```java
throw exception ;
```
Ví dụ về ném ra ngoại lệ IOException
```java
throw new IOException("File khong ton tai") ;
```
Cách ném ra ngoại lệ bằng từ khóa throw
```java
import java.io.*;
public class DemoJava {
    static void demoThrow ()throws IOException{
        throw new IOException("File khong ton tai");
    }
    public static void main(String[] args) throws IOException {
    demoThrow();
    }

}
```
Kết quả

> Exception in thread "main" java.io.IOException: File khong ton tai

Lưu ý khi throw ra một exception trong một phương thức thì hoặc:

* Phải dùng từ khóa throws để bỏ qua ngoại lệ đó.
* phải dùng khối try-catch để bắt ngoại lệ đó.

| throw | throws |
| ---------------- | ----------- |
| Từ khóa throw trong java được sử dụng để ném ra một ngoại lệ rõ ràng.          | Từ khóa throws trong java được sử dụng để khai báo một ngoại lệ.    |
| Ngoại lệ checked không được truyền ra nếu chỉ sử dụng từ khóa throw.           | Ngoại lệ checked được truyền ra ngay cả khi chỉ sử dụng từ khóa throws.  |
| Sau throw là một instance.            | Sau throws là một hoặc nhiều class.        |
| Throw được sử dụng trong phương thức có thể quăng ra Exception ở bất kỳ dòng nào trong phương thức (sau đó dùng try-catch để bắt hoặc throws cho thằng khác sử lý)        | Throws được khai báo ngay sau dấu đóng ngoặc đơn của phương thức. Khi một phương thức có throw bên trong mà không bắt lại (try – catch) thì phải ném đi (throws) cho thằng khác xử lý.  |
| Không thể throw nhiều exceptions.      | Có thể khai báo nhiều exceptions    |
## Tạo ra Exception của riêng mình
Để tạo một Custom Exception trong Java, cần tạo một lớp kế thừa từ lớp `Exception` hoặc các lớp con của nó. Dưới đây là một ví dụ về cách tạo một Custom Exception có tên là `InvalidAgeException`:
```java
// File: InvalidAgeException.java
class InvalidAgeException extends Exception {
    InvalidAgeException(String s) {
        super(s);
    }
}
```
Ở đây, chúng ta đã tạo một lớp InvalidAgeException kế thừa từ Exception. Lớp này có một constructor để truyền thông điệp ngoại lệ.

Bây giờ, chúng ta có thể sử dụng Custom Exception trong ứng dụng của mình. Dưới đây là một ví dụ:
```java
// File: TestCustomException1.java
class TestCustomException1 {

    static void validate(int age) throws InvalidAgeException {
        if (age < 18)
            throw new InvalidAgeException("Không đủ tuổi mất rồi :))))");
        else
            System.out.println("Chúc mừng bạn đã đủ tuổi uống rượu");
    }

    public static void main(String args[]) {
        try {
            validate(13);
        } catch (InvalidAgeException e) {
            System.out.println("Xảy ra ngoại lệ: " + e.getMessage());
        }

        System.out.println("Phần còn lại của mã...");
    }
}
```