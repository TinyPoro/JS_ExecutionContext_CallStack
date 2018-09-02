# JS_ExecutionContext_CallStack

## Javascript? Execution Context là gì? The Call Stack là gì?

Execution Context trong Javascript là gì?
Tôi cá là bạn cũng không biết được câu trả lời.
Đâu là thành phần quan trọng nhất của 1 ngôn ngữ lập trình?
Các biến là các hàm đúng không? Mọi người đều  có thể học  mảng này.
Nhưng bên trên những thứ cơ bản nhất chúng ta có gì?
Đâu là những thứ quan trọng nhất của Javascript mà bạn nên làm chủ trước khi gọi mình là 1 developer Javascript mức intermediate (hay thậm chí là senior)
Có rất nhiều thứ: Scope, Closure, Callbacks, Prototype, and so on.
Nhưng trước khi đi sâu vào những khái niệm này thì ít nhất bạn cần hiểu được cách mà engine Javascript hoạt động đã.
Trong bài viết này chúng ta sẽ điểm qua 2 thành phần cơ bản của mỗi engine Javascript: the Execution Context và the Call Stack
(Đừng sợ, nó dễ hơn bạn nghĩ nhiều).
Sẵn sàng chưa?
Tài liệu này là một phần trong lớp Javascript nâng cao của tôi cho đào tạo từ xa 1-1 hoặc đào tạo tại chỗ ở châu Âu.

#### Javascript: Execution Context là gì? Những gì bạn sẽ học được
Trong bài này bạn sẽ học được:

- cách Javascript Engine hoạt động
- Execution Context trong Javascript
- Call Stack là gì
- sự khác biệt giữa Global Execution Context và Local Execution Context

#### Javascript: The Execution Context là gì?  Javascript chạy code của bạn như thế nào?
Javascript chạy code của bạn như thế nào?
Nếu bạn là 1 senior developer, bạn hẳn đã biết câu trả lời
Nếu bạn là người mới, chúng ta sẽ cùng nhau làm rõ vấn đề này.
Sự thực là, hiểu được bên trong của Javascript không hề dễ dàng.
Nhưng tôi đảm bảo bạn có thể học được nó.
Và khi bạn càng học, bạn sẽ càng cảm thấy  tự tin và thông minh hơn.
Bằng cách xem xét những chức năng bên trong của Javascript bạn có thể trở thành 1 Javascript developer tốt hơn, thậm chí ngay cả khi bạn không thể thành thao trong bất kỳ lĩnh vực nào.
Giờ xem qua đoạn code sau:
Xong?
Trông nó không hề khó!
Giờ hãy nói tôi nghe: bạn nghĩ trình duyệt sẽ xử lý code này theo trình tự nào?
Hay nói cách khác, nếu Bạn là trình duyệt, bạn  đọc code này thế nào?
Điều này nghe có vẻ dễ dàng.
Hầu hết mọi người đều nghĩ "yeah, trình duyệt sẽ thực hiện hàm pow và trả về kết quả, sau đó nó gán 2 vào num."
Bạn có muốn biết học sinh của tôi trả lời thế nào không?
Từ trên xuống
Trình duyệt sẽ bắt đầu tại hàm pow, tính toán num * num
JS engine chạy code từng dòng
Tôi cũng đã hi vọng như thế.
Tôi cũng nói y như vậy vài năm trước đây.
Trong phần tiếp theo, bạn sẽ được khám phá cách hoạt động đằng sau những  dòng code tưởng chừng đơn giản này.
#### Javascript: The Execution Context là gì? Javascript Engines
Bạn có muốn làm Javascript developer ở mức trung bình không??
Tôi cá là bạn không muốn như vậy đâu
Nếu bạn muốn tạo 1 ấn tượng tốt trong 1 buổi phỏng vấn Javascript bạn ít nhất nên biết về cách JS chạy code của bạn.
(Và một loạt các thứ khác mà tôi sẽ không đề cập ở đây).
Đừng vội lao đầu vào những khái niệm này.
Bạn không thể học được bất cứ thứ gì trong 1 ngày. Sẽ tốn thời gian

