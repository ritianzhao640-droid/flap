# 202工坊 · 对外静态站（代币发布 ＋ 税收金库）

这是一个**纯静态**的网页站：没有账号系统、没有服务端、没有数据库、**没有构建步骤**。
浏览器直接打开 `index.html` 就能看，访问者的钱包自己连区块链、自己签名。

## 三个文件各是什么

| 文件 | 是什么 |
|---|---|
| `index.html` | ★ **入口页**。黑底白字，一屏看完，两个大按钮分别进「发布代币」与「税收金库」。 |
| `publish.html` | **发布代币**页。填名称与图标、选定报价币，一键发一枚新代币；发行费与买入税当场算给你看。 |
| `vault.html` | **税收金库**页。已发出去的币收到的税去哪了：四路分账、能领多少、什么时候能领。 |

另外两件（不进站点、只为交付与核对）：

| 文件 | 是什么 |
|---|---|
| `说明-给挂站的人.txt` | 给挂站的人／平台看的一页说明（怎么放文件、域名怎么指、文件指纹）。 |
| `site-public.zip` | 上面几件打成的 zip，方便整包交给别人。 |

⛔ 这个仓库里**故意没有**任何构建配置（没有 `package.json`、没有 `vercel.json`、没有构建脚本）——
它不需要构建。谁要是往里加构建配置，那就是加错了。

## 怎么部署到 Vercel

1. 把这个仓库推到 GitHub（**根目录**就是这三张页，`index.html` 在根上）；
2. 在 Vercel 里 **Add New… → Project**，选中这个仓库并导入；
3. **Framework Preset 选 `Other`**，Build Command 与 Output Directory **都留空**（不设构建命令）；
4. 点 **Deploy**。Vercel 会把仓库根目录当静态站发布 ⇒ 打开根域名出现的就是 `index.html`。

⛔ 不需要环境变量、不需要 API、不需要任何服务端配置。

## 域名怎么指（xiao17.asia）

★ **一律照 Vercel 界面给出的 DNS 指示配**：在 Vercel 项目的 **Settings → Domains** 里添加
`xiao17.asia`，它会把该填的记录逐条列出来（根域一般是一条 **A 记录**指向 Vercel 给的地址；
`www` 一般是一条 **CNAME** 指向 Vercel 给的名称 —— 以界面显示为准），照它填即可。

⛔ 我们**不在这里写任何 IP 地址**（这是公开仓库，写服务器地址等于对外广播）。
域名的 DNS 由 Vercel 的界面说了算：它给什么，就填什么。

## 文件的 sha256

生成这一刻现算，你可以自己核一遍（Linux／macOS `shasum -a 256 文件名`；
Windows PowerShell `Get-FileHash 文件名 -Algorithm SHA256`）：

    index.html    sha256 = 2527A0FAD0DC4DDE09153581FA9B3EA182460FB81FF6935D0F9A78881EF7047F     3558 字节
    publish.html  sha256 = 38221B0198C422FE228729F2C26C40185BE358CE417621EBF21E59800AA00258     148737 字节
    vault.html    sha256 = 5F9C35353A8E1FEEF8F7A7B80D789B3DB8DA376C54EA3FC0CB73F8806BA65DBC     91040 字节

⛔ 这张表**不列 README.md 自己**：文件里写自己的指纹就变成了自指（写进去，指纹就变了 ⇒ 那句话必假）。
想核它自己，直接 `Get-FileHash README.md -Algorithm SHA256`（Linux／macOS 用 `shasum -a 256 README.md`）。

## 一句话边界

这些页面对链上数据**只读**；交易由访问者在自己的钱包里**亲手签名**。
页面本身不碰私钥、不签名、不广播；这个仓库里也没有任何对内页或内部配置。
