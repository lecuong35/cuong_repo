# Ruby Programming
## Biến trong Ruby
1. ***Biến cục bộ***

    Biến cục bộ là biến được khai báo và sử dụng chỉ trong hàm hoặc module đó. Nếu sử dụng biến cục bộ ngoài hàm đó thì sẽ nhận báo lỗi không tìm thấy biến.
2. ***Biến toàn cục***

    Biến toàn cục là biến có thể được truy cập từ bất kỳ đâu trong hệ thống. Biến toàn cục có thể bị thay thế giá trị nếu triy cập không hợp lý -> khó tìm ra lỗi --> trong dự án các biến toàn cục nên được quản lý trong 1 file ví dụ tạo một file trong folder settings của dự án.
3. ***Biến hằng***

    Biến hằng chỉ được khai báo một lần duy nhất. Nếu khai báo lần 2 thì sẽ gặp cảnh báo nhưng kết quả vẫn là giá trị mới nhất vì Ruby đánh giá trị như C tức là gán giá trị cho một địa chỉ và khi khai báo lần 2 thì địa chỉ đã bị thay đổi.

    Để biến hằng không bị thay đổi -> báo lỗi chứ ko phải warning thì có thể dùng hàm freeze. Hàm freeze chỉ báo lỗi nếu giá trị của biến đó bị thay đổi ví dụ như dùng hàm str[0] = "new_value" thì sẽ nhận lỗi FrozenError. 
4. ***Biến instance***

    Biến instance là biến thuộc về một đối tượng cụ thể. Mỗi đối tượng có thể có các giá trị khác nhau cho các biến instance của nó. Biến instance được bắt đầu bằng ký tự @.
5. ***Biến lớp***

    Biến lớp là biến thuộc về một lớp cụ thể. Tất cả các đối tượng của lớp đó chia sẻ cùng một giá trị cho biến lớp. Biến lớp được bắt đầu bằng ký tự @@

6. ***Biến an toàn***

    Biến an toàn '*&*' để kiểm tra thực thể có tồn tại không trước khi thực hiện hàm được gọi của nó, nếu không nó trả về nil chứ ko gây lỗi.

## Hàm trong Ruby
1. ***Khai báo hàm***
    ```ruby
        def hello_world
            puts "Hello, World!"
        end
    ```

    Giá trị trả về mặc định là giá trị của biểu thức cuối cùng trong hàm, có thể chỉ định giá trị trả về bằng cách sử dụng từ khóa 'return'.

    Hàm có thể nhận số lượng tham số tùy ý thông qua *params. Hàm cũng là một đối tượng -> có thể gán hàm cho 1 biến, truyền hàm vào hàm khác như một tham số.

2. ***Metadata programming***

    Đây là cách khai báo tên động cho một hàm. Ví dụ ta có 2 hàm xử lý logic giống nhau nhưng tham số đầu vào chỉ khác kiểu dữ liệu thì nên sử dụng hàm động để gọi.
    ```ruby
    class Person
        ["name", "age"].each do |field|
            define_method("get_#{field}") do |prefix|
            puts "#{prefix} #{instance_variable_get("@#{field}")}"
            end
        end
    end

    person = Person.new
    person.instance_variable_set("@name", "John")
    person.instance_variable_set("@age", 30)
    person.get_name("My name is") # Output: "My name is John"
    person.get_age("I am") # Output: "I am 30"
    ```
3. ***block, procs, lamda***
    BLock: được gói trong do ... end hoặc là phần xử lý trong hàm
    ```ruby
        [1,2,3,4,5].each do |i|
            puts i
        end
    ```
    Procs: là một đối tượng, giống như block nhưng có thể được lưu trữ và sử dụng lại.
    ```ruby
        my_proc = Proc.new { |num| puts num }
        [1, 2, 3].each(&my_proc)
    ```
    Lambda: giống như procs nhưng có một số khác biệt nhỏ là lamda kiểm tra số lượng tham số chứ ko gán là nil nếu thiếu và từ khóa return trong lamda chỉ kết thúc lamda chứ không kết thúc hàm.
    ```ruby
        my_lambda = lambda { |x| puts x }
        [1, 2 ,3].each($my_lamda)
    ```
## Condition, loop
1. ***Condition***
    
    * if - elsif - else - end
    * unless - end
    * case expresion - when value1 - when value2 - else - end
    * condition ? value_if_true : value_if_false
2. ***Loop***
    
    * while condition - end
    * until condition - end
    * for ele in collection - end
    * collection.each do |ele| - end
    * n.times do - end
## Array
1. ***Cơ bản***

    Đây là kiểu lưu các giá trị của biến dựa trên chỉ số. Với mảng trong Ruby có các hàm xử lý được xây dựng sẵn như sau:
    
    * *each* - lặp qua từng phần tử để thực thi khối lệnh và không tạo mảng mới.
    * *map* - tương tự như each nhưng tạo mảng mới từ mảng đã cho, nếu phần tử nào thiếu -> nil.
    * *select* - hoạt động như một filter lọc các phần tử của mảng với một điều kiện.
    * *reject* - trái ngược với hàm select
    * *reduce* - lặp qua từng phần tử một cách tuyến tính để thực hiện tích lũy, ví dụ tính tổng của mảng
    * *find* - tìm phần tử đầu tiên
    * *find_all* - tìm tất cả phần tử chung giá trị
    * *unique* - xóa các phần tử trùng với phần tử có sẵn trước đó trong mảng.
    * *các hàm có dấu ! ở sau cùng* thì không tạo mảng mới mà tác động trực tiếp lên mảng
    * *compact* - loại bỏ các phần tử nil trong mảng

## Hash
1. ***Cơ bản***

    Đây là dạng tương tự mảng nhưng lưu các phần tử theo kiểu key-value với key được gọi là symbol
    ```ruby
        person = { name: "John", age: 30, city: "Ha Noi" }
    ```

    Các thao tác với hash:
    * kiểm tra key - has_key?(:symbol) hoặc key?(symbol)
    * kiểm tra value - has_value?(value)

## String
1. ***Cơ bản***

    * *lenth* - lấy độ dài
    * *concat hoặc +* - nối chuỗi
    * *upcase/downcase* - viết hoa, viết thường
    * *split("char_to_split")* - tách chuỗi thành mảng
    * *gsub* - thay chuỗi con bằng chuỗi thay thế
    * *strip* - bỏ khoảng trắng đầu và cuối chuỗi
    * *sub* - thay chuỗi con đầu tiên bằng chuỗi thay thế

## Range, biến đổi thành mảng %i %w
1. ***range***
    * *..* - lấy cả phần tử cuối
    * **...* - bỏ phần tử cuối

2. ***%i %w***
    * *%i* - đổi chuỗi thành symbol
    * *%w* - đổi chuỗi thành mảng ký tự

## Xử lý ngoại lệ
1. ***Cơ bản***
    
    ```ruby
    begin
        result = 10 / 0
    rescue ZeroDivisionError => e
        puts "Lỗi chia cho 0: #{e.message}"
    ensure
        puts "Khối ensure được thực thi"
    end
    ```
## OOP trong Ruby
1. ***Scope trong OOP***

    * *public* - truy cập được từ mọi nơi trong chương trình
    * *protected* - truy cập được trong lớp và các lớp con
    * *private* - chỉ truy cập trong lớp, không truy cập được từ lớp con
2. ***Class***
    * *phương thức*
    * *thuộc tính*
    * *các từ khóa cần biết*
3. ***Module***
4. ***Interface***
5. ***Import class, module, interface***