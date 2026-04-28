## 本地生成与发布说明

简明步骤（在 Windows PowerShell）：

1. 前提工具
   - Python 3.8+
   - LaTeX（含 latex 可执行程序）
   - dvipng

2. 在仓库根目录（含 `jemdoc.py`）的推荐做法

   - 从 `www` 目录生成到 `html/`（PowerShell）：

```powershell
cd www
python ..\jemdoc.py -c jemdoc.conf -o ..\html\ index.jemdoc biography.jemdoc publications.jemdoc projects.jemdoc services.jemdoc
```

   - 在类 Unix / Git Bash 下：

```bash
cd www
python ../jemdoc.py -c jemdoc.conf -o ../html/ index.jemdoc biography.jemdoc publications.jemdoc projects.jemdoc services.jemdoc
```

3. 注意事项
   - `jemdoc.py` 已做了 Python3 兼容修改，仍可能产生少量 SyntaxWarning（来自旧正则字符串），这些通常为警告且不影响生成。
   - 若出现 LaTeX/ dvipng 错误，公式图片生成会失败；可以临时通过 `-c jemdoc.conf` 中关闭公式支持或安装相应工具。

4. 部署到 GitHub Pages
   - 如果这是用户页面（repository 名称为 `yourname.github.io`），将仓库推到远端（push 到 `main` 或 `master`），GitHub 会自动在 `https://yourname.github.io/` 提供站点。
   - 如果是 repo page（非 special 名），可在仓库设置中选择 `gh-pages` 分支或将生成后的 `html/` 内容发布到 `gh-pages` 分支。
   - 使用自定义域：在仓库根目录添加 `CNAME` 文件，内容为你的域名，并在 GitHub 仓库设置中配置 Pages 的自定义域。

5. 持续集成（可选）
   - 本仓库已包含一个示例 GitHub Actions workflow（见 `.github/workflows/DeployJemdoc.yml`），可用于自动构建并把生成的 `html/` 发布到 Pages。确认 workflow 配置与分支匹配并启用 Actions。

6. 常见问题排查
   - 若遇到 `Missing parentheses in call to 'print'`：表示使用了 Python2 脚本，请用 Python3 运行（本仓库已转换）。
   - 若看到 `latex: not found` 或 `dvipng: not found`：安装 LaTeX 套件并确保可执行在 PATH 中。

如果需要，我可以：
- 把 `GENERATE_AND_DEPLOY.md` 的内容合并进现有 `README.md`，或
- 提交并创建一个 PR（或直接 commit），并添加一个小脚本 `make-html.ps1` 来简化生成命令。

-- 生成脚本由我在仓库中运行并验证过（输出文件位于 `html/`）。
