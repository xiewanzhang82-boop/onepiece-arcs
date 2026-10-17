# 素材来源与许可

站里一共有五类外来素材：**六张旧版篇章封面**、**arc2 满屏底图**、**arc2 两条音效**、
**arc2 三件物件（实拍照片）**、**arc2 卡片边框与角饰（实拍照片）**。
除第二类是文生图模型生成的，其余四类都是从维基共享资源下的实拍照片/录音，逐条列了来源页与许可。
第三～第五类还额外记了"怎么处理的"，方便以后重做或换图。

## 一、六张旧版篇章封面（维基共享资源）

六张照片全部来自 **维基共享资源（Wikimedia Commons）**，均为允许商用的许可
（CC BY / CC BY-SA / 公有领域）。三家里 CC BY 与 CC BY-SA 要求署名，
所以这里逐张记下来源页、作者与许可 —— 下面这张表由 `_audit/covers.py` 自动生成，别手改。

| 篇 | 文件 | 原始文件 | 作者 | 许可 |
|---|---|---|---|---|
| 空岛篇 Skypiea | `assets/arc1-cover.jpg` | [Karst peaks with sea of clouds at sunrise, South view from the top of Mount Nam Xay, Vang Vieng, Laos.jpg](https://commons.wikimedia.org/wiki/File%3AKarst_peaks_with_sea_of_clouds_at_sunrise%2C_South_view_from_the_top_of_Mount_Nam_Xay%2C_Vang_Vieng%2C_Laos.jpg) | Basile Morin | CC BY-SA 4.0 |
| 恐怖三桅帆船篇 Thriller Bark | `assets/arc2-cover.jpg` | [2024-06-30 01 SILVA OF HALIFAX - IMO 5327996 - Halifax NS CAN.jpg](https://commons.wikimedia.org/wiki/File%3A2024-06-30_01_SILVA_OF_HALIFAX_-_IMO_5327996_-_Halifax_NS_CAN.jpg) | Gordon Leggett | CC BY 4.0 |
| 顶上战争篇 Marineford | `assets/arc3-cover.jpg` | [Project 1164 Moskva 2012 G4.jpg](https://commons.wikimedia.org/wiki/File%3AProject_1164_Moskva_2012_G4.jpg) | George Chernilevsky | Public domain |
| 鱼人岛篇 Fishman Island | `assets/arc4-cover.jpg` | [Arrecife de coral (Acropora hemprichii, Xenia umbellata, Siderastrea savignyana), parque nacional Ras Muhammad, Egipto, 2022-03-27, DD 92.jpg](https://commons.wikimedia.org/wiki/File%3AArrecife_de_coral_%28Acropora_hemprichii%2C_Xenia_umbellata%2C_Siderastrea_savignyana%29%2C_parque_nacional_Ras_Muhammad%2C_Egipto%2C_2022-03-27%2C_DD_92.jpg) | Diego Delso | CC BY-SA 4.0 |
| 德雷斯罗萨篇 Dressrosa | `assets/arc5-cover.jpg` | [Φηρά 0059.jpg](https://commons.wikimedia.org/wiki/File%3A%CE%A6%CE%B7%CF%81%CE%AC_0059.jpg) | C messier | CC BY-SA 4.0 |
| 蛋糕岛篇 Whole Cake Island | `assets/arc6-cover.jpg` | [Parque estadual ilha do cardoso-THIAGO CAMPI 02.jpg](https://commons.wikimedia.org/wiki/File%3AParque_estadual_ilha_do_cardoso-THIAGO_CAMPI_02.jpg) | Thiago Campi | CC BY-SA 4.0 |

调色由 `_audit/covers.py` 统一完成（去饱和 0.30 / 深褐覆盖 0.62 / 对比 1.06 / 颗粒 5 / 暗角 0.72）。想还原原色，把 `SEPIA_MIX` 调成 0 重跑。

> ⚠️ 第四轮起 arc2 已经不用 `arc2-cover.jpg` 了（换成满屏底图 `arc2-hero.jpg`）。
> 这张封面图还留在 `assets/` 里没删 —— 留着是因为它同时也是"六张封面"那条自动化脚本的产物，
> 删了下次重跑 `covers.py` 又会生出来。真要清干净就连 `covers.py` 里 arc2 那一行一起改。

---

## 二、arc2 满屏底图（AI 生成）

| 文件 | 来源 | 说明 |
|---|---|---|
| `assets/arc2-hero.jpg` | 文生图模型生成 | 1920×1080，电影感写实：古堡尖塔 + 两侧发光红眼 + 夜空月亮 + 横贯铁链 |

- 原始出图存在 `D:\XINXICHA\second brain\generated-images\海贼王篇章站-arc2底图\`（含原始比例稿与预览图）。
- 生成图右下角带「AI生成 WORKBUDDY」水印，**亮度扫描扫不出来**（半透明灰，亮度只有 120 上下）。
  处理办法是**从顶部按 16:9 裁掉底部**（`crop((0, 0, w, int(w * 9 / 16)))`）—— 水印正好落在被切掉的那条里，
  顺手也把图从 1536×1024 变成了 1920×1080 的满屏 16:9。**以后遇到类似水印，别用亮度阈值找，直接裁角放大肉眼确认。**
- 图上两只红眼的中心量出来是 **左 32.0% / 右 69.7%，y ≈ 33.5%**（1920×1080 坐标系）。
  `.op-arc-art` 那个 16:9 图盒是拿 `background-size:100% 100%` 铺图的，**图和盒子 1:1**，
  所以这两个数可以直接照抄进 `.op-arc-eye::before/::after` 的 `left` / `top`。
- 量法（**换底图之后必须重量**）：`红通道 > 205 且 红减蓝 > 45` 取暖色像素，掐掉中轴那一竖条，
  再分左右求质心。别用"亮度 > 235"——那会把月亮一起圈进来。

---

## 三、arc2 音效（维基共享资源，两条真录音）

进 arc2 会自动响，左下角静音钮控制。**两条都是真录音**，下面还叠了一层浏览器现场合成的风声与爆裂声
（脚本第 5 段），合成层不涉及任何素材许可。

| 站里用的文件 | 原始文件 | 作者 | 许可 |
|---|---|---|---|
| `assets/audio/arc2-wind.ogg` | [Killiney Hill Storm Floris 20250804 1537.ogg](https://commons.wikimedia.org/wiki/File:Killiney_Hill_Storm_Floris_20250804_1537.ogg) | Karlunun | CC0 1.0（公有领域献出，署名非强制） |
| `assets/audio/arc2-fire-clean.wav` | [WWS Bonfireburning.ogg](https://commons.wikimedia.org/wiki/File:WWS_Bonfireburning.ogg) | Work With Sounds / Werstas | CC BY 4.0（须署名） |

- 风：1160895 字节 / 68.6 秒。2025-08-04 下午录于爱尔兰都柏林南边的 Killiney Hill（约海拔 150 米），
  原始描述里明确写了 **"no rain"** —— 要的就是纯风啸、不带雨声，10 分钟窗口内阵风一度到 83 km/h。
- 火：原文件 51.88 秒，芬兰仲夏节前夜的篝火（Work With Sounds 项目采集）。
  **站里放的是剪过的版本**：原始录音第 24–28 秒有人在近处讲话，所以只取第 31–51.88 秒，
  末尾 1.5 秒等功率叠进开头 → 19.38 秒无缝循环。剪完 RMS 对齐回原文件的 0.04443，
  所以 `fire.volume = 0.46` 不用改。
  未剪的原文件留在 `_audit/audio-src/arc2-fire.ogg`（不进交付目录），剪法见 `_audit/_audio_trim.js`。
- 两条原始素材都是 Ogg Vorbis，文件头 `4f676753`（"OggS"）—— 下载完顺手校验过。
  剪完这条存成 **WAV**（本机没有 OGG 编码器；PCM 加个 44 字节头就是文件，854KB 可以接受）。
- ⚠️ **千万别把这两个 `<audio>` 接进 `createMediaElementSource`**：`file://` 下会被判成跨源污染，
  整条 Web Audio 链路直接变哑。合成层单独建一张图（`new AudioContext()`），别碰这两个元素。
- 下载时踩的两个坑记在这儿：①维基的图/音频**缩略图宽度只认固定档位**；②连续下载会 **429**，
  两条之间要 `sleep 8` 并带 5 次退避重试，且必须带 User-Agent。直连超时就走代理 `127.0.0.1:7897`。

### 顺带记一下：怎么确认"哪一秒有人在讲话"

本机没有 ffmpeg / librosa，Python 解不了 Ogg，所以是**借 Chrome 的 `decodeAudioData` 把 PCM 解出来**，
在页面里做完分析再把小数据传回 Node。前后试过三把尺子，只有第一把管用，后两把的作用是"排除误报"：

| 尺子 | 怎么量 | 结论 |
|---|---|---|
| **音节调制节律**（主力） | 取 300–3400Hz 包络，看它在 2.5–8Hz 段的能量占比（人说话音节以 3–6Hz 开合） | 管用。arc2-fire 的 p97 = **0.441**，高于全部 5 个候选（0.349–0.456）；逐秒看，第 24–28 秒是 0.81 / 0.84 / **1.00** / **1.00** / 0.78，一秒都不带含糊 |
| 倒谱峰突出度 CPP | log 幅度谱 → 倒谱 → 找基音周期处的峰 | **不管用**。arc2-fire 的可疑段和干净段都是 0.14，分不开（对"远处、被火声糊过的人声"不敏感） |
| 400Hz 高通后算自相关 | 滤掉火自己的低频轰鸣，再看 80–300Hz 延迟区间的周期性 | 用来**排除误报**。arc2-wind 第 58–60 秒被节律尺子判 1.00，但它的 CPP 全程平在 0.128–0.135，高通过后的周期性只有 0.22（人声在 0.5 以上）→ 那是一阵强阵风，不是人声。风保持原样没动 |

> 这套东西值得留着 —— 以后再往站里放环境音，先过一遍"音节调制节律"，逐秒看有没有 0.6 以上的孤峰。
> 脚本：`_audit/_voice_hunt.js`（打分）、`_audit/_voice_verify.js`（自相关复核）、
> `_audit/_audio_clips.js`（切片段给人耳听）。
> ⚠️ 打分是**按文件自己分位数**归一化的，"1.00"只表示"这条录音里最像人讲话的几秒"，
> **不能跨文件比绝对值**；要比绝对值就看 `ratio` 那一列。

---

## 四、arc2 三件物件（维基共享资源，实拍照片）

右上角那三件"道具"——头骨、南瓜灯、三头犬石雕 —— **全是实拍照片抠出来的**，没有一张是 AI 生成的。
理由：这三样东西网上有大量明确长相的实物照片，生成模型反而容易画成卡通简化版。
候选一共下了 19 组、150 多张，拼成总览图挑的；选中的源图和许可如下。

| 站里用的文件 | 原始文件 | 作者 | 许可 |
|---|---|---|---|
| `assets/props/obj-skull.png` | [Skull on turntable.jpg](https://commons.wikimedia.org/wiki/File:Skull_on_turntable.jpg) | Watty62 | CC BY-SA 4.0 |
| `assets/props/obj-pumpkin.png` | [Jack-o'-Lantern 2003-10-31.jpg](https://commons.wikimedia.org/wiki/File:Jack-o%27-Lantern_2003-10-31.jpg) | Toby Ord | CC BY-SA 2.5 |
| `assets/props/obj-cerberus.png` | [Cerberus the three-headed dog (25239496470).jpg](https://commons.wikimedia.org/wiki/File:Cerberus_the_three-headed_dog_%2825239496470%29.jpg) | Thomas Quine | CC BY 2.0 |

**三张都是 1024×1024 的正方形画布、透明底，物件占画布 86%。**
为什么必须正方形：CSS 那边用 `background-size:contain` 按正方形盒子铺图，
源图不是正方形的话，占比会和 `.op-obj::after` 那团暖光斑对不上。
抠图脚本 `_audit/_props_build.py`，候选素材留在 `_audit/props-clean/`（带 `_meta.json`），
中间核对图在 `_audit/props-preview/`。

三张各有一个坑，记在这儿免得重踩：

- **头骨**（源图是"放在转盘上拍的"，转盘边缘比头骨宽得多）：
  黑白正脸，`灰度 < 186` 阈值 + 闭开运算拿到主体，然后**按行扫宽度把转盘切掉**——
  某一整行突然比画布 70% 还宽，就说明从这一行往下都是转盘，整段归零。
  下巴底下那圈白色转盘靠"又靠下（y > 0.80）又很亮"单独按掉，牙齿在界线之上不受影响。
- **南瓜灯**（源图本来就是纯黑底 + 内部暖橙烛光）：**不抠，只裁到本体范围**，
  再叠一层径向 alpha 化进夜色。这源图是这次挑得最省事的一张，抠图几乎零成本。
- **三头犬石雕**（白大理石，背景是浅色墙，颜色和石头几乎一样）：
  纯 GrabCut 会把背景一起粘进来，所以先**手描 32 点多边形**圈出允许区，
  让 GrabCut 只在那圈边界上找真实边缘；再把"细脖子连着的背景碎块"用
  "先腐蚀饿瘦 → 取最大连通域 → 按原轮廓胖回来"甩掉。
  这个轮廓前后调了 4 轮，靠的是脚本吐的 `{name}-overlay.jpg`（把 alpha 轮廓半透明绿叠回原图）逐张核对。
- 三头犬是白石头，在浅色船身上会糊掉，所以 CSS 里单独给了它一圈暗描边
  （`filter: drop-shadow(0 0 3px rgba(4,6,12,.92)) ...`）把它托出来。

---

## 五、arc2 卡片边框与四角铁饰（维基共享资源，实拍照片）

恐怖三桅帆船这一篇的卡片边框是石墙、四角挂的是墓园铁艺 —— 同样是实拍照片做的，
做成九宫格切片后给 CSS 的 `border-image` 用。

| 站里用的文件 | 原始文件 | 作者 | 许可 |
|---|---|---|---|
| `assets/props/border-arc2-narrow.png`<br>`assets/props/border-arc2-wide.png` | [Mossy stone wall diff 16k (Amal Kumar via Poly Haven).png](https://commons.wikimedia.org/wiki/File:Mossy_stone_wall_diff_16k_%28Amal_Kumar_via_Poly_Haven%29.png) | Amal Kumar（经 Poly Haven） | CC0 1.0 |
| `assets/props/corner-{tl,tr,bl,br}.png` | [Wrought iron gate in cemetery Großostheim (1).jpg](https://commons.wikimedia.org/wiki/File:Wrought_iron_gate_in_cemetery_Gro%C3%9Fostheim_%281%29.jpg) | FF-11 | CC0 1.0 |

- 石材用的是 Poly Haven 那套石墙扫描贴图的**漫反射图层**（diffuse/albedo），不是照片预览图——
  `tex-stone/03.png` 就是它。切成 **96×96、slice 32** 的九宫格：四角各 32px 不拉伸，
  上下左右各 32px 沿一个方向拉，中间留空给正文。
  原图偏黄绿，直接压暗会变成"旧木头"不是"黑暗的石头"，所以调色时**往冷灰拉了一把**
  （`lum*0.58 + 原色*0.42`，再乘 `[0.86,0.90,1.0]`），`tone` 取 0.40（窄版）/ 0.30（宽版）。
  四角还随机抠了 26 处缺角，免得看着像瓷砖。
- 四角铁饰是从一张**墓园锻铁大门**照片上裁的一段卷草花饰。选这张是因为铁是暗的、背后墙面是亮的，
  **亮度阈值就是干净的剪影**，不用手工描轮廓。四角各存一份：
  CSS 没法对 `background-image` 单独做镜像，所以是**在 Python 里先把 tl/tr/bl/br 四个方向翻好存成文件**。
- 成品预览与核对图在 `_audit/props-preview/`（`border-preview.jpg` / `border-check.jpg`）。

**改边框厚度只改两个变量**：`#arc2` 里 `--op-frame`（大卡 11px / 小卡 7px）。
两版素材都留着（窄版 9922B / 宽版 9086B），想换风格只改 `border-image` 那句的 URL。

> ⚠️ `border-image` 一上，`border-left` 会被整圈石纹盖掉 —— 所以名场面卡片那条朱红竖条
> 是改走 `box-shadow` 的 `inset` 画的，不是 `border-left`。
> 另外别忘了配 `background-clip:padding-box`，否则旧纸纹理会被拖进边框区，石框上浮出一层纸色。

---

## 六、arc3 顶上战争（进行中 · 大部分还是占位）

这一篇是在 arc2 的模板上铺的第二篇满屏页。**目前只有"骨架 + 占位素材"是真的**，
真正的照片、实物抠图、边框、音效都还没到，下面逐项标清楚哪个是真、哪个是等。

### 6.1 已定稿的（自己画的，无版权问题）

| 站里用的文件 | 来源 |
|---|---|
| `assets/props/arc3-fleet-near.svg`<br>`assets/props/arc3-fleet-far.svg` | **自己生成的**（`_audit/make-fleet-svg.py`），远/近两层小船影，贴在海平线上缓移 |

- 两张都是 1280×64 的平铺贴图，纵横比 20:1。CSS 那边带子也用 `aspect-ratio:1280/64` 对齐，
  再套"元素两格宽 + 位移 50%"的老写法写字幕滚动 —— 这样任何窗口宽度下循环点都接得上。
- 船的大小是相对贴图定的：近层 42×0.18~0.26 ≈ 8~11 单位，远层 0.10~0.15。
  换算下来近层船高 ≈ 13px，是"海平线上一条小船"该有的尺寸，不会抢前面那张照片。
- 想调密/调大：改脚本末尾 `build(...)` 里的 `count`（条数）、`smin/smax`（大小）、`gap`（最小间距），
  改完重跑 `python _audit/make-fleet-svg.py` 即可，CSS 不用动。

### 6.2 已换真素材的（2026-10-10 第六轮补齐）

| 站里用的文件 | 现在是什么 |
|---|---|
| `assets/arc3-hero.jpg` | **用户自己提供的顶上战争截图**（1920×1080）。旧的低清副本已备份为 `assets/arc3-hero.old.jpg`（保留不引用）。裁切/放大/调色见 `_audit/make-heroes.py` |
| `assets/audio/arc3-sword.wav` | **真实录音**：`File:Metal Clanging Noises.ogg`（CC BY-SA 4.0，Camshaft64）→ 剪成 13.5s 无缝循环 |
| `assets/audio/arc3-crowd.wav` | **真实录音**：`File:360703 eguobyte large-crowd-medium-distance-stereo.wav`（CC0，eguobyte）→ 取中段剪成 16.6s 无缝循环，当"远处战场人潮"的垫底 |

> 仍不引用的旧文件：`assets/props/obj-arc3-*.png`、`assets/props/border-arc3-*.png`、
> `assets/props/corner-arc3-*.png` —— 互动物件与旧边框整批弃用，文件留着没删。

### 6.3 换底图时必须跟着改的一个数（**本轮起已不触发**）

`.op-arc3-fleet` 的 `top:68%` —— 那是**在海平线上**，量的是当前这张底图。
**换照片后必须重新量**（把截图逐行求亮度均值，找天空/海面那道跳变最大的行），否则千帆就飘在半空。

> ⚠️ 2026-10-10 起这条规矩**暂时不触发**：用户提供的这张底图下三分之一本来就是一支整编帆船舰队，
> 再叠一层"自己画的小船影"就是同一件事画两遍，所以 `op-arc3-fleet` 那三行 CSS 已撤，
> 贴图与生成脚本都留着 —— 换成没有船的海面时把 CSS 捞回来即可，脚本不用改。

> 顺带记一条踩过的坑：`.op-arc-bg` 的点亮规则**必须带篇章后缀**
> （`#op-p3:checked ~ .op-arc-bg--arc3`）。写成不带后缀的 `~ .op-arc-bg`，
> arc2 和 arc3 的底图会同时点亮、DOM 靠后的压在上面，**arc2 的页面显示成 arc3 的图**。
> `_audit/check.py` 的 [13] 和 `_audit/render-check.js` 的"层隔离"两处都盯着这件事。

---

## 七、卡片材质重做（2026-10-10，走 VPN 从 Wikimedia Commons 抓的实拍）

用户两条原话定方向：「海军我要的是那种混凝土加铁栅栏的文本设计」、
「恐怖三角帆……根本不是墓碑的样子……自己去 github 上或者谷歌上找开源或者墓碑的设计」。
所以两页卡片彻底分家，素材全部是实拍照片，由 `_audit/make-cards-tex.py` 裁切调色生成。
原始下载图与来源页存在 `_audit/tex/`（每张带一个 `.src.txt`）。

| 站里用的文件 | 用在哪 | 原始文件（Wikimedia Commons） | 处理 |
|---|---|---|---|
| `assets/props/card-arc2-stone.jpg` | arc2 全部卡片面 | Weathered sandstone gravestone (Cedar Hill Cemetery, Newark, Ohio, USA) 3.jpg（geograph 系墓园石碑实拍，苔藓风化砂岩） | 裁平整碑面 → 2× LANCZOS → 锐化 → 压暖压暗 |
| `assets/props/card-arc3-concrete.jpg` | arc3 全部卡片面 | Grey speckled moderately cracked grubby grungy seamless concrete building wall texture.jpg（无缝混凝土） | 中心裁 1024² → 冷化（R0.93/G0.965/B1.045）→ 微暗 0.92 |
| `assets/props/card-arc3-bars.jpg` | arc3 卡片头顶的铁栅横窗 | Old arched prison window with iron bars on grunge concrete wall, Indonesia.jpg（监狱拱窗铁栅实拍） | 裁左半扇矮条 → 列亮度投影找竖杆周期 → 按整数周期裁（可 repeat-x 无缝）→ 压暗加铁锈 |

arc2 的「墓碑感」三件套：碑肩抹圆（border-radius 118px 圆角，不是整卡大拱——宽卡整拱会吃掉左上角的字）、
碑面刻线（::before 双线槽 + 内沿高光）、凿字标题（暗字 + 下沿石面高光 text-shadow）。
arc3 的「要塞感」三件套：混凝土面、卡顶铁栅横窗（::before 贴顶 repeat-x，四种卡四档高度）、
2px 钢板边框 + 四角铆钉（::after 四颗 radial-gradient 圆点，替掉了有亮斑毛病的 corner-arc3-\*.png）。

> 仍占位的：arc3 两条音效（静音 wav）等真实录音；`obj-arc3-*.png`、`border-arc*-*.png`、
> `corner-*.png` 这批旧物件/旧边框图已不再被引用，文件留着没删。

---

## 八、首页藏宝图（2026-10-10 第五轮：一体翻页 + 真图换假图）

用户两条原话定方向：「翻开之后六个地点就在翻开的那张藏宝图上，翻的边和最终的图一定是一体的」、
「原版首页背景藏宝图太假了，根本没有真实藏宝图那种破烂的质感，而且太小太挤」。
旧 `map.jpg`（1536×880，来源不明、本节之前一直没记账）整图换掉。

| 站里用的文件 | 原始文件（Wikimedia Commons，公有领域） | 处理（`_audit/make-map.py`） |
|---|---|---|
| `assets/map.jpg`（2560×1500 横版） | [1650 Portolan chart of the Mediterranean Sea by François Ollive](https://commons.wikimedia.org/wiki/File:1650_Portolan_chart_of_the_Mediterranean_Sea_by_Fran%C3%A7ois_Ollive.jpg)（真羊皮纸海图：罗盘玫瑰/恒向线/海怪/自带污损） | 裁掉最左大黑斑 → 暖化 → **折痕烘焙**（中缝暗线+亮沿，另两竖一横）→ 暗角 + 颗粒 |
| `assets/map-port.jpg`（1400×2000 竖版） | 同上，竖窗裁切（`@media (max-aspect-ratio:4/5)` 换上） | 同上 |
| `assets/map-back.jpg`（2000×2000 纸背） | 同一张图右下角空旷海域裁一块 → 强模糊去线条 | 背面与正面同纸同色（本来就是同一张皮） |

「一体」的实现：底座与折页引用同一张 map.jpg，`background-size:200% 100%` 各取一半，
折页绕中缝 rotateY(0→-180°) 掀开，两次镜像后中缝像素天然对齐。
结构/时序细节与踩坑（filter 压平 3D、drift 必须挂共同壳 .op-map-book）都写在 index.html 注释里，
回归断言在 `_audit/check.py` [15] 与 `_audit/render-check.js`「翻页闭态/落定」两条。
候选图与来源页存 `_audit/tex/map-*.jpg(.src.txt)`，抓取脚本 `_audit/hunt-map.py`。

---

## 九、章节满屏底图与主题卡片纹理（2026-10-10 第六轮）

### 9.1 五张满屏底图（`assets/arcN-hero.jpg`）

| 站里用的文件 | 来源 | 处理（`_audit/make-heroes.py`） |
|---|---|---|
| `assets/arc1-hero.jpg`（1920×1080） | **用户提供的空岛截图**（1750×899） | 裁真 16:9 → LANCZOS 放大 → 提亮压对比 → 固定种子颗粒 |
| `assets/arc3-hero.jpg`（1920×1080） | **用户提供的顶上战争截图**（1672×941，替换旧低清版） | 同上；新图清晰度约为旧图 10 倍（Laplacian 方差 2313 vs 230），颗粒从轻 |
| `assets/arc4-hero.jpg`（1920×1080） | **用户提供的鱼人岛截图**（1629×966） | 同上 |
| `assets/arc5-hero.jpg`（1920×1080） | **用户提供的德雷斯罗萨截图**（巨脸俯瞰玩具城，1744×901） | 同上 |
| `assets/arc6-hero.jpg`（1600×900） | **用户提供的蛋糕岛截图**（1080×550） | 源图最小、只放大约 1.6 倍，改走"加重颗粒把糊读成旧海报"的路子 |

> 这五张是**用户自己提供的动画截图**，版权在原作方；本站是个人非公开的学习/展示项目，
> 底图仅作背景氛围使用。若要公开传播，请自行替换为有权使用的素材。

### 9.2 四张主题卡片纹理（`assets/props/card-arcN-*.jpg`，Wikimedia Commons 实拍）

> **⚠️ 第六轮的实拍纹理方案已在第七轮作废**（用户口径：海贼王是动漫，卡片不能用真实世界照片，
> 也不能只做"方框垫图"；要整个卡片变成主题物件的剪影外形 + 卡通纹路填充）。
> 四张 jpg 已停引用、移到 `_audit/deprecated/` 留档。替代方案见 9.3。

### 9.3 四篇卡通剪影卡片（2026-10-10 第七轮，现行方案）

每篇出**两个自绘 SVG**（生成脚本 `_audit/make-card-shapes.py`，viewBox 1000×600、
`preserveAspectRatio="none"` 由 CSS 拉伸适配卡片尺寸）：

| 篇 | 文件 | 剪影外形 | 纹路填充 |
|---|---|---|---|
| arc1 空岛 | `props/mask-arc1-cloud.svg` + `props/skin-arc1-cloud.svg` | 蓬软云朵 | 波浪云纹线 + 云朵圆点 |
| arc4 鱼人岛 | `props/mask-arc4-coral.svg` + `props/skin-arc4-coral.svg` | 珊瑚礁峰 | 珊瑚枝杈 + 气泡 |
| arc5 德雷斯罗萨 | `props/mask-arc5-toy.svg` + `props/skin-arc5-toy.svg` | 积木块（顶部三凸点） | 积木拼色块 |
| arc6 蛋糕岛 | `props/mask-arc6-cookie.svg` + `props/skin-arc6-cookie.svg` | 方饼干（扇贝边 + 右上咬痕） | 巧克力豆圆点 |

- **全部代码绘制**（矢量 SVG），零照片、零 AI 生成图、零版权负担，file:// 直开。
- CSS 挂载：`mask-image` 裁剪影外形，`background` 铺 skin SVG（底色 + pattern 纹路 + 粗描边），
  `filter: drop-shadow` 补回被 mask 裁掉的投影。
- **安全区**：剪影上缘只在中央上凸、中带全宽（画布 x 2%~98%），配合大 padding
  （block 顶 90px／char 顶 60px／li 顶 56px），保证任何卡高下**没有一行字被裁**——
  这也是用户第三点「要呼吸感」的落点；六篇的卡内 padding 全部按此复查过。

---

## 十、六篇氛围音（2026-10-10 第六轮）

用户点名四篇的氛围音：「空岛是很安静的，风声。德雷斯罗萨就人群的嘈杂声音。
人鱼岛要水里气泡那种咕噜咕噜的声音。蛋糕岛就要那种烹饪和制作甜品的声音」；
并要求 arc3 那两条占位静音本轮一起配真录音。全部来自 Wikimedia Commons，
抓取脚本 `_audit/dl-audio6.py`（点名清单，慢速重试绕开 429），
裁剪脚本 `_audit/_audio_build.js`（headless Chrome 的 Web Audio 解码 → 取窗口 → 末尾等功率交叉淡化 → 归一 → 输出 WAV）。

| 站里用的文件 | 用在哪 | 原始文件（Wikimedia Commons） | 许可 / 作者 | 剪法 |
|---|---|---|---|---|
| `assets/audio/arc1-wind.wav`（18.8s） | arc1 空岛·安静的风声 | *Gentle breeze and birds singing.ogg* | Public domain / ezwa | 取 4–24s，1.2s 交叉淡化 |
| `assets/audio/arc3-sword.wav`（13.5s） | arc3 顶战·刀剑碰撞 | *Metal Clanging Noises.ogg* | CC BY-SA 4.0 / Camshaft64 | 整条 0.8s 交叉淡化 |
| `assets/audio/arc3-crowd.wav`（16.6s） | arc3 顶战·众人怒吼（远处战场人潮） | *360703 eguobyte large-crowd-medium-distance-stereo.wav* | CC0 / eguobyte | 取 15–33s，1.4s 交叉淡化 |
| `assets/audio/arc4-water.wav`（16.8s） | arc4 鱼人岛·水下气泡咕噜 | *Water bubbles chortling.ogg* | Public domain / stephan | 取 8–26s，1.2s 交叉淡化 |
| `assets/audio/arc5-crowd.wav`（18.6s） | arc5 德岛·人群嘈杂 | *1 minute at the alexa mall in berlin.ogg* | Public domain / thore | 取 12–32s，1.4s 交叉淡化 |
| `assets/audio/arc6-cook.wav`（18.6s） | arc6 蛋糕岛·烹饪/做甜品 | *Kitchen sounds recorded while cooking.ogg* | CC BY-SA 4.0 / User:Akum20 | 取 30–50s，1.4s 交叉淡化 |

- 六条统一归一到目标 RMS = 0.06（绝对响度一致），相对大小交给页面脚本里的 `CFG.volume` 调。
- 每篇再叠一层浏览器现场合成的氛围声（风/火/人潮/水下/厨房/金属），
  为的是"某个浏览器解不开格式时还有声"以及"真录音单薄时补底"。合成层与真录音各走各的，
  绝不用 `createMediaElementSource`（file:// 下会被判跨源污染，整条 Web Audio 链变哑）。
- 原文件存在 `_audit/audio6/<组>/`，元数据汇总在 `_audit/audio6/_picked.json`。

---

## 十一、角色头像（2026-10-10 第七轮：19/19 已入库）

六篇共 **19 个角色**要配真实头像。用户原话「你可以去百度搜索这个人物，然后 copy 它的头像放进去」，
但实测百度两条路全堵（`baike.baidu.com` 直连/代理都 403；`image.baidu.com/search/acjson` 返回
`{"antiFlag":1,"message":"Forbid spider access"}`），随后用户改口径为「你要什么头像给我列个清单，我去找」。

**第七轮已全部落位**：用户按清单顺序投了 19 张图进 `assets/avatars/incoming/`，
但微信导出的文件名全是无意义编号（`微信图片_…_433_275.png` … `_451`），按名认领一条都认不上。
由助手逐张识图建立显式映射表 `_audit/avatar-map.json`（抽查 7 张全对，顺序＝清单顺序），
`make-avatars.py` 改为**映射表优先、按名认领兜底**，19/19 入库。

- **成品**：`assets/avatars/<slug>.jpg` ×19（288×288，`ImageOps.fit` 人脸偏上 centering=(0.5,0.38)）。
- **页面**：`index.html` 的 `/* op-avatars:begin */ … :end */` 段已生成 19 条规则
  （`background:url(...) center/cover` + 篇章主题色描边）；头像圈由 60px 放大到 **76px**。
- **换图须知**：脚本"已在库不覆盖"——想换某个头像先删旧的 `assets/avatars/<slug>.jpg` 再重跑。
- 真实性：头像版权在版权方手里；用户投图属于个人使用，脚本只做本地裁切。
- 兜底不变：头像走 CSS `background-image`（非 `<img>`），规则只给"确实有图"的角色生成。

---

## 十二、章节档案卡边框（2026-10-11 第八轮：用户提供素材）

四篇的正文卡片（空岛 / 鱼人岛 / 德雷斯罗萨 / 蛋糕岛）不再用自绘剪影，
改用**用户本人提供的四格素材**当卡片边框（用户原话：「我已经有 4 个章节专属 UI 素材……
把这四个素材作为章节信息卡片的边框」）。

- **来源**：用户提供的单张 2×2 拼图（1536×1024，黑底分隔），
  原始路径 `C:/Users/18026/.workbuddy/clipboard-images/clipboard-2026-10-10T15-53-35-989Z-cb2d6e6f.jpg`。
  **用户提供，非本站生成、非 AI 二次生成**；本轮只做裁切与排版，不再重绘。
- **裁切**：`_audit/make-card-borders.py`（亮度扫缝 → 按缝切四格 → 每边内缩 6px 吃掉黑边）。
- **成品**：
  | 文件 | 篇章 | 裁框 | 尺寸 | 比例 |
  |---|---|---|---|---|
  | `assets/props/card-arc1-cloud.jpg` | 空岛 | (12,12,762,501) | 750×489 | 1.534 |
  | `assets/props/card-arc4-coral.jpg` | 鱼人岛 | (774,14,1524,500) | 750×486 | 1.543 |
  | `assets/props/card-arc5-toy.jpg` | 德岛 | (12,513,762,989) | 750×476 | 1.576 |
  | `assets/props/card-arc6-cookie.jpg` | 蛋糕岛 | (774,516,1524,984) | 750×468 | 1.603 |
  另各出一张 `card-arcN-*-tile.jpg`（取各格中心 256、镜像拼成 512 可平铺贴图），
  给窄屏解构模式与「名场面」板块当同源纹理。
- **用法**：整格素材当卡片背景，卡锁成素材比例（`aspect-ratio`）→ `background-size:100% 100%` 等比、零拉伸
  （**第十二轮起改成 `104% 110%`**，见下面十四）；
  内容用绝对定位安全区（`.op-dossier-inner` 的 `inset`）。**不用 `border-image` 九宫格** ——
  素材的装饰物在边的中段（浮岛/帆船/骷髅旗/甜甜圈），九宫格一拉就糊。

### 十二·补（第九轮）：外轮廓也是从素材里抠的

用户否掉了"矩形 + 圆角"（原话：「不是简单的正方形加圆角，而是要不规则的边框，
可以根据图片的边缘形状进行切割……不要随便用代码搞一点看似不规则其实很规则的图案」）。
于是卡片外形改成从素材里提**真实轮廓**当 `clip-path`：

- **脚本**：`_audit/make-card-clips.py`（numpy + Pillow，零新装依赖，不引 cv2/scipy/potrace）。
  灰度 → 阈值 **50**（定死；探明 40~80 都安全，≥100 会挖穿 arc6 巧克力块 / arc5 骷髅旗）→
  四边泛洪标"外部黑" → 取反 → 最大连通域 → **去小斑点 + 填小针孔 + 向内腐蚀 3px** →
  Moore 邻域追踪 → **环绕滑动平均** → Douglas–Peucker（主卡 ε=1.2px）。

  ⚠️ **第十轮把原来那步 3×3 闭运算拿掉了**（对应的"为什么要改"见下面十三）：
  闭运算会把轮廓量化成 3px 的台阶，渲染出来就是一圈锯齿 ——
  用户那句「这些边边角角太丑了，圆滑一点啊」元凶就在这儿。
  换成"去斑点 + 填针孔 + 只做向内腐蚀"之后尖角（>70°）从 29/191 降到 0~8/175。
  **向内腐蚀那 3px 也不能省**：素材最外一圈像素是跟黑底混在一起的（抗锯齿 + JPEG），
  不腐蚀进去就会带着一圈黑边，也就是用户说的「这里有黑边，抠一下」。
  滑动平均会让凸处内缩约 0.5px（IoU 掉到 0.994），所以补了一个沿法线外推 0.6px 的
  `offset_outward` 拉回来 —— 取面积变大的那个方向才对。
- **产物**：8 个 `clipPath`（`op-clip-arcN` 主卡高保真 + `op-clip-band-arcN` 横带），
  由 `_audit/_inject_clips.py` 内联进 `index.html` 的 `<main>` 末尾。
  **必须 inline**：外部 `.svg` 引用在 HTML 元素上 Chrome 已废弃。**用 `clip-path` 不用 `mask`**：
  Safari 下 mask 不参与命中测试，会"看不见却点得到"。
- **横带**（人物框 / 名场面 / 底部提示共用）：从同一条真实轮廓上取 `y<0.35H` 的上缘 +
  `y>0.65H` 的下缘（两端也是真实边缘点），所以整页"所有文本框一致"且同源。
- **核对**：`_audit/tex6/verify-arcN.png`（轮廓红线叠回原图 + 填色叠影），
  实测 IoU 0.9975~0.9994（阈值 ≥0.995）；`silhouette-sheet.png` 是四个剪影与横带的汇总。
- **背景**：`background-size` 从 106% 回 100%（比例已锁，等比零拉伸形状才对得上）；
  **第十二轮起又加回放大：`104% 110%`**，见下面十四。理由跟第九轮"回 100%"不冲突 ——
  第九轮是怕拉伸后形状对不上轮廓，而 `104%/110%` 是**等比**放大（把最外圈那张矩形底板推出轮廓），
  轮廓本身不动；
  `border-radius` 与 `box-shadow` 都删了 —— filter 在 clip-path 之前生效，投影会被一起裁掉。
- **旧素材处置**：`assets/props/mask-arc*.svg`、`skin-arc*.svg` 已删；
  生成脚本 `make-card-shapes.py` 移入 `_audit/deprecated/`。`_audit/tex5/borders-sheet.png` 是裁框对照图。

### 十三（第十轮）：小文本框与返回钮的底色改成"本篇素材自己裁一块"

用户原话：「背景换成天空，可以模仿上面主卡片的背景」「这里用玩具的背景，不能自己生成，
要用上面那个主卡片的背景自己裁剪，**但是也不可以对主卡片的比例进行压缩**」
「返回藏宝图……背景改成深海颜色，不要白色和这个米黄色」。

**四张素材还是那四张，没有新增任何图片文件。** 变的只是怎么用：

- **大文本框**（人物框 / 名场面 / 底部提示）：background-image 直接用本篇主卡素材，
  配 `background-size:cover`（等比铺满再裁，比例零压缩；算出来是 1.49x，
  跟主卡 `100% 100%` 同一个倍率，所以看着是同一张材质的延续）。
  原来那层"白的 .86 + 米黄 tile"整批拆掉；名场面每条 `li` 自带的
  `background:var(--op-surface)`（`#f4e6c4`，正是用户点名不要的那块米黄）改成 12% 近乎全透；
  三处都补了 `background-color:transparent`，免得哪天某个图层没铺满它从缝里露出来。
- **返回藏宝图**：四篇逐篇换成本篇素材。**这里不能用 cover** —— 钮只有 58px，
  cover 会把整张素材压到 58px（12.9 倍缩小），而且 cover 取到整图高度的 100%，
  上下两条边正好落在轮廓之外（那里是纯黑，实测鱼人岛黑占比 2.38%）。
  改成给 px 宽度 + auto 高度**放大**取一块，且那一块必须整个落在轮廓内。
- **暗处兜底**：空岛 / 德岛 / 蛋糕岛用 `background-blend-mode:lighten` 的亮度地板
  （`#99a1a8` / `#a8a59d` / `#a8a2a3`），逐通道取 `max(地板色, 素材)` ——
  比地板亮的地方一个像素都不动；鱼人岛反过来用半透明罩 `rgba(226,246,252,.68)` /
  `rgba(200,236,248,.52)`（它那条带子本来白占比就只有 1%，用 lighten 反而会把仅剩的暗部层次切平）。

数值不是拍脑袋的，是脚本搜出来的「最低够用值」——再低正文对比度就掉到 WCAG AA 线（4.5）以下了：

| 位置 | 轮廓内 | lum | gstd | 黑% | 白% | 最暗处对比度 |
|---|---|---|---|---|---|---|
| 空岛 人物框 / 名场面 / 底部提示 | —（有遮罩） | 221 / 228 / 221 | 25.4 / 20.0 / 25.7 | 0 | 46 / 51 / 46 | 5.04 / 5.03 / 5.00 |
| 鱼人岛 同上 | —（有遮罩） | 219 / 221 / 219 | 13.8 / 13.4 / 13.6 | 0 | 1.9 / 4.7 / 1.6 | 5.15 / 4.94 / 5.50 |
| 德岛 同上 | —（有遮罩） | 211 / 216 / 211 | 25.4 / 23.1 / 25.4 | 0 | 12 / 25 / 11 | 5.29 / 5.50 / 5.35 |
| 蛋糕岛 同上 | —（有遮罩） | 214 / 219 / 214 | 23.0 / 19.5 / 22.9 | 0 | 3.4 / 12.6 / 3.0 | 5.67 / 6.17 / 5.68 |
| 返回钮 / 胶囊 | 是（四篇都落在内） | 197 / 100 / 192 / 210 | 22.8 / 23.8 / 23.3 / 24.0 | ≤1.0 | — | — |

（`—（有遮罩）`是指大文本框本身带 clip-path，"取样落不落进轮廓"这个问题不成立 ——
外面那圈早被裁掉了，真正要看的是遮罩之后还剩多少黑，也就是上面那一栏。）

产出脚本：`_probe_slice.js`（读 computedStyle）+ `_slice_verify.py`（反推渲染再体检，判据是
黑占比 / gstd / 按一行文字大小开窗的 WCAG 对比度）+ `_pick_floor.py` / `_tune_pill.py` / `_tune_arc4.py`（搜参数）。

### 十四（第十一轮）：音源没变，变的是**每条放多大声**

**没有新增、没有替换、没有重新剪辑任何音频文件** —— 八条还是第八轮/第六轮那八条
（来源与许可见本文第三、十节）。这一轮只动了 `index.html` 里那张音量表。

背景：用户说「就是太轻，提音量就行」。`_rms_probe.js` 量出来八条的原始 RMS 齐刷刷在
−24 ~ −27 dBFS，乘上原来那串 0.26~0.46 之后落到耳朵上只剩 −30 ~ −36 dBFS。

现在的音量是**按目标电平反算**的（`≈0.053` / 叠加处每层摊 `1/√2` / 再用峰值卡 0.92）：

| `<audio>` id | 文件 | 原音量 | 现音量 | 现「RMS×音量」 |
|---|---|---|---|---|
| `op-a1-wind` | arc1-wind.wav | 0.30 | **0.88** | 0.0528 |
| `op-a2-wind` | arc2-wind.ogg | 0.34 | **0.56** | 0.0297（被峰值 1.65 压住） |
| `op-a2-fire` | arc2-fire-clean.wav | 0.46 | **0.85** | 0.0377 |
| `op-a3-sword` | arc3-sword.wav | 0.42 | **0.63** | 0.0378 |
| `op-a3-crowd` | arc3-crowd.wav | 0.26 | **0.63** | 0.0378 |
| `op-a4-water` | arc4-water.wav | 0.34 | **0.88** | 0.0528 |
| `op-a5-crowd` | arc5-crowd.wav | 0.30 | **0.88** | 0.0528 |
| `op-a6-cook` | arc6-cook.wav | 0.32 | **0.95** | 0.0434 |

合成层总增益 `SYNTH` 0.085 → **0.12**（真录音提了 ~9dB，它不跟一点就听不见了）。

> ⚠️ **`arc2-wind.ogg` 那条峰值是 1.38~1.65**（解码后有 14 个采样点超过满刻度，
> 全挤在第 64.45 秒那一下）。按电平它该给 0.71，但那样每次循环到那一处都会削波，
> 所以压到 0.56 —— 这是**唯一一条没按电平给足**的，别再"顺手把它调上去"。

量法：`_rms_probe.js`（借 Chrome 的 `decodeAudioData` 量八条的解码电平）+
`_audio_level.js`（在总线 → destination 之间插 AnalyserNode 量输出）。渐入的实测数据在
`说明.md` 第十节。

### 十五（第十二轮）：素材文件一个没改，改的是**铺法**

**没有新增、没有替换、没有重新裁切任何图片**。四张 `card-arcN-*.jpg`、四张 `-tile.jpg`、
8 个 `clipPath` 全部原样。这一轮只改了 `index.html` 里四行 `background-size`。

背景：用户说「边角组里面有黑边黑角」，追问后指**空岛篇**、「小角落有一些地方很黑」。

查出来四张素材是同一套做法 —— 一个框画在**矩形底板**上（空岛底板是深海蓝黑，
玩具的是黑棕）。第九轮抠的轮廓是贴着**框的外沿**走的，比底板的内沿还靠外一点，
底板就顺着轮廓留了一圈黑边。30×18 占用率图：空岛**右上角那一格 93% 是暗的**、左边一条 47%/32%。

**改法**：`background-size:100% 100%` → **`104% 110%`**（四篇统一，等比放大）。
素材被放大之后最外圈那层底板整个落到轮廓外，轮廓形状 / 盒子尺寸 / 卡内文字位置全不动。

- 横向 4% / 纵向 10% —— 素材按**短边**算边距，上下那道底板比左右厚一倍。四篇同一组值。
- 窄屏那条媒体查询里素材是 `100% auto`（一整张照片铺顶部，底板从左右露出），
  改成 **`106% auto`**。上限是 `.op-dossier-inner` 的 `padding-top:66vw` 卡的：
  素材高度 ≈ 卡宽 × 1.06 × (489/750) ≈ 0.691 × 卡宽，820px 宽时两者差 4px（落在内边距里）。
- 试过「四边铺天空色 `linear-gradient` + `lighten` 当边圈地板」，数值很好但渲染出来是
  一块发白的平补丁，比黑边还假，否掉。

实测（轮廓内 <130 的暗像素）：空岛 1.537% → **1.063%**，鱼人岛 0.631% → 0.496%，
德岛 5.971% → 5.447%，蛋糕岛 2.467% → 2.149%；空岛轮廓内最外 24px 那圈的
第 5 百分位亮度 **112 → 221**，同时四篇的"画面深处"一点没被刷白。
量法：`_audit/_edge_profile.py`（由外向内逐环剖面）、`_audit/_darkmap.py`（轮廓内暗像素占用率图）、
`_audit/_sim_zoom.py`（按轮廓离线模拟各倍率）、`_audit/_fix_verify.py`（改前改后对照）。

### 十六（第十三轮）：三篇氛围特效的素材全是本地算出来的

**还是一张外面找的图都没有。** 这一轮的背景是网络不通
（直连 wikimedia 12 秒超时返 000，代理 `127.0.0.1:7897` 端口没有监听），
所以三样素材全部现算：

| 文件 / 载体 | 是什么 | 生成方式 | 脚本 |
|---|---|---|---|
| `props/fx-cloud-a.webp` | 积云（横向漂移用）2200×1300 / 98KB | PIL + numpy：分形值噪声 + 软椭圆云团，噪声啃边 | `_audit/_make_fog.py` |
| `props/fx-cloud-b.webp` | 横向拉长的云带（上浮用）2200×1300 / 90KB | 同上，`stretch_x=3.4` | 同上 |
| `props/fx-cloud-c.webp` | 小团碎云 2200×1300 / 101KB | 同上（**这一轮没用上**，留着备用） | 同上 |
| `props/fx-haze.webp` | 整屏薄雾 1800×1100 / 159KB | 纯噪声低通 | 同上 |
| 内联 SVG ×2 | 气泡贴图（大 420px / 小 237px） | 抖动网格铺圆 + 左上高光点，`quote()` 成 data URI | `_audit/_make_bubble.py` |
| 内联 SVG ×3 | 蝙蝠剪影（上挥 / 平展 / 下挥） | 手写路径，中线镜像；暗填充 + 一圈冷紫描边 | `_audit/_make_bat.py` |

**没有版权的第三方素材，因此这一节不需要署名。**
写进这里是为了留个底：这四张 WebP 是自己算的，不是从哪张照片裁的；
以后要重做，跑一遍 `_audit/_make_fog.py` 就有（随机种子固定，结果可复现）。

顺带一条**用图规矩**：云雾贴片必须**四边羽化到全透明**（`edge_fade()`，横 14% 纵 12%），
因为 CSS 那边用的是"两张同图首尾相接、一起推一整张"的无缝循环 ——
接缝两边都是空的，才看不到一条硬边。换贴片时这条不能丢。

⚠️ 另外记一个坑：气泡那两张 SVG 是**内联 data URI**，
生成脚本写出来的字符串**自带 `data:image/svg+xml,` 前缀**。
第一版把它整条塞回 `url("data:image/svg+xml,__X__")` 的模板里，前缀就写了两遍，
浏览器拿到 `data:image/svg+xml,data:image/svg+xml,%3Csvg…` —— **图直接不渲染**，
外面完全看不出来（`backgroundImage` 的长度是 4080，看着正常）。
现在 `_make_bubble.py` 写两份：`_bubble_css.txt` 给人看（带前缀）、
`_uri_<k>.txt` 只留编码载荷给模板用。详见 `说明.md` 第十一节。


---

## 十三、七套幕布转场皮肤（2026-10-12 第十九轮：全部自绘，无第三方素材）

七套"幕布"转场皮肤（藏宝图纸 / 云层 / 黑幕 / 海浪 / 泡泡 / 玩具 / 甜品）**没有一个字节来自外部**：

- 云层、海浪、泡泡、玩具、甜品五套是**脚本生成的平铺 SVG**，以 `data:image/svg+xml,` 内联在 CSS 里
  （生成脚本 `_audit/_make_tt_skins.py`，随机种子固定 `20261012`，结果可复现）；
- 藏宝图纸、黑幕两套干脆是 **CSS 渐变**（`radial-gradient` / `repeating-linear-gradient`），连 SVG 都没有；
- 罗盘是照着站里 `.op-back` 那颗内联 SVG 复制的，同一套配色（`#c8892f` / `#8a5a1e` / `#ffe4b8`）。

**所以这一节不需要署名。** 写在这里是为了留个底：以后要换皮肤，
改 `_make_tt_skins.py` 重跑 → `_apply_r19d.py <名字>` 刷新 CSS 块即可，不用手工改 `index.html`。

⚠️ 两条**换贴片时不能丢**的规矩：

1. 贴图必须**可平铺**：软的圆/环跨边要按 3×3 环绕复制，硬的小点可以留边（切了看不出来）；
   否则平铺出一张肉眼可见的网格。
2. 数据 URI 里只许出现 `A-Za-z0-9-_.~`：`'` 必须编成 `%27`、`)` 必须编成 `%29`。
   这两个漏编，CSS 的 `url("…")` 会被提前截断，而且**外面完全看不出来**（图直接不渲染）。
   另外 ⚠️ **`url("data:…")` 里带双引号，绝不能塞进 HTML 的 `style="…"` 内联属性** ——
   属性会被提前截断，整层背景失效且不报错。这一轮做皮肤预览页时当场踩过。

---

## 十四、影像位视频封面（2026-10-14 第二十三轮：B站 官方封面 + 用户截图）

六个影像位（`.op-video-frame`）里的封面图，点击后跳对应 bilibili 原视频。
这些是**视频封面 / 截图**，版权归各 UP 主与作品原作，**站内仅作跳转示意、不作商用**；点封面即离开本站去原页。

| 篇 | 文件 | 封面来源 | bilibili |
|---|---|---|---|
| 空岛篇 | `assets/video/arc1.jpg` | bilibili 官方封面 | [BV1664y1v7pd](https://www.bilibili.com/video/BV1664y1v7pd) |
| 恐怖三桅帆船篇 | `assets/video/arc2.jpg` | bilibili 官方封面 | [BV1qo4y1m7rx](https://www.bilibili.com/video/BV1qo4y1m7rx) |
| 顶上战争篇 | `assets/video/arc3.jpg` | bilibili 官方封面 | [BV1e7411i7S9](https://www.bilibili.com/video/BV1e7411i7S9) |
| 鱼人岛篇 | `assets/video/arc4.jpg` | bilibili 官方封面 | [BV1v2DUYYEXr](https://www.bilibili.com/video/BV1v2DUYYEXr) |
| 德雷斯罗萨篇 | `assets/video/arc5.jpg` | **用户提供的截图**（320×200，Lanczos 放大 + 轻锐化） | [BV1Tx411r7ws](https://www.bilibili.com/video/BV1Tx411r7ws) |
| 蛋糕岛篇 | `assets/video/arc6.jpg` | bilibili 官方封面 | [BV1CY4y1e7jw](https://www.bilibili.com/video/BV1CY4y1e7jw) |

arc1/2/3/4/6 的封面经 `api.bilibili.com/x/web-interface/view` 取 `data.pic` 下载后转 jpg（progressive q90）；
arc5 因官方封面实测也是 320×200，按用户拍板直接用其提供的截图放大。原始 PNG 备份在 `_audit/video-covers-src/`。
