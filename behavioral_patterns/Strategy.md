# Strategy

Độ phức tạp: ★☆☆

Độ phổ biến: ★★★

## **🎯 Mục đích**

**Strategy pattern** cho phép bạn xác định một nhóm thuật toán, đặt từng thuật toán vào một lớp riêng biệt và làm cho các đối tượng của chúng có thể hoán đổi cho nhau.

![](../images/strategy.png)

---

## **❓ Vấn đề**

Một ngày nọ, bạn muốn tạo ra một ứng dụng chỉ đường cho khách du lịch. Ứng dụng tập trung vào một bản đồ đẹp mắt, giúp người dùng nhanh chóng xác định vị trí của họ ở bất kỳ thành phố nào.

Một trong những tính năng được yêu cầu nhiều nhất cho ứng dụng là lập kế hoạch lộ trình tự động. Một người dùng có thể nhập vào một địa chỉ và xem lộ trình nhanh nhất tới điểm đích được hiển thị trên bản đồ.

Phiên bản đầu tiên của ứng dụng chỉ có thể xây dựng lộ trình dành cho người lái xe. Những người chạy xe thì rất thích ứng dụng này. Nhưng rõ ràng không phải ai cũng lái xe trong kỳ nghỉ của mình. Vì vậy trong lần cập nhật phiên bản tiếp theo, bạn thêm một tuỳ chọn cho phép xây dựng lộ trình dành cho người đi bộ. Ngay sau đó, bạn thêm một tuỳ chọn khác cho phép mọi người sử dụng các phương tiện giao thông công cộng trong lộ trình của họ.

Tuy nhiên, đó chỉ mới là bắt đầu. Về sau, bạn đã lên kế hoạch xây dựng lộ trình dành cho người đi xe đạp. Và thậm chí sau này, một tuỳ chọn khác để xây dựng lộ trình đi ngang qua các điểm thu hút khách du lịch của thành phố.

![](../images/strategy_problem.png)

Nhìn từ khía cạnh kinh doanh thì ứng dụng của bạn đã thành công, còn về mặt kỹ thuật lại phải khiến bạn phải đau đầu. Mỗi lần bạn thêm một thuật toán xác định lộ trình, class Navigator tăng gấp đôi kích thước. Tại một thời điểm nào đó, ứng dụng sẽ trở nên quá khó để bảo trì.

Bất kỳ thay đổi nhỏ nào đối với một trong các thuật toán đều ảnh hưởng đến toàn bộ class. Điều này làm tăng khả năng gây ra lỗi trong đoạn code đang hoạt động "ngon lành".

Ngoài ra teamwork sẽ trở nên kém hiệu quả hơn. Đồng nghiệp của bạn, những người mà vừa được thuê ngay sau sự thành công của phiên bản đầu tiên, phàn nàn rằng họ dành quá nhiều thời gian để giải quyết merge conflict. Việc tích hợp thêm một tính năng mới buộc bạn phải thay đổi trong cùng một class lớn sẽ tạo ra conflict với code do những người khác tạo ra.

---

## **✅ Giải pháp**

**Strategy pattern** gợi ý bạn sẽ tạo một class thực hiện một điều gì đó theo nhiều cách khác nhau và sẽ chia các thuật toán thành nhiều lớp riêng biệt được gọi là các _chiến lược (strategies)_.

Class ban đầu, được gọi là _context_, phải có 1 trường để lưu tham chiếu đến 1 trong các chiến lược. Context sẽ uỷ quyền thực hiện công việc cho một chiến lược thay vì tự thực hiện nó.

Context sẽ không chịu trách nhiệm chọn thuật toán thích hợp cho công việc đó. Thay vào đó, người dùng sẽ chuyển chiến lược đến cho context. Thực tế context sẽ không biết nhiều về chiến lược. Nó hoạt động với tất cả chiến lược thông qua một generic interface, cái mà chỉ hiển thị một phương thức để trigger thuật toán nằm trong chiến lược đã chọn.

Bằng cách này, context sẽ trở nên độc lập với các chiến lược cụ thể. Vì vậy bạn có thể thêm thuật toán mới hoặc sửa thuật toán của các chiến lược đã tồn tại mà không làm thay đổi code của context hoặc các chiến lược khác.

![](../images/strategy_solution.png)

Trong ứng dụng chỉ đường của chúng ta, mỗi thuật toán xấy dựng lộ trình có thể tách ra nhiều class riêng với một phương thức `buildRoute`. Phương thức này nhận vào điểm hiện tại và điểm đích và trả về một tập hợp các lộ trình.

Mặc dù nhận vào cùng các đối số, mỗi class chiến lược khác nhau sẽ xây dựng lộ trình khác nhau. Class Navigator không cần quan tâm thuật toán nào đã được chọn bởi vì nhiệm vụ chính của nó là hiển thị lộ trình lên trên map. Nó sẽ có một phương thức để thay đổi chiến lược xây dựng lộ trình hiện tại và ví dụ một nút trên giao diện có thể thay đổi chiến lược xây dựng lộ trình hiện tại bằng một chiến lược khác.

---

## **🌏 Liên hệ thực tế**

![](../images/strategy_real_world.png)

Hãy tưởng tượng rằng bạn sẽ đi tới sân bay. Bạn có thể đi xe bus, bắt taxi hoặc đi bằng xe đạp. Đó là những chiến lược vận chuyển của bạn. Bạn có thể chọn 1 trong những chiến lược đó tuỳ vào số tiền hoặc thời gian.

---

## **🏢 Cấu trúc**

![](../images/strategy_structure.png)

1. **Context** duy trì tham chiến đến 1 trong những chiến lược cụ thể và chỉ giao tiếp với đối tượng này thông qua **Strategy** interface.
2. **Strategy** interface xài chung cho tất cả chiến lược cụ thể. Nó khai báo một phương thức mà context sử dụng để thực thi một chiến lược.
3. **Concrete Strategies (Các chiến lược cụ thể)** thực hiện các thuật toán khác nhau mà context sẽ sử dụng.
4. Context sẽ thực thi phương thức trong chiến lược được chọn mỗi khi nó cần chạy thuật toán. Context không biết nó sẽ hoạt động với chiến lược nào hoặc thuật toán được thực thi như thế nào.
5. **Client** sẽ tạo một chiến lược cụ thể và chuyển nó vào context. Context cung cấp một hàm setter cho phép thay thế chiến lược hiện tại của context khi chạy.

---

## **👨‍💻 Code**

```typescript
// Strategy interface khai báo các phương thức chung cho
// tất cả chiến lược. Context sử dụng interface này
// để gọi thực thi thuật toán của các chiến lược cụ thể.
interface Strategy {
  execute(a: number, b: number): number;
}

// Các chiến lược cụ thể triển khai thuật toán
// theo Strategy interface. Interface có thể làm các
// chiến lược có thể hoán đổi cho nhau trong context.
class ConcreteStrategyAdd implements Strategy {
  execute(a: number, b: number): number {
    return a + b;
  }
}

class ConcreteStrategySubtract implements Strategy {
  execute(a: number, b: number): number {
    return a - b;
  }
}

class ConcreteStrategyMultiply implements Strategy {
  execute(a: number, b: number): number {
    return a * b;
  }
}


class Context {
  // Context duy trì một tham chiếu tới 1 trong các
  // chiến lược. Context không biết về lớp cụ thể của
  // một chiến lược. Nó chỉ làm việc với các chiến
  // lược thông qua Strategy interface.
  private strategy: Strategy;

  // Thông thường context sẽ nhận vào 1 chiến lược thông
  // qua constructor và cũng cung cấp 1 phương thức
  // setter để thay đổi chiến lược khi chạy.
  constructor(strategy: Strategy) {
    this.strategy = strategy;
  }

  setStrategy(strategy: Strategy): void {
    this.strategy = strategy;
  }

  // Context sẽ uỷ quyền thực thi tới một object chiến lược
  // thay vì triển khai dưới dạng nhiều phiên bản khác nhau
  // của thuật toán ở bên trong context.
  executeStrategy(a: number, b: number): number {
    return this.strategy.execute(a, b);
  }
}

// Tạo ra một chiến lược cụ thể và chuyển nó vào context.
class ExampleApplication {
  main(): void {
    // Tạo đối tượng context
    const context = new Context(null);

    const firstNumber = // Logic lấy số thứ nhất
    const lastNumber = // Logic lấy số thứ hai
    const action = // Logic lấy hành động

    if (action === "addition") {
      context.setStrategy(new ConcreteStrategyAdd());
    }

    if (action === "subtraction") {
      context.setStrategy(new ConcreteStrategySubtract());
    }

    if (action === "multiplication") {
      context.setStrategy(new ConcreteStrategyMultiply());
    }

    const result = context.executeStrategy(firstNumber, lastNumber);

    console.log(result);
  }
}
```