Muốn nghe tin tốt không?  Tôi sẽ cố biến những thứ này trở nên dễ hiểu với tất cả mọi người (ít nhất là tôi sẽ cố làm điều đó)
Để hiểu được cách mà JS chạy code của bạn chúng ta sẽ tìm hiểu về thứ đáng sợ nhất: Execution Context.
Vậy Execution Context là gì?
Mỗi lần bạn chạy JS trong trình duyệt (hay trong Node) engine sẽ chạy qua 1 vài bước
1 trong những bước này liên quan đến việc  tạo ra Global Execution Context.
Nhưng khoan đã, engine là cái gì?
Đó là, JS engine là "động cơ" để chạy code JS
Ngay nay có 2 engine JS nổi bật: Google V8 và SpiderMonkey.
V8 là 1 bộ máy JS mã nguồn mở của Google, sử dụng trong Google Chrome và Nodejs,
SpiderMonkey là 1 engine JS của Mozilla, sử dụng trong Firefox.
Và cho tới giờ chúng ta có engine JS và 1 Execution Context.
Giờ là lúc để hiểu cách chúng làm việc với nhau

#### JS: Execution Context là gì? Cách nó hoạt động ra sao?
Engine tạo 1 Global Execution Context mỗi khi bạn chạy code JS.
Execution Context là 1 từ hay được dùng để miêu tả môi trường mà code JS của bạn chạy
Thật khó để mô tả những thứ trừu tượng như thế này
Nên từ giờ hay nghĩ Global Execution Context như là 1 cái hộp vậy
Nhìn lại code của chúng ta 1 chút
Engine sẽ đọc code như thế nào?
Dưới đây là 1 mô tả đơn giản:
Engine: Dòng 1. Có 1 biến! Tuyệt. Hãy lưu nó trong Global Memory.
Engine: Dòng 3. Tôi thấy có 1 khai báo hàm. Tuyệt. Hãy lưu nó trong Global Memory 
Engine: Có vẻ như mình xong rồi.

Nếu tôi hỏi lại bạn 1 lần nữa: cách mà trình duyệt "đọc" những dòng code sau, bạn sẽ nói thế nào?
Yeah, nó vẫn là từ trên xuống nhưng ...
Như bạn có thế thấy là engine không chạy hàm pow!
Nó là 1 khai báo hàm, không phải 1 lời gọi hàm. 
Code trên sẽ được dịch ra thành 1 vài giá trị để lưu trong Global Memory: 1 khai báo hàm và 1 biến.
Global Memory?
Velentino, khi tôi còn đang bối rối về Execution context thì ông lại quăng cho tôi cái Global Memory này ư?
Ừ đúng rồi đấy
Hãy cùng xem Global Memory là gì.

#### Javascript:  Execution Context là gì? The Global Memory
engine JS cũng có 1 Global Memory
Global Memory sẽ chứa các biến toàn cục và các khai bào hàm để sử dụng sau này.
Nếu bạn đọc cuốn "Scope và Closures" của Kyle Simpson bạn có thể nhận ra Global Memory có khá nhiều điểm tương đồng với khái niệm của Global Scope
Trong thực tế thì chúng là 1.
Vì 1 lý do tốt đẹp nào đó, tôi đang bay ở trên độ cao 10000 feet.
Đây là những khái niệm khó. 
Nhưng bạn không nên lo lắng
Bạn muốn hiểu 2 mảnh ghép quan trọng này.
Khi JS engine chạy code của bạn, nó tạo ra:
1 Global Execution context
1 Global Memory( hay còn gọi là Global Scope và Global Variable Environment)
Rõ ràng chưa nào
Nếu tôi là bạn bây giờ tôi sẽ làm như sau:
viết 1 vài dòng code JS
Phân tích code từng dòng như thể bạn là engine vậy
Vẽ 1 sơ đồ thể hiện cả Global Execution context và Global Memory trong qua trình thực thi
Bạn có thể viết bài tập này trên giấy hoặc 1 công cụ  tạo mẫu nào đó.

Với ví dụ nhỏ của tôi thì nó sẽ như thế này:
Trong phần tiếp theo, chúng ta sẽ tìm hiểu 1 thứ đáng sợ khác : Call Stack

