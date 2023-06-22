Bài toán "Find the Runner-Up Score!" trên HackerRank yêu cầu tìm ra điểm số thứ hai lớn nhất trong một danh sách điểm số.

Đầu vào:
- Dòng đầu tiên chứa một số nguyên N (2 ≤ N ≤ 10^5), số lượng điểm số.
- Dòng thứ hai chứa N số nguyên, mỗi số tương ứng với một điểm số.

Đầu ra:
- In ra một số nguyên duy nhất, tương ứng với điểm số thứ hai lớn nhất trong danh sách.

Ví dụ:

```
Input:
5
2 3 6 6 5

Output:
5
```

Để giải quyết bài toán này, ta có thể sử dụng set và list để loại bỏ các phần tử trùng lặp và sắp xếp danh sách các điểm số theo thứ tự tăng dần. Sau đó, ta lấy phần tử thứ hai từ cuối cùng của danh sách để tìm ra điểm số thứ hai lớn nhất.

Dưới đây là đoạn code Python để giải quyết bài toán này trên HackerRank:

```python
if __name__ == '__main__':
    n = int(input())
    arr = list(map(int, input().split()))

    # Loại bỏ các phần tử trùng lặp bằng set
    unique_scores = set(arr)

    # Sắp xếp danh sách điểm số theo thứ tự tăng dần
    sorted_scores = sorted(unique_scores)

    # In ra điểm số thứ hai lớn nhất
    print(sorted_scores[-2])
```

Trong đoạn code trên, ta sử dụng hàm `set()` để loại bỏ các phần tử trùng lặp trong danh sách điểm số. Sau đó, ta sử dụng hàm `sorted()` để sắp xếp danh sách các điểm số theo thứ tự tăng dần. Cuối cùng, ta lấy phần tử thứ hai từ cuối cùng của danh sách và in ra giá trị đó bằng lệnh `print()`.



Bài toán "Lists" trên Hackerrank yêu cầu thực hiện các thao tác trên danh sách, bao gồm chèn phần tử vào danh sách, xóa phần tử khỏi danh sách và thực hiện các lệnh được chỉ định trên danh sách.

Dưới đây là một lời giải bằng Python cho bài toán này:

```python
n = int(input())
lst = []

for i in range(n):
    command = input().split()
    if command[0] == "insert":
        lst.insert(int(command[1]), int(command[2]))
    elif command[0] == "print":
        print(lst)
    elif command[0] == "remove":
        lst.remove(int(command[1]))
    elif command[0] == "append":
        lst.append(int(command[1]))
    elif command[0] == "sort":
        lst.sort()
    elif command[0] == "pop":
        lst.pop()
    elif command[0] == "reverse":
        lst.reverse()
```

Cụ thể, lời giải này bắt đầu bằng cách đọc vào số lượng câu lệnh N. Sau đó, với mỗi câu lệnh, chương trình đọc vào lệnh đó và thực hiện hành động tương ứng trên danh sách `lst`. Các câu lệnh được xử lý bao gồm:

- `insert i e`: chèn phần tử `e` vào vị trí `i` trong danh sách
- `print`: in ra danh sách hiện tại
- `remove e`: xóa phần tử `e` đầu tiên trong danh sách
- `append e`: thêm phần tử `e` vào cuối danh sách
- `sort`: sắp xếp danh sách theo thứ tự tăng dần
- `pop`: xóa phần tử cuối cùng trong danh sách
- `reverse`: đảo ngược danh sách

Lưu ý rằng các phần tử được chèn vào danh sách đều là số nguyên, và phần tử bị xóa cũng là một số nguyên.




Bài toán "Finding the percentage" trên Hackerrank yêu cầu tính điểm trung bình của một học sinh trong lớp học dựa trên tên của học sinh và điểm số của họ. Đầu vào sẽ gồm một số nguyên N cho biết số học sinh trong lớp, sau đó là N dòng, mỗi dòng chứa tên của một học sinh theo đúng thứ tự và một danh sách số thực biểu thị điểm số của học sinh đó ở các môn học khác nhau. Yêu cầu của bài toán là in ra điểm trung bình của học sinh có tên được cung cấp.

Dưới đây là một lời giải bằng Python cho bài toán này:

```python
n = int(input())
student_marks = {}
for _ in range(n):
    line = input().split()
    name, scores = line[0], line[1:]
    scores = list(map(float, scores))
    student_marks[name] = scores
query_name = input()

if query_name in student_marks:
    avg_score = sum(student_marks[query_name])/len(student_marks[query_name])
    print("{:.2f}".format(avg_score))
```

Cụ thể, lời giải này bắt đầu bằng cách đọc vào số lượng học sinh N. Sau đó, với mỗi học sinh, chương trình đọc vào tên và danh sách điểm số của học sinh đó, và lưu trữ chúng trong một từ điển `student_marks`, với tên của học sinh là khóa.

Cuối cùng, chương trình đọc vào tên học sinh cần tính điểm trung bình và in ra điểm trung bình đó nếu học sinh có tên đó có trong danh sách `student_marks`.

Lưu ý rằng kết quả được in ra với định dạng là số thực có 2 chữ số sau dấu phẩy, do đó ta sử dụng phương thức `format` để định dạng kết quả in ra.