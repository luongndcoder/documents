## OOP In Python (Object Oriented Programming)
- Python là ngôn ngữ lập trình hướng đối tượng. Mọi thứ trong Python đều là những đối tượng với những thuộc tính(properties) và phương thức(methods).
- OOP là kỹ thuật cho phép tạo ra các đối tượng để trừ tượng hóa 1 đối tượng thực tế(đưa các đối tượng trong thực tế vào trong code). Cho phép lập trình viên tương tác với các đối tượng này.
- Một đối tượng bao gồm: thuộc tính(attributes) và phương thức (methods).
- Thuộc tính(attributes) chính là các thông tin, đặc điểm của đối tượng. 
    VD: chó(châ, đuôi, màu lông)
- Phương thức(methods) là thao tác, hành động mà đối tượng đó có thể thực hiện. VD: Con mèo(ăn, ỉa, cắn, gào)...
- Lớp (class) có thể hiểu là một bản thiết kế để tạo ra một thực thể nào đó, là tập hợp nhiều thuộc tính đặc trưng cho đối tượng được tạo ra từ lớp này. chó (tên, màu sắc, đuôi, tai, ...)
- Đối tượng là một thực thể của một lớp nào đó, được tạo ra từ lớp đó:
    VD: Chó đốm (Tên là mèo, màu trắng đen, không có đuôi, 2 tai, 4 chân, ...)

# OOP tuân thủ một số nguyên lý cơ bản, có 4 nguyên lý cả đời làm code không được quên: 
    + Tính đóng gói
    + Tính kế thừa 
    + Tính bao đóng
    + Tính đa hình

# Các nguyên lý cơ bản của Python 
    - Tính đóng gói(Encapsulation): Các dữ liệu và phương thức có liên quan quan với nhau được đóng gói thành 1 lớp. Mỗi lớp được xây dựng để thực hiện một nhóm chức năng đặc trưng của riêng lớp đó. Che dấu các thông tin của lớp đó. Che dấu các thông tin của lớp đó đối với bên ngoài thể hiện ở public, protected, private đối với từng thuộc tính và phương thức.
    - Tính kế thừa (Inheritance): Nguyên tắc này cho phép xây dựng một lớp mới dựa trên 1 lớp đã khai báo từ trước. Lớp con có thể sử dụng lại các thuộc tính và phương thức của lớp cha mà không cần khai báo lại. Tùy thuộc vào từng ngôn ngữ cho phép việc kế thừa 1 hoặc nhiều class cha.
    - Tính trừu tượng (Abtraction): Tổng quát hóa phương thức đối tượng không quan tâm phương thức thực hiện như thế nào, được thể hiện bởi interface (có các tên phương thức nhưng không có body của phương thức, khi class nào impliment interface thì thực hiện nó).
    - Tính đa hình (Polymorphism): Tính đa hình được thể hiện bởi một phương thức, hành động có thể thực hiện theo nhiều cách khác nhau.
        - Ví dụ: Chó và mèo đều là động vật nhưng khi thực hiện phương thức "sủa" thì chó sủa "gâu gâu" còn mèo thì "mèo méo meo mèo meo" :v .
