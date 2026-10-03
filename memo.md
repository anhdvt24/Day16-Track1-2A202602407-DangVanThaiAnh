# Memo Teardown — Cursor

**Họ tên:** Đặng Văn Thái Anh

**Vì sao chọn sản phẩm này:** (1–2 câu) Cursor là một sản phẩm AI-native trong software development, có lịch sử công khai đủ rõ để dựng timeline từ codebase context → AI editing → Agent → Background Agent → multi-agent → enterprise governance. Pain point cũng cụ thể: giảm thời gian coding/context switching và dần chuyển từ hỗ trợ cá nhân sang tự động hóa engineering workflow.

**§1. Timeline các cập nhật lớn**

| Thời điểm | Cập nhật | Context lúc đó | Nguyên lý |
|---|---|---|---|
| **06/2023** | **Codebase Context v1** — Cursor đưa context của toàn bộ codebase vào Chat/Search, cho phép AI trả lời dựa trên repository thay vì chỉ đoạn code hiện tại. [Nguồn](https://www.cursor.com/changelog/codebase-context-v1) | AI coding assistant lúc đó chủ yếu giải quyết đoạn code/file hiện tại. Vấn đề lớn là model thiếu context về cấu trúc và quan hệ giữa các file trong repository. | **Wrapper → Moat:** giá trị không chỉ nằm ở foundation model; lớp retrieval/context chuyên biệt cho codebase tạo thêm giá trị mà một chatbot tổng quát không tự có. |
| **03/2024** | **Custom Cursor Tab model** — Cursor bắt đầu dùng model riêng được train để dự đoán edit trong code; về sau Tab mở rộng sang dự đoán cả edit và “jump” tiếp theo. [Nguồn](https://www.cursor.com/blog/tab-update) | Autocomplete truyền thống chủ yếu dự đoán text tiếp theo. Cursor nhận ra việc chỉnh sửa code còn gồm navigation và thay đổi nhiều phần liên quan. | **x10:** không chỉ làm autocomplete tốt hơn mà giảm thêm thao tác lặp lại trong toàn bộ quá trình editing. |
| **08/2024** | **Series A và định vị lại ambition** — Cursor công bố $60M Series A và hơn 40.000 customers; công ty mô tả mục tiêu dài hạn là xây công cụ có thể viết phần lớn phần mềm. [Nguồn](https://cursor.com/blog/series-a) | Cursor đã vượt giai đoạn thử nghiệm ban đầu và bắt đầu có quy mô user đủ lớn để đầu tư sâu vào model, retrieval và code rewriting. | **x10:** Cursor nâng đơn vị giá trị từ “code assistant hỗ trợ cá nhân” lên “công cụ viết phần lớn phần mềm” — mở rộng đơn vị công việc mà AI có thể đảm nhận, đồng thời mở ra không gian cho các bước nhảy tiếp theo (Agent, Background Agent). |
| **12/2024** | **Agent trở thành workflow thực thi nhiều bước** — Agent có thể chạy command, đọc exit code/linter errors, tự sửa lỗi, dùng docs/git/web/folder context và chỉnh nhiều vị trí song song. [Nguồn](https://cursor.com/changelog/0-44-x) | Foundation models đã đủ khả năng thực hiện chuỗi hành động thay vì chỉ sinh một đoạn code. Giới hạn chuyển từ “AI viết code” sang “AI có thể hoàn thành task đến đâu?”. | **x10:** tăng đơn vị công việc mà AI có thể đảm nhận: từ suggestion/edit → engineering task có nhiều bước. |
| **05/2025** | **Background Agent** — Agent có thể chạy song song, từ xa và trong môi trường riêng; user có thể theo dõi, gửi follow-up hoặc take over. [Nguồn](https://cursor.com/changelog/0-50) | Khi agent xử lý task lớn hơn, việc bắt developer phải ngồi trước IDE chờ từng bước trở thành bottleneck mới. | **x10:** loại bỏ human-in-the-loop ở những bước không cần thiết và chuyển từ synchronous copilot sang asynchronous software worker. |
| **10/2025** | **Cursor 2.0 + Composer** — Cursor ra mắt coding model riêng Composer và giao diện mới tập trung vào nhiều agent chạy song song thay vì chỉ xoay quanh file. [Nguồn](https://cursor.com/blog/2-0) | Foundation models ngày càng phổ biến và nhiều đối thủ có thể gọi cùng các model frontier. Cursor cần khác biệt ở coding-specific model, agent tooling và workflow. | **Wrapper → Moat:** xây năng lực chuyên biệt cho software engineering ở model + tools + agent harness, thay vì chỉ là UI wrapper quanh model bên ngoài. |
| **02/2026** | **Cloud agents có thể điều khiển máy tính riêng** — agent có VM/development environment riêng, có thể test phần mềm, tạo screenshot/video/logs và tạo merge-ready PR. [Nguồn](https://cursor.com/blog/agent-computer-use) | Agent không chỉ cần viết code; để tự chủ hơn, nó phải chạy và sử dụng chính phần mềm mà nó đang xây để kiểm chứng kết quả. | **Vertical AI + Wrapper → Moat:** Cursor xây năng lực chuyên biệt cho software engineering (VM riêng, test runtime, merge-ready artifact) — domain expertise mà foundation model đơn thuần không có, đồng thời tạo moat mới khó copy từ các coding assistant chỉ wrap model. |
| **06/2026** | **Organizations cho Cursor Enterprise** — doanh nghiệp có thể quản lý nhiều teams với budget, security, governance, feature/model controls và usage analytics ở cấp organization. [Nguồn](https://cursor.com/blog/organizations) | User đã mở rộng từ individual developer sang engineering organizations. Khi nhiều team cùng dùng agent, bài toán mới là governance, budget, security và kiểm soát adoption. | **Vertical AI / Domain expertise + Moat:** Cursor đưa AI vào workflow software engineering ở cấp tổ chức, bổ sung governance và operational layer mà foundation model đơn thuần không cung cấp. |

**Vì sao chọn những mốc này:** Tôi chọn các mốc trên vì mỗi mốc đại diện cho một thay đổi về **đơn vị công việc hoặc customer problem**, không chỉ là một feature release nhỏ. Tôi loại các hotfix, bug fix, UI refresh và các model update nhỏ vì chúng cải thiện execution nhưng không làm thay đổi đáng kể product strategy. Ví dụ, các bản vá SSH, crash hoặc memory/performance được Cursor liệt kê trong changelog nhưng không đủ tư cách là một “quyết định sản phẩm” độc lập. [Nguồn](https://www.cursor.com/en/changelog)

**§2. Tệp user & JTBD**

| | Early adopters | Tệp hiện tại |
| **Đặc điểm** | Individual software developer/engineer ở startup hoặc team nhỏ; quen VS Code, Git, terminal; sẵn sàng thử AI coding tools và ưu tiên tốc độ phát triển. | Engineering teams và enterprise organizations; gồm senior engineers, engineering managers, DevEx/engineering leaders và CTO-level buyers; cần AI productivity nhưng đồng thời quan tâm security, governance, budget và visibility. |
| **JTBD chính** | **“Khi tôi xây dựng hoặc sửa phần mềm, tôi muốn biến ý định thành code chạy được với ít thao tác tìm kiếm, gõ code và context switching hơn, để hoàn thành feature/fix nhanh hơn.”** | **“Khi team của tôi phát triển phần mềm ở quy mô lớn, tôi muốn AI có thể thực hiện nhiều engineering tasks nhưng vẫn kiểm soát được security, model access, spending và workflow của tổ chức.”** |
| **Trước đó họ làm bằng cách nào** | VS Code + Git + terminal + GitHub Copilot/ChatGPT + Google/Stack Overflow + tự đọc codebase và tự debug. | IDE + GitHub/Copilot hoặc AI coding tools + internal engineering processes; quản lý team và security bằng các công cụ enterprise riêng. |

**Dịch chuyển tệp:**
 **Mốc 12/2024 — Agent** là bước chuyển quan trọng từ individual productivity sang task automation: AI không chỉ gợi ý code mà có thể chạy command, đọc lỗi và chỉnh nhiều vị trí. [Nguồn](https://cursor.com/changelog/0-44-x)

**Mốc 05/2025 — Background Agent** làm shift rõ hơn: developer có thể giao task cho agent chạy từ xa và quay lại review kết quả, mở đường cho workflow team thay vì chỉ tương tác trực tiếp trong editor. [Nguồn](https://cursor.com/changelog/0-50)

**Mốc 06/2026 — Organizations** xác nhận segment enterprise đã trở thành một bài toán sản phẩm riêng: Cursor cho phép nhiều team nằm dưới một organization với budget, governance, model controls và analytics. [Nguồn](https://cursor.com/blog/organizations)

**Switching cost (map 4 forces):** 
| Force | Phân tích với Cursor |
|---|---|
| **Push** — vấn đề với giải pháp hiện tại | Coding truyền thống và các tool AI đơn giản vẫn tạo context switching: developer phải tự tìm code, documentation, lỗi, rồi chuyển giữa IDE và chatbot. Product Hunt reviews thường nhắc tới codebase context, multi-file edits, debugging và giảm context switching như các giá trị chính. [Nguồn](https://www.producthunt.com/products/cursor) |
| **Pull** — sức hút của Cursor | VS Code-style workflow, codebase-aware context, autocomplete, multi-file editing, Agent và Background Agent khiến AI nằm trực tiếp trong workflow thay vì là chatbot bên ngoài. |
| **Habit** — thói quen cũ | Developer đã quen editor, shortcuts, extensions, Git, terminal và cách review diff. Cursor có lợi thế adoption vì giữ workflow kiểu VS Code; review trên Product Hunt cũng ghi nhận việc giữ extensions/custom shortcuts giúp migration dễ hơn. [Nguồn](https://www.producthunt.com/products/cursor) |
| **Anxiety** — nỗi lo khi chuyển/ở lại | Chi phí/usage khó dự đoán, context loss, hallucination, code agent sửa sai, resource usage và stability là các lo ngại được phản ánh trong reviews. Với enterprise còn có privacy, security và governance. [Nguồn](https://www.producthunt.com/products/cursor) |

Kết luận 4 forces

**Lực giữ user ở lại mạnh nhất hiện tại có vẻ là workflow lock-in hơn là data lock-in.** Cursor nằm trong editor và gắn với codebase, Git, terminal, extensions, rules và agent workflow; vì vậy chuyển sang một tool khác có thể đồng nghĩa với việc thay đổi cách developer thực hiện công việc hằng ngày. Tuy nhiên, switching cost chưa phải tuyệt đối cao vì nhiều đối thủ vẫn có thể giải quyết cùng JTBD và Cursor vẫn dựa trên workflow VS Code.

**Nếu workflow lock-in biến mất** — ví dụ một đối thủ cung cấp cùng mức codebase context, agent capability và UX mà không yêu cầu thay đổi workflow — user có thể chuyển đổi tương đối dễ hơn. Vì vậy Cursor cần tiếp tục tạo moat ở agent reliability, coding-specific models, tools, workflow và enterprise controls.

**§3. Ba dự đoán hướng đi (6–12 tháng tới)**

**Dự đoán 1** *(loại: mở rộng tính năng)*
- **Dự đoán:** Cursor sẽ tiếp tục chuyển từ “một agent làm một task” sang **orchestration của nhiều agent**, với delegation, routing, verification và automation ở cấp project/team.
- **Lập luận:** … §1 cho thấy Cursor đã đi từ Tab → Agent → Background Agent → Composer/multi-agent → agent có môi trường máy tính riêng; Cursor 2.0 đã thiết kế interface xoay quanh nhiều agent và tháng 12/2025 đã có multi-agent judging để tự đánh giá các kết quả song song. [Nguồn](https://cursor.com/blog/2-0) [Nguồn](https://cursor.com/changelog/2-2)

**Dự đoán 2** *(loại: mở rộng segment)*
- **Dự đoán:** Cursor sẽ tiếp tục đẩy sâu vào **large engineering organizations**, mở rộng governance, security, budget, model policy, analytics và organization-wide agent controls.
- **Lập luận:** §2 cho thấy user đã dịch từ individual developer sang team/enterprise; tháng 06/2026 Cursor đã đưa Organizations vào Enterprise, cho phép quản lý nhiều teams, budget, security, feature/model controls và usage analytics ở cấp công ty. [Nguồn](https://cursor.com/blog/organizations)

**Dự đoán 3** *(loại: thay đổi mô hình kiếm tiền)*
- **Dự đoán:** Cursor sẽ tiếp tục kết hợp **seat-based pricing với usage/compute economics**, đặc biệt phân biệt heavy agent users với normal users.
- **Lập luận:** §1–§2 cho thấy workload đã chuyển từ autocomplete sang long-running/background agents, làm usage và inference cost biến động hơn; tháng 06/2026 Cursor đã có Standard/Premium seats, các usage pools riêng và spend controls cho Teams. [Nguồn](https://cursor.com/blog/teams-pricing-june-2026)

### Câu hỏi phản biện

**Dự đoán tôi tự tin nhất:** Dự đoán 1 — agent orchestration.

**Giả định có thể làm nó gãy:** việc chạy nhiều agent song song phải tạo productivity gain lớn hơn coordination overhead. Nếu agents vẫn cần developer micromanage quá nhiều, lỗi giữa các agents khó kiểm soát hoặc chi phí compute tăng nhanh hơn giá trị tạo ra, Cursor có thể phải ưu tiên reliability của single-agent workflow thay vì tiếp tục tăng số lượng agent.
**§4. AI Log**

| Việc | AI làm hay bạn làm? | Bạn kiểm chứng/phán đoán lại thế nào? |
|---|---|---|
| Tìm các milestone ứng viên | **AI hỗ trợ research** | Đối chiếu từng milestone với Cursor changelog/blog chính thức; loại hotfix và feature nhỏ nếu không thể hiện thay đổi product strategy. |
| Xác định thời điểm và nội dung milestone | **AI tổng hợp; người làm bài kiểm chứng** | Mở link nguồn gốc của Cursor và kiểm tra ngày + nội dung trước khi nộp. |
| Revert milestone về nguyên lý | **AI đề xuất; người làm bài phán đoán** | Kiểm tra xem nguyên lý có phải concept đã học trong Day 16 và có giải thích được “vì sao nước đi này xảy ra” hay chỉ là nhãn chung chung như “tăng trưởng”. |
| Xác định early adopter/current user | **AI tổng hợp từ nguồn công khai; người làm bài phán đoán** | So sánh với Product Hunt reviews và các thay đổi Teams/Enterprise của Cursor; không coi claim marketing của Cursor là bằng chứng duy nhất. |
| Viết JTBD | **AI hỗ trợ draft; người làm bài phán đoán** | Kiểm tra JTBD có mô tả “việc cần làm” hay đang vô tình mô tả một feature như “cần AI chatbot/Agent”. |
| Phân tích 4 forces | **AI hỗ trợ cấu trúc; người làm bài phán đoán** | Đối chiếu Push/Pull/Habit/Anxiety với reviews và workflow thực tế; đặc biệt kiểm tra giả thuyết “workflow lock-in” có evidence hay chỉ là suy luận. |
| Ba dự đoán 6–12 tháng | **Chủ yếu là phán đoán của người làm bài, AI chỉ hỗ trợ phản biện** | Mỗi prediction phải truy ngược được ít nhất một milestone ở §1 hoặc nhận định user ở §2; nêu rõ assumption có thể làm prediction sai. |
| Kiểm tra tính trung thực của AI log | **Người làm bài chịu trách nhiệm cuối cùng** | Không ghi “tôi tự research” cho những phần AI đã tìm/tổng hợp; các link và claim quan trọng phải được người làm bài mở và kiểm chứng trước khi nộp. |
---