---

## **💡 Ứng dụng**

🔅 **Sử dụng Strategy pattern khi bạn muốn sử dụng nhiều biến thể khác nhau của một thuật toán bên trong một object và có thể thay đổi sang một thuật toán khác trong khi chạy ở runtime.**

Strategy pattern cho phép bạn thay đổi gián tiếp hành vi của một object tại runtime bằng cách kết hợp với sub-objects khác nhau, có thể thực hiện một việc cụ thể theo nhiều cách khác nhau.

🔅 **Sử dụng Strategy pattern khi bạn có nhiều class giống nhau chỉ khác nhau ở cách mà chúng thực hiện một số hành vi.**

Strategy pattern cho phép bạn tách các hành vi khác nhau thành một hệ thống phấn cấp class riêng biệt và kết hợp các class ban đầu làm một, giảm trùng lặp code.

🔅 **Sử dụng Strategy pattern để tách logic nghiệp vụ của một class khỏi các chi tiết triển khai một thuật toán có thể không quan trọng trong ngữ cảnh của logic đó.**

Strategy pattern cho phép bạn tách code, dữ liệu và các thành phần phụ thuộc của các thuật toán khác nhau ra khỏi phần còn lại. Các đoạn code khác sẽ có một interface đơn giản để thực hiện các thuật toán và có thể chuyển đổi dễ dàng khi chạy ở runtime.

🔅 **Sử dụng Strategy pattern khi class của bạn có một câu lệnh điều kiện lớn chuyển đổi qua lại giữa các biến thể khác nhau của cùng một thuật toán.**

Strategy pattern cho phép bạn loại bỏ các điều kiện như vậy bằng cách tách các thuật toán thành các lớp riêng biệt và tất cả cùng implement một interface. Object ban đầu sẽ uỷ quyền thực thi cho một trong các object này thay vì thực thi hết tất cả biến thể của thuật toán.

## **📋 Cách thực hiện**

1. Trong class context xác định một thuật toán dễ bị thay đổi thường xuyên. Nó có thể là một điều kiện lớn để chọn và thực thi một biến thể khác của cùng một thuật toán khi chạy ở runtime.
2. Khai báo một strategy interface chung cho tất cả các thuật toán.
3. Từng bước tách các thuật toán thành một class riêng và implement strategy interface.
4. Trong context class thêm một trường để tham chiếu đến một object chiến lược. Cung cấp phương thức setter để có thể thay đổi giá trị của trường đó. Context chỉ nên làm việc với object chiến lược thông qua strategy interface. Context có thể định nghĩa một interface cho phép chiến lược truy cập được dữ liệu của nó.
5. Client của context phải kết hợp nó với một chiến lược phù hợp với cách họ mong đợi context thực hiện công việc chính của nó.

## **⚖ Ưu điểm và nhược điểm**

### Ưu điểm

✔ Bạn có thể thay đổi thuật toán bên trong một object khi chạy ở runtime.

✔ Bạn có thể tách biệt cách triển khai thuật toán khỏi đoạn code sử dụng nó.

✔ Có thể thay thế kế thừa (inheritance) bằng thành phần (composition).

✔ Nguyên tắc _Open/Closed_. Bạn có thể thêm chiến lược mới mà không phải thay đổi class context.

### Nhược điểm

❌ Nếu bạn chỉ có vài thuật toán và chúng ít khi thay đổi thì không có lí do gì để phức tạp hoá chương trình với các lớp và interface mới.

❌ Client phải nhận thức được sự khác biệt giữa các chiến lược để có thể đưa ra một chiến lược phù hợp.

❌ Nhiều ngôn ngữ lập trình hiện đại có hỗ trợ functional type cho phép bạn triển khai các phiên bản khác nhau của một thuật toán bên trong một tập hợp các hàm ẩn danh (anonymous function). Sau đó bạn có thể sử dụng các function này như cách bạn sử dụng các object chiến lược nhưng không làm code cồng kềnh hơn với các lớp và interface bổ sung.