# Class, methods, attributes
    - Python có nhiều lớp được định nghĩa sẵn. Do mọi thứ trong Python đều là đối tượng ví dụ như list, tuple, dictionary, string, int... là các lớp. Khi chúng ta khai báo biến thuộc các lớp này thì chúng là các đối tượng
    - VD: type(1) // <class 'int'>, type(1.1) // <class 'float'>
    - Ngoài các class có sẵn thì chúng ta có thể định nghĩa ra các lớp riêng biệt sử dụng từ khóa class :
        class Animal:
            pass // khi viết hàm này python ngầm hiểu mình không cần phải khai báo thêm thuộc tính gì nữa (lớp rỗng, nếu không viết gì thì sẽ báo lỗi)
    - animal = Animal()
    print type(animal) // <type 'classobj'>
    print type(animal) // <type 'instance'>

    - class Animal:
        weight: 12.5
        
        def __init__(self, name):
            self.name = name
    animal = Animal("Dog")
    print(animal.name)

    - Các phương thức có sẵn được kế thừa từ lớp gốc - magic method
        - Phương thức __init__() trình bày khởi tạo các tham số, thuộc tính của class
        - Ngoài ra còn có `__repr__(), __str__(), __del__(), __format__(), __bytes__(), __hash__(), __len__(), __add__(), __call__(), ...`
    - Tính bao đóng
        - bản chất trong python khái niệm về private, protected, public không có, trong code chúng ta cần ám chỉ điều này cho việc truy cập đúng.
            - Với public thì truy cập được mọi nơi, cách khai báo như hàm bình thường
            - Với protected thì chỉ lớp con có thể truy cập được, cách khai báo bằng một dấu gạch ngang "_", VD: _age, _name. Chúng ta cần ngầm hiểu là không sử dụng nếu không phải class con.
            - Với private thì chỉ class đó có quyền truy cập, cách khai báo bằng bắt đầu bằng 2 dấu gạch ngang "__" VD: __name, __age.
            `
                class Animal:
                    __name = "Dog"
                    def __get_name(self):
                        print(self.__name)
                    def get(self):
                    self.__get_name()
                print(Animal().__name) # error
                Animal().__get_name() # error
                Animal().get()
            `
    - Kế thừa 
        - Cú pháp kế thừa: class childClass(baseClass):

        class Animal:
            legs = '0'

            def __init__(self):
                pass
            
            def whoAmI(self):
                print("Animal")
            
            def eat(self):
                print("Eating")
        
        class Dog(Animal):
            def __int__(self):
                Animal.__int__(self):
                print ("Dog created")
                self.legs = "4"
            def whoAmI(self):
                print ("Dog go go")
            
            def eat(self):
                print ("eat eat eat .....")

            def run(self):
                print ("legs: " + self.legs + " run run run .....")
        d = Dog()
        d.whoAmI()
        d.eat()
        d.run() 
    
    - Trong Python chúng ta có thể đa kế thừa - cho phép từ 1 class con có thể kế thừa nhiều class cha:
        class Animal:
            legs = '0'

            def __init__(self):
                pass

            def whoAmI(self):
                print ("Animal")
            
            def eat(self):
                print ("Eating")

        class Entity:
            def __init__(self):
                pass

            def weight(self):
                print 'weight 88';
            
        class Dog(Entity, Animal):
            def __init__(self):
                Animal.__init__(self)
                Entity.__init__(self)
                print ("Dog created")
                self.legs = '4';
            
            def whoAmI(self):
                print ("Dog go go")
            
            def eat(self):
                print ("eat eat eat .....")

            def run(self):
                print ("legs: " + self.legs + " run run run .....")
            
            
        d = Dog()
        d.whoAmI()
        d.eat()
        d.run()
        d.weight()
    - Interface, abstract class
        - abstract class: Các Abstract clas cho phép cung cấp chức năng mặc định cho các class con. Bằng cách định nghĩa một abtract base class (lớp cơ sở trừu tượng), có thể xây dựng nên một mô hình chung cho một nhóm các class con. Mặc định trong Python sẽ không cung cấp Abtract Class cho chúng ta sử dụng. Nhưng Python có một mô-đun là Abstract Base Classes (ABC) để giúp chúng ta làm điều đó.
        - Mô-đun này nằm trong package abc nên chúng ta cần import vào trước khi sử dụng.
        - from abc import ABC, abstractmethod
        
        # abtract class
        class abstractClassName(ABC):
            @abstractmethod
            def methodName(self):
                pass
        
        # tạo class implement từ abstractClassName
        class normalClass(abstractClassName):
            # Khai báo thuộc tính, phương thức class ở đây
            def methodName(self):
                pass
        - Interface :
            - Do Python có đa kế thừa nên interface thực sự không cần thiết tuy nhiên nếu biết thì vẫn là tốt hơn. Cú pháp khai báo cũng giống như trên thôi.
            
            form abc import ABC, abstractmethod

            class InformalParserInterface:
                @abstractmethod
                def load_data_source(self):
                    pass

                def extract_text(self):
                    pass
