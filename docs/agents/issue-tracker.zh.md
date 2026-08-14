# Issue tracker：GitHub

[English](issue-tracker.md) | 中文

本仓库的 Issue 和规格说明记录在 GitHub Issues 中。所有操作使用 `gh` CLI（命令行界面）。

## 约定

- **创建 Issue**：`gh issue create --title "..." --body "..."`。多行正文使用 heredoc。
- **读取 Issue**：运行 `gh issue view <number> --comments`，使用 `jq` 筛选评论并获取标签。
- **列出 Issue**：运行 `gh issue list --state open --json number,title,body,labels,comments --jq '[.[] | {number, title, body, labels: [.labels[].name], comments: [.comments[].body]}]'`，并按需添加 `--label` 和 `--state` 筛选条件。
- **评论 Issue**：`gh issue comment <number> --body "..."`
- **添加或移除标签**：`gh issue edit <number> --add-label "..."` 或 `--remove-label "..."`
- **关闭 Issue**：`gh issue close <number> --comment "..."`

仓库从 `git remote -v` 推断；在 clone 内运行时，`gh` 会自动完成这一步。

## PR 作为 triage 入口

**PR 是否作为请求入口：no。** _（如果本仓库将外部 PR（Pull Request）视为功能请求，可设为 `yes`；`/triage` 会读取此标记。）_

设为 `yes` 后，PR 通过对应的 `gh pr` 命令使用与 Issue 相同的标签和状态：

- **读取 PR**：`gh pr view <number> --comments` 和 `gh pr diff <number>`。
- **列出待 triage 的外部 PR**：运行 `gh pr list --state open --json number,title,body,labels,author,authorAssociation,comments`，仅保留 author association 为 `CONTRIBUTOR`、`FIRST_TIME_CONTRIBUTOR` 或 `NONE` 的 PR。
- **评论、添加标签或关闭**：使用 `gh pr comment`、`gh pr edit --add-label` 或 `--remove-label`，以及 `gh pr close`。

GitHub 的 Issue 和 PR 共用编号空间。遇到单独的 `#42` 时，先运行 `gh pr view 42`，再回退到 `gh issue view 42`。

## 当 skill 要求“发布到 issue tracker”时

创建 GitHub Issue。

## 当 skill 要求“获取相关 ticket”时

运行 `gh issue view <number> --comments`。

## Wayfinding 操作

供 `/wayfinder` 使用。**Map** 是一个 Issue，**child** Issue 是其 ticket。

- **Map**：带有 `wayfinder:map` 标签的 Issue，正文包含 Notes、Decisions-so-far 和 Fog。使用 `gh issue create --label wayfinder:map` 创建。
- **Child ticket**：将 Issue 作为 GitHub sub-issue 关联到 map。如果 sub-issue 不可用，就把它加入 map 正文的任务列表，并在其正文顶部写入 `Part of #<map>`。添加 `wayfinder:<type>` 标签，其中 type 为 `research`、`prototype`、`grilling` 或 `task`。
- **阻塞关系**：使用 GitHub Issue dependencies。运行 `gh api --method POST repos/<owner>/<repo>/issues/<child>/dependencies/blocked_by -F issue_id=<blocker-db-id>` 添加关系；`<blocker-db-id>` 是 `gh api repos/<owner>/<repo>/issues/<n> --jq .id` 返回的数字 database ID。dependencies 不可用时，在 child 正文中添加 `Blocked by: #<n>, #<n>`。
- **Frontier 查询**：列出 map 的开放 child，排除已分配或存在开放 blocker 的 ticket，然后选择 map 顺序中的第一个。
- **领取**：运行 `gh issue edit <n> --add-assignee @me`；这是会话中的第一次写操作。
- **解决**：评论回答、关闭 ticket，再把 context pointer 追加到 map 的 Decisions-so-far。
