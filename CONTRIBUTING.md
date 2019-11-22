# Hướng dẫn và quy tắc khi đóng góp

Chào mừng bạn đến với kho tài liệu Tiếng Việt của Gatsby! Trước hết, nhóm bảo trì của Gatsby muốn gửi đến bạn lời cảm ơn vì đã quan tâm và mong muốn đóng góp cho Gatsby trở nên dễ tiếp cận hơn trong Tiếng Việt.

Đây là một tài liệu quan trọng, hữu ích và cũng là hướng dẫn mà mọi người phải tuân theo để có thể bắt đầu đóng góp cho Gatsby.

## Giới thiệu về kho lưu trữ

Tài liệu cho Gatsby là tập hợp những trang được viết bằng [Markdown](https://dillinger.io/) (một ngôn ngữ đánh dấu đơn giản và dễ tiếp cận). Những trang này khi hoàn tất sẽ được hiển thị trên website tài liệu chính thức của [Gatsby](https://www.gatsbyjs.org/). Từng tập tin Markdown (*.md) tương ứng với một trang tài liệu và cần được dịch sang Tiếng Việt. Nhóm bảo trì của Gatsby đã và đang cố gắng làm việc này, bạn có thể xem [tiến độ phiên dịch](https://github.com/gatsbyjs/gatsby-vi/issues/1) trong mục [Vấn đề](https://github.com/gatsbyjs/gatsby-vi/issues) của kho lưu trữ này. Trang tiến độ phiên dịch sẽ cho bạn thấy những trang đã được dịch và những trang cần được dịch.

## Hướng dẫn

Chúng tôi biết rằng bạn muốn giúp đỡ chúng tôi trong việc phiên dịch một cách nhanh chóng nhưng chúng tôi có một quy trình để đảm bảo rằng việc dịch thuật diễn ra trôi chảy.

### Nhận trang cần dịch

Hãy vui lòng thực hiện theo những bước sau sau để nhận trang cần dịch. Chúng tôi mong muốn rằng thời gian và công sức bạn bỏ ra thực sự có ích và tránh việc nhiều người đóng góp cùng dịch những tài liệu bị trùng lặp.

1. Đi đến trang [tiến độ phiên dịch](https://github.com/gatsbyjs/gatsby-vi/issues/1) và chọn một trong những trang cần được dịch. Những trang chưa được dịch sẽ chưa được đánh dấu. Ví dụ:

    * [ ] community/code-of-conduct

    Lưu ý rằng bạn chỉ được chọn 1 trang trong 1 lần dịch.

1. Khi bạn đã có trang bạn mong muốn dịch, hãy để lại một comment bên dưới phần bình luận để nhóm bảo trì có thể chỉ định bạn cho trang đó. Nếu có thể, hãy đính tên một thành viên nhóm bảo trì trong comment. Ví dụ:

    @vitokhangnguyen Mình muốn dịch trang  `tutorial/part-seven`.

1. Chờ đến khi một thành viên của nhóm bảo trì trả lời comment và chỉ định trang cần dịch cho bạn. Bạn sẽ thấy tên Github của bạn được đặt cạnh tên trang cần dịch trong trang tiến độ phiên dịch. Ví dụ:

    * [x] tutorial/part-seven

1. Bắt đầu dịch  :white_check_mark:

Trong những phần tiếp theo, chúng tôi sẽ hướng dẫn bạn cách clone bản dịch về máy và nộp bản dịch bằng cách thực hiện Pull Request.

### Clone kho lưu trữ và bắt đầu dịch

Thật tuyệt vời nếu đây là lần đầu tiên bạn đóng góp cho cộng đồng phần mềm mã nguồn mở! Trong phần này, Chúng tôi sẽ hướng dẫn bạn thực hiện một quy trình sử dụng Git và Github để lưu toàn bộ kho lưu trữ về máy tính cá nhân của bạn để bạn sẵn sàng cho bản dịch đầu tiên.

Đừng lo lắng khi bạn chưa quen với quy trình này. Bạn luôn có thể liên hệ chúng tôi để nhận được sự giúp đỡ!

#### Những công cụ cần thiết

Bạn cần cài đặt những phần mềm sau trong máy tính của bạn để có thể đóng góp:

* [Git](https://git-scm.com/)
* Một terminal - cửa sổ gõ dòng lệnh (ví dụ: PowerShell, Windows Terminal, Git Bash...)
* Một chương trình chỉnh sửa văn bản (ví dụ: Notepad++, Sublime, Visual Studio Code...). Chúng tôi khuyến cáo Visual Stdio Code vì hỗ trở tốt định dạng Markdown và có các tiện ích bổ sung hữu ích.

#### Quy trình

1. Đầu tiên, bạn cần Fork kho lưu trữ về kho của bạn.

    Điều hướng hướng đến kho lưu trữ gốc (tại [đây](https://github.com/gatsbyjs/gatsby-vi)). Hãy bấm vào nút **Fork** ở góc phía trên, bên phải của kho lưu trữ và đợi vài giây để Github sao chép kho lưu trữ gốc về tài khoản cá nhân của bạn.

    Bản sẽ được chuyển hướng đến một kho lưu trữ tương tự như kho lưu trữ gốc với tên người sở hữu là bạn.

1. Tiếp theo, bạn cần Clone kho lưu trữ về máy để tiện làm việc.

    Tại kho lưu trữ mới bạn sở hữu, bấm vào nút **Clone or Download** màu xanh lá bên tay phải và sao chép đường trong pop-up xuất hiện.

    Điều hướng đến nơi bạn muốn chứa kho lưu trữ trên máy tính cá nhân của bạn, mở terminal tại đây (bạn có thể click chuột phải và chọn `Git Bash Here`) và thực hiện câu lệnh sau với `<URL>` là đường link bạn sao chép phía trên.

    ```bash
    git clone <URL>
    ```
    
    Chờ vài giây để Git clone toàn bộ kho lưu trữ về máy bạn. Sau đó, hãy điều hướng termiank vào trong thư mục chứa kho lưu trữ:

    ```bash
    cd gatsby-vi
    ```

1. Tạo 1 nhánh phát triển (branch) cho kho lưu trữ.

    Khi bạn clone kho lưu trữ về, bạn sẽ mặc định bắt đầu trong nhánh `master`, nơi chỉ nên chứa những tài liệu dịch chính thức. Những thay đổi của bạn trong kho lưu trữ này nên nằm trong một nhánh "tại chỗ" khác.

    Khi bạn đã trong thư mục chứa kho lưu trữ, thực hiện dòng lệnh sau để tạo 1 nhánh phát triển mới với `<TÊN-NHÁNH>` đại diện tài liệu bạn chuẩn bị dịch. Ví dụ: `tutorial-7`, `docs-index`, `code-of-conduct`...

    ```bash
    git checkout -b <TÊN-NHÁNH>
    ```

    Nếu bạn dùng terminal Git Bash hoặc khi bạn chạy lệnh `git branch`, bạn sẽ thấy tên nhánh của bạn đã được đổi từ `master` sang tên mới. Lúc này bạn có thể bắt thực hiện những thay đổi trong kho lưu trữ tại chỗ để bắt đầu dịch trang tài liệu bạn đã được chỉ định.
    
<!-- ## Cách đóng góp

1. Navigate to a folder to store the repository
1. Clone this repository:

    ```bash
    git clone https://github.com/gatsbyjs/gatsby-vi.git
    ```

1. Navigate into the new clone

    ```bash
    cd gatsby-vi
    ```

1. Checkout to a new branch

    ```bash
    git checkout -b <branch-name>
    ```

1. Do your translation or modification.
1. Commit your changes

    ```bash
    git add <filename>
    git commit -m "change description"
    ```

1. Push the change to your own branch

    ```bash
    git push origin <branch-name>
    ```

1. Go to the [translation repository](https://github.com/gatsbyjs/gatsby-vi) and make a Pull Request -->