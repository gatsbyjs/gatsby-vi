---
title: Thiết lập môi trường phát triển
typora-copy-images-to: ./
disableTableOfContents: true
---

Trước khi bắt đầu xây dựng trang web Gatsby đầu tiên của bạn, bạn cần phải làm quen với những công nghệ web cốt lõi và đảm bảo rằng bạn đã cài đặt những phần mềm công cụ cần thiết.

## Làm quen với cửa sổ dòng lệnh

Cửa sổ dòng lệnh (the Command-line) là một giao diện bằng văn bản được dùng để chạy các lệnh trên máy tính của bạn. Bạn cũng sẽ thường thấy nó được đề cập đến với cái tên terminal. Trong bài hướng dẫn này, chúng tôi sẽ sử dụng cả hai một cách thay đổi liên tục cho nhau. Nó rất giống với sử dụng Finder trên Mac hay Explorer trên Windows. Finder và Explorer là những ví dụ của giao diện đồ họa người dùng (graphical user interface - GUI). Cửa sổ dòng lệnh là một cách mạnh mẽ để giao tiếp với máy tính của bạn bằng văn bản.

Hãy dành một chút thời gian để tìm và mở giao diện dòng lệnh (command line interface - CLI) cho máy tính của bạn. Tùy thuộc vào hệ điều hành mà bạn đang sử dụng, hãy xem [Hướng dẫn cho Mac](https://www.macworld.co.uk/how-to/mac-software/how-use-terminal-on-mac-3608274/), [Hướng dẫn cho Windows](https://www.quora.com/How-do-I-open-terminal-in-windows) hoặc [Hướng dẫn cho Linux](https://www.howtogeek.com/140679/beginner-geek-how-to-start-using-the-linux-terminal/).

## Cài đặt Homebrew cho Node.js

Để cài đặt Gatsby và Node.js, nó được đề nghị rằng bạn nên dùng [Homebrew](https://brew.sh/). Một chút thiết lập ban đầu có thể giúp bạn tránh khỏi những lần đau đầu sau này.

Cách để cài đặt và kiểm tra Homebrew trên máy tính của bạn:

1. Mở terminal của bạn.
1. Xem nếu Homebrew đã được cài đặt bằng cách chạy lệnh `brew -v`. Bạn nên thấy được "Homebrew" và số hiệu phiên bản.
1. Nếu không, tải và cài đặt [Homebrew với hướng dẫn](https://docs.brew.sh/Installation) cho hệ điều hành của bạn (Mac, Linux hoặc Windows).
1. Một khi bạn đã cài đặt Homebrew, lặp lại bước 2 để kiểm tra.

### Người dùng Mac: Cài đặt công cụ cửa sổ dòng lệnh cho Xcode

1. Mở terminal của bạn.
1. Trên máy Mac của bạn, cài đặt công cụ cửa sổ dòng lệnh cho Xcode bằng cách chạy lệnh `xcode-select --install`.
   1. Nếu việc đó thất bại, tải nó [trực tiếp từ trang web của Apple](https://developer.apple.com/download/more/), sau khi đằng nhập với tài khoản nhà phát triển của Apple.
1. Sau khi được yêu cầu để bắt đầu quá trình cài đặt, bạn sẽ được yêu cầu lại để chấp nhận một bản quyền phần mềm cho công cụ để tải.

## ⌚ Cài đặt Node.js và npm

Node.js là một môi trường có thể chạy code JavaScript bên ngoài một trình duyệt web. Gatsby được xây dựng với Node.js. Để chạy Gatsby, bạn sẽ cần một phiên bản gần đây của Node.js cài đặt trên máy tính của bạn.

_Lưu ý: Phiên bản Node.js thấp nhất Gatsby hỗ trợ là Node 8, tuy nhiên bạn có thể thoải mái dùng một phiên bản gần đây hơn._

1. Mở terminal của bạn.
1. Chạy lệnh `brew update` để đảm bảo rằng bạn có phiên bản mới nhất của Homebrew.
1. Chạy câu lệnh sau để cài đặt Node và npm trong một lượt: `brew install node`

Một khi bạn đã làm theo những bước cài đặt trên, hãy đảm bảo rằng mọi thứ đã được cài đặt đúng cách:

### Kiểm tra cài đặt Node.js

1. Mở terminal của bạn.
2. Chạy lệnh `node --version`. (Nếu bạn là người mới trong việc sử dụng cửa sổ dòng lệnh, “chạy lệnh `command`” có nghĩa là “gõ lệnh `node --version` vào cửa sổ dòng lệnh, và nhấn Enter”. Từ giờ trở đi, đây là ý của chúng tôi khi chúng tôi nói “chạy lệnh `command`”).
3. Chạy lệnh `npm --version`.

Kết quả của từng lệnh trên là một số hiệu phiên bản. Phiên bản của bạn có thể không giống với những số được hiển thị bên dưới! Nếu việc nhập vào những lệnh trên không hiển thị số hiệu phiên bản, hãy quay ngược trở lại và đảm bảo rằng bạn đã cài đặt Node.js.

![Kiểm tra phiên bản Node và npm trong terminal](01-node-npm-versions.png)

## Cài đặt Git

Git là một hệ thống kiểm soát phiên bản phân tán mã nguồn mở và miễn phí được thiết kế để xử lý mọi dự án từ nhỏ đến lớn với tốc độ và sự hiệu quả. Khi bạn cài đặt một trang Gatsby với mẫu "khởi động", Gatsby sử dụng Git ở hậu cảnh để tải và cài đặt những file cần thiết để bạn bắt đầu. Bạn sẽ cần cài đặt Git để thiết lập trang web Gatsby đầu tiên của bạn.

Những bước để tải và cài đặt Git phụ thuộc vào hệ điều hành của bạn. Hãy làm theo chỉ dẫn dành cho hệ thống của bạn:

- [Cài đặt Git cho macOS](https://www.atlassian.com/git/tutorials/install-git#mac-os-x)
- [Cài đặt Git cho Windows](https://www.atlassian.com/git/tutorials/install-git#windows)
- [Cài đặt Git cho Linux](https://www.atlassian.com/git/tutorials/install-git#linux)

## Sử dụng Gatsby CLI

Công cụ Gatsby CLI cho phép bạn tạo những trang web được hỗ trợ bởi Gatsby một cách nhanh chóng và chạy những câu lệnh để phát triển những trang web Gatsby đó. Nó là một gói npm đã được xuất bản.

Gatsby CLI đã có sẵn thông qua npm và nên được cài đặt một cách toàn cục (globally) bằng cách chạy lệnh `npm install -g gatsby-cli`.

_**Lưu ý**: Khi bạn cài đặt Gatsby và chạy nó lần đầu tiên, bạn sẽ thấy một tín nhắn ngắn thông báo cho bạn về việc dữ liệu ẩn danh được thu thập cho những câu lệnh Gatsby, bạn có thể đọc thêm về cách mà dữ liệu đó được rút ra và sử dụng trong [tài liệu về dữ liệu từ xa](/docs/telemetry)._

Để xem những câu lệnh sẵn có, chạy lệnh `gatsby --help`.

![Kiểm tra những lệnh của Gatsby trong terminal](05-gatsby-help.png)

> 💡 Nếu bạn không thể chạy Gatsby CLI do vấn đề về quyền, bạn có thể muốn xem qua [tài liệu npm về chỉnh sửa quyền](https://docs.npmjs.com/getting-started/fixing-npm-permissions) hoặc [bài chỉ dẫn này](https://github.com/sindresorhus/guides/blob/master/npm-global-without-sudo.md).

## Tạo một trang web Gatsby

Bây giờ bạn đã sẵn sàng để sử dụng công cụ Gatsby CLI để tạo trang web Gatsby đầu tiên của bạn. Sử dụng công cụ đó, bạn có thể tải mẫu "khởi động" (một trang web đã được xây dựng một phần với một số cấu hình mặc định) để giúp bạn tiến lên nhanh hơn trong việc tạo một kiểu trang nhất định. Mẫu khởi động "Hello World" mà bạn sẽ sử dụng tại đây là một mẫu khởi động với những phần thiết yếu tối thiểu cần cho một trang web Gatsby.

1. Mở terminal của bạn.
2. Chạy lệnh `gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world`. (_Lưu ý: Tùy thuộc vào tốc độ tải, thời lượng tiêu tốn cho việc này sẽ khác nhau. Một cách ngắn gọn, ảnh gif dưới đây được tạm dừng trong một phần của quá trình cài đặt_).
3. Chạy lệnh `cd hello-world`.
4. Chạy lệnh `gatsby develop`.

<video controls="controls" autoplay="true" loop="true">
  <source type="video/mp4" src="./03-create-site.mp4" />
  <p>Xin lỗi! Trình duyệt của bạn không hỗ trợ video này.</p>
</video>

Điều gì vừa xảy ra vậy?

```shell
gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world
```

- `new` là một câu lệnh Gatsby để tạo một dự án Gatsby mới.
- Ở đây, `hello-world` là một tên tiêu đề tùy chọn — bạn có thể chọn bất cứ gì. Công cụ CLI sẽ đặt code cho trang web mới của bạn vào một thư mục mới gọi là “hello-world”.
- Cuối cùng, đoạn URL Github được chỉ định trỏ đến một kho lưu trữ code nắm giữ phần code khởi động mà bạn muốn sử dụng.

```shell
cd hello-world
```

- Lệnh này nói rằng 'Tôi muốn chuyển địa chỉ (change directory - cd) đến thư mục con "hello-world". Bất cứ khi nào bạn muốn chạy bất kì lệnh nào cho trang web của bạn, bạn cần phải đang ở trong phạm vi bối cảnh của trang web đó (nói cách khác, terminal của bạn cần được trỏ đến thư mục đang chứa code cho trang web của bạn).

```shell
gatsby develop
```

- Lệnh này khởi động một máy chủ (server) phát trển. Bạn sẽ có thể thấy và tương tác với trang web mới của bạn trong một môi trường phát triển — cục bộ (trên máy tính của bạn, chưa được phát hành lên Internet).

### Xem trang web của bạn một cách cục bộ (local)

Mở một tab mới trong trình duyệt của bạn và điều hướng tới [**http://localhost:8000**](http://localhost:8000/).

![Kiểm tra trang chủ](04-home-page.png)

Chúc mừng bạn! Đây là khởi đầu cho trang web Gatsby đầu tiên của bạn! 🎉

Bạn có thể ghé thăm trang web một cách cục bộ tại [**_http://localhost:8000_**](http://localhost:8000/) miễn là máy chủ phát triển của bạn đang chạy. Đó là tiến trình mà bạn đã bắt đầu bằng cách chạy lệnh `gatsby develop`. Để ngừng chạy tiến trình đó (hoặc là để “ngừng chạy máy chủ phát triển”), hãy trở về cửa sổ dòng lệnh, giữ phím “control”, và nhấn “c” (ctrl-c). Để bắt đầu lại, chạy lại lệnh `gatsby develops`!

**Lưu ý:** Nếu bạn đang sử dụng thiết lập máy ảo như `vagrant` và/hoặc muốn lắng nghe trên địa chỉ IP cục bộ của bạn, hãy chạy lệnh `gatsby develop -- --host=0.0.0.0`. Giờ đây, máy chủ phát triển sẽ lắng nghe trên cả 'localhost' và IP cục bộ của bạn.

## Cài đặt một trình chỉnh sửa văn bản

Một trình chỉnh sửa văn bản là một chương trình được thiết kế cụ thể cho việc chỉnh sửa mã máy tính. Có rất nhiều công cụ rất tốt ở ngoài kia.

### Tải VS Code

Tài liệu của Gatsby đôi khi bao gồm ảnh chụp màn hình được chụp từ VS Code, nên nếu bạn chưa có một công cụ chỉnh sửa văn bản yêu thích, sử dụng VS Code sẽ đảm bảo rằng màn hình của bạn trông giống như những ảnh chụp màn hình trong những bài hướng dẫn và tài liệu. Nếu bạn chọn sử dụng VS Code, hãy đến [trang của VS Code](https://code.visualstudio.com/#alt-downloads) và tải về phiên bản phù hợp cho nền tảng của bạn.

### Cài đặt plugin Prettier

Chúng tôi cũng khuyến cáo sử dụng [Prettier](https://github.com/prettier/prettier), một công cụ giúp định dạng code của bạn nhằm tránh các rủi ro.

Bạn có thể dùng Prettier trực tiếp trong trình sửa văn bản của bạn bằng cách sử dụng [Plugin Prettier cho VS Code](https://github.com/prettier/prettier-vscode):

1. Mở giao diện những thành phần mở rộng (extensions) trong VS Code (View => Extensions).
2. Tìm kiếm với "Prettier - Code formatter".
3. Click vào "Install". (Sau quá trình cài đặt, bạn sẽ được yêu cầu khởi động lại VS Code để kích hoạt thành phần mở rộng. Những phiên bản mới hơn của VS Code sẽ tự động kích hoạt thành phần mở rộng sau khi cài tải về.)

> 💡 Nếu bạn không sử dụng VS Code, hãy xem qua tài liệu của Prettier về [hướng dẫn cài đặt](https://prettier.io/docs/en/install.html) hoặc [tích hợp với trình sửa văn bản khác](https://prettier.io/docs/en/editors.html).

## ➡️ Làm gì tiếp theo?

Để tóm tắt lại, trong phần này, bạn đã:

- Học về cửa sổ dòng lệnh và cách sử dụng nó
- Cài đặt và học vè Node.js và công cụ npm CLI, hệ thống kiểm soát phiên bản Git và công cụ Gatsby CLI
- Tạo ra một trang web Gatsby mới sử dụng công cụ Gatsby CLI
- Chạy máy chủ phát triển Gatsby và tham quan trang web cục bộ của bạn
- Tải một trình chỉnh sửa văn bản
- Cài đặt một trình định dạng code gọi là Prettier

Bây giờ, hãy di chuyển đến trang [**làm quen với các thành phần cấu tạo của Gatsby**](/tutorial/part-one/).

## Tham khảo

### Tổng quan về những công nghệ cốt lõi

Bạn không cần thiết đã phải là một chuyên gia trong những công nghệ đó rồi — nếu bạn không phải, đừng lo lắng! Bạn sẽ góp nhặt được nhiều thứ thông qua quá trình của loạt bài hướng dẫn này. Sau đây là một số những công nghệ web chủ yếu mà bạn sẽ dùng khi xây dựng một trang web Gatsby:

- **HTML**: Một ngôn ngữ đánh dấu mà tất cả các trình duyệt web đều có thể hiểu. Nó viết tắt cho HyperText Markup Language (Ngôn ngữ Đánh dấu Siêu Văn bản). HTML cung cấp cho nội dung trang web của bạn một cấu trúc thông tin phổ thông, định nghĩa những thứ như các đề mục, đoạn văn và hơn thế nữa.
- **CSS**: Một ngôn ngữ trình bày được sử dụng để tạo kiểu cho vẻ bề ngoài của nội dung trang web của bạn (phông chữ, màu sắc, bố cục... vân vân). Nó được viết tắt cho Cascading Style Sheet.
- **JavaScript**: Một ngôn ngữ lập trình giúp chúng ta làm cho trang web năng động và có tính tương tác.
- **React**: Một thư việc code (được xây dựng bằng JavaScript) cho việc xây dựng giao diện người dùng. Nó là bộ khung (framework) mà Gatsby sử dụng để xây dựng những trang và kết cấu nên nội dung.
- **GraphQL**: Một ngôn ngữ truy vấn cho phép bạn kéo dữ liệu vào trang web của bạn. Nó là giao diện mà Gatsby sử dụng để quản lý dữ liệu cho trang web.

### Như thế nào là một trang web?

Để có một sự giới thiệu toàn diện về trang web là gì--bao gồm một phần giới thiệu về HTML và CSS--hãy xem qua trang “[**Xây dựng trang web đầu tiên của bạn**](https://learn.shayhowe.com/html-css/building-your-first-web-page/)”. Đó là một nơi tuyệt vời để bắt đầu học về web. Để có một sự giới thiệu thực tế hơn về [**HTML**](https://www.codecademy.com/learn/learn-html), [**CSS**](https://www.codecademy.com/learn/learn-css) và [**JavaScript**](https://www.codecademy.com/learn/introduction-to-javascript), hãy xem qua những bài hướng dẫn từ Codecademy. [**React**](https://reactjs.org/tutorial/tutorial.html) và [**GraphQL**](http://graphql.org/graphql-js/) cũng có những bài hướng dẫn giới thiệu riêng của họ.

### Tìm hiểu thêm về cửa sổ dòng lệnh

Để có một bài giới thiệu tuyệt vời về việc sử dụng cửa sổ dòng lệnh, hãy xem qua [**Bài hướng dẫn về cửa sổ dòng lệnh của Codeacademy**](https://www.codecademy.com/courses/learn-the-command-line/lessons/navigation/exercises/your-first-command) dành cho người dùng Mac và Linux, và [**Bài hướng dẫn này**](https://www.computerhope.com/issues/chusedos.htm) cho người dùng Windows. Kể cả khi bạn là người dùng Windows, trang thứ nhất của bài hướng dẫn Codeacademy là một bài đọc có giá trị. Nó giải thích cửa sổ dòng lệnh là gì, chứ không chỉ là cách để tương tác với nó.

### Tìm hiểu thêm về npm

npm là một trình quản lý gói (package) cho JavaScript. Một gói là một mô-đun code bạn có thể chọn để bao gồm vào dự án của bạn. Nếu bạn đã tải và cài đặt Node.js, npm đã được cài chung với nó!

npm có ba thành phần riêng biệt: trang web của npm, cơ sở dữ liệu của npm và giao diện dòng lệnh (CLI) của npm.

- Trên trang web của npm, bạn có thể duyệt qua những gói JavaScript có sẵn trong cơ sở dữ liệu npm.
- Cơ sở dữ liệu của npm là một cơ sở dữ liệu lớn chứa thông tin về những gói JavaScript có sẵn trong npm.
- Một khi bạn đã xác định một gói mà bạn muốn, bạn có thể dùng CLI của npm để cài đặt nó vào trong dự án của bạn hoặc một cách toàn cục (global, như những công cụ CLI khác). CLI của npm là thứ mà sẽ giao tiếp với cở sở dữ liệu — bạn phần lớn chỉ tương tác với trang web của npm hoặc CLI của npm.

> 💡 Hãy xem qua giới thiệu về npm, “[**Npm là gì?**](https://docs.npmjs.com/getting-started/what-is-npm)”.

### Tìm hiểu thêm về Git

Bạn sẽ không cần biết Git để hoàn thành bài hướng dẫn này nhưng nó là một công cụ rất hữu ích. Nếu bạn hứng thú trong việc tìm hiểu thêm về kiểm soát phiên bản, Git và Github, hãy xem qua [Cẩm nang về Git](https://guides.github.com/introduction/git-handbook/) của Github.
