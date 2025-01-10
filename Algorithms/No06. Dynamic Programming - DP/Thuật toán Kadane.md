### Yêu cầu bài toán:

**Bài toán:**  

Cho một mảng số nguyên \( A \) gồm \( n \) phần tử, hãy viết chương trình C/C++ để tìm **tổng lớn nhất của một mảng con** của \( A \).  

- **Mảng con** được định nghĩa là một dãy liên tiếp các phần tử trong mảng gốc. Mảng con phải có ít nhất một phần tử.  

**Đầu vào:**  
1. Dòng đầu tiên chứa một số nguyên \( n \) (\( 1 \leq n \leq 10^5 \)): Số phần tử của mảng.
   
2. Dòng thứ hai chứa \( n \) số nguyên, cách nhau bởi dấu cách: Các phần tử của mảng \( A \) (\( -10^4 \leq A[i] \leq 10^4 \)).  

**Đầu ra:**  

- Một số nguyên duy nhất: Giá trị tổng lớn nhất của mảng con cần tìm.  

**Chú ý:**  

- Dữ liệu đầu vào luôn hợp lệ.
  
- Chương trình cần được tối ưu để xử lý nhanh với \( n \) lớn.

**Ví dụ:**  

*Ví dụ 1:* 

**Đầu vào:**  
```
5
-2 1 -3 4 -1
```
**Đầu ra:**  
```
4
```
(*Mảng con lớn nhất: [4]*)  

*Ví dụ 2:*

**Đầu vào:**  
```
8
-2 -3 4 -1 -2 1 5 -3
```
**Đầu ra:**  
```
7
```
(*Mảng con lớn nhất: [4, -1, -2, 1, 5]*)  

---

Bạn cần hỗ trợ viết code hay giải thích thuật toán nào không? 😊

Bài toán này là một ứng dụng của thuật toán **Kadane**, rất hiệu quả trong việc tìm tổng lớn nhất của một mảng con liên tục trong thời gian \(O(n)\).

### **Đặc điểm của Kadane**:

- **Loại thuật toán**: Dynamic Programming (DP).
  
- **Mục đích**: Tìm **mảng con có tổng lớn nhất** trong một mảng số nguyên 1 chiều.
  
- **Nguyên lý chính**: Tối ưu hóa bài toán bằng cách sử dụng kết quả đã tính từ các bước trước đó (dựa trên tính chất của DP).

---

### **Cách hoạt động của Kadane**:

Kadane dựa trên hai quyết định ở mỗi bước:

1. **Tiếp tục cộng phần tử hiện tại vào tổng của mảng con trước đó**, nếu nó làm tăng tổng.
   
2. **Bắt đầu một mảng con mới từ phần tử hiện tại**, nếu tổng của mảng con trước đó không còn tối ưu.

Nhờ cách tiếp cận này, thuật toán chỉ cần duyệt qua mảng đúng **một lần** để tìm ra kết quả, với độ phức tạp thời gian \(O(n)\).

Dưới đây là mã chương trình bằng C++ để giải bài toán:

```c++
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main() {

    // Đọc số phần tử của mảng
    int n;

    cin >> n;

    // Đọc các phần tử của mảng

    vector<int> A(n);

    for (int i = 0; i < n; ++i) {

        cin >> A[i];
    }

    // Áp dụng thuật toán Kadane để tìm tổng lớn nhất của mảng con

    int maxSum = A[0];

    int currentSum = A[0];

    for (int i = 1; i < n; ++i) {

        currentSum = max(A[i], currentSum + A[i]); // Chọn tiếp tục cộng hay bắt đầu lại từ A[i]

        maxSum = max(maxSum, currentSum);         // Cập nhật tổng lớn nhất
    }

    // In ra tổng lớn nhất

    cout << maxSum << endl;

    return 0;
}
```
### Giải thích mã:

1. **Đọc dữ liệu đầu vào**:
   
   - `n` là số phần tử của mảng.
     
   - Mảng `A` chứa các phần tử số nguyên.

2. **Thuật toán Kadane**:
   
   - `currentSum`: Đại diện cho tổng của mảng con tốt nhất tính đến phần tử hiện tại.
     
   - `maxSum`: Lưu trữ tổng lớn nhất tìm được.
     
   - Ở mỗi bước, kiểm tra:
     
     - **Tiếp tục cộng phần tử hiện tại vào mảng con cũ** hoặc
       
     - **Khởi tạo lại một mảng con mới từ phần tử hiện tại**.
       
   - Cập nhật `maxSum` nếu `currentSum` vượt qua tổng lớn nhất trước đó.

3. **Đầu ra**:
   
   - In ra `maxSum`, là tổng lớn nhất của mảng con liên tục.