#### Javascript: Execution là gì? Call Stack là gì?
Bạn đã có 1 cái nhìn rõ ràng về cách mà Execution Context, Global Memory và JS engine họa động với nhau chưa?
Nếu chưa dành thời gian xem lại phần trước nhé
Giờ chúng tôi sẽ giới thiệu về 1 "miếng ghép" khác: Call Stack.
Hãy xem điều gì xảy ra trong quá trình code thực thi.
Đầu tiên hãy tóm tắt lại những gì xảy ra khi JS engine chạy code của bạn.
Nó đã tạo:
1 Global Execution context
1 Global Memory
Ngoài ra trong ví dụ của chúng ta thì không có gì xảy ra nữa.
Đoạn code là 1 sự phân bố thuần của các giá trị.
Hãy thêm 1 bước nữa.
điều gì sẽ xảy ra khi chúng ta gọi hàm?
1 câu hỏi thú vị.
Hành động gọi 1 hàm trong JS cần sự trợ giúp của engine.
Và sự trợ giúp này tới từ 1 người bạn của JS engine:Call Stack.
Điều này nghe có vẻ k rõ ràng lắm nhưng JS engine cần  theo dõi những gì đang xảy ra.
Điều này được thực hiện dựa vào Call Stack.
Vậy Call Stack trong JS là gì?
Call Stack nó giống như là bản ghi log của quá trình thực thi chương trình hiện tại.
Trong thực tế nó là 1 cấu trúc dữ liệu: 1 stack.
Vậy chính xác thì Call Stack hoạt động thế nào?
KHông ngạc nheien là nó có 2 phương thức: push và pop. 
Pushing là hành động đặt 1 thứ gì đó vào stack
Đó là khi khi bạn chạy 1 hàm JS, engine sẽ push hàm đó vào Call Stack
Mỗi lời gọi hàm sẽ bị đẩy vào Call Stack.
Thứ đầu tiên bị đẩy vào là hàm main()(hay global()), luồng thực thi chính của ứng dụng JS.
Giờ bức ảnh ảnh trước sẽ trông như thế này.

Poping là hành động ngược lại là xóa thứ gì đó khỏi stack.
Khi 1 hàm thực thi xong, nó sẽ bị xóa khỏi Call Stack.
Và Call Stack của chúng ta sẽ trông như sau:

Và giờ bạn đã sẵn sàng để trở thành bậc thầy với mỗi khái niệm JS.

Nhưng giờ chưa xong đâu! Đi tiếp đến phần tiếp theo nào!

#### Advanced Javascript: The Execution Context là gì? The Local Execution Context
Mọi thứ dường như đã rõ ràng hơn.
Chúng ta có bỏ sót điều gì không nhỉ.
Chúng ta đã biết rằng JS engine tạo 1 Global Execution context và 1 Global Memory.
Sau đó khi bạn gọi 1 hàm trong code:
JS engine sẽ yêu cầu sự giúp đỡ từ 1 người bạn của JS engine :Call Stack
Call Stack theo dõi những hàm được gọi trong code của bạn.
1 điều nữa sẽ xảy ra khi bạn chạy 1 hàm trong JS.
Đầu tiên, hàm xuất hiện trong Global Execution context.
Sau đó 1 mini-context khác xuất hiện bên cạnh hàm
Cái box nhỏ mới này được gọi là Local Execution Context.
1 Local Execution Context được tạo bên trong hàm!

Gì cơ??
Nếu bạn để ý, trong bức ảnh trước 1 biến mới xuất hiện trng Global memory: var res.
Các biến res có 1 giá trị không xác định ban đầu.
Sau đó ngay sau khi hàm pow xuất hiện trong Global Execution Context, hàm sẽ thực thi và res sẽ lấy giá trị đó..
Trong phiên thực thi 1 Local Execution Context sẽ được tạo ra, bên cạnh 1 Local Memory cho việc lưu trữ các biến local.

Thật là 1 khái niệm to lớn.
Hãy nhớ lấy nó.
Hiểu được cả Global và Local Execution Context là chìa khóa để trở thành bậc thầy Scope và Closures
#### Javascript: Execution Context là gì? Call Stack là gì? Kết hợp chúng lại
Bạn có tin được những gì đằng sau 4 dòng code kia ko?
JS engine tạo 1 Execution Context, Global Memory, và 1 Call Stack.
Nhưng ngay khi bạn gọi 1 hàm, engine tạo 1 Local Execution Contexxt có 1 Local Memory
Cuối bài viết này bạn nên có thể hiểu được những gì xảy ra khi bạn chạy 1 vài dòng code JS. 
Dù thường bị bỏ qua nhưng những gì bên trong JS thường được xem là những thứ bí ẩn với dev mới.
Giờ chúng là chìa khóa để master các khái niệm JS nâng cao.
Nếu bạn học Executon Context, Global Memory, và Call Stack, sau đó là Scope, Closure, Callbacks và những thứ khác sẽ trở nên dễ như ăn bánh.
Thông thường hiệu được Call Stack là điều tiên quyết.
Tất cả các JS sẽ bắt đầu  trở thành vấn đề 1 khi bạn  nhắc lại nó: bạn cuối cung sẽ hiểu tại sao JS là bất đồng bộ và tại sao chúng ta cần Callback. 
Bạn đã biết những gì đằng sau 4 dòng code kia chưa?
Giờ bạn biết rồi đấy.
