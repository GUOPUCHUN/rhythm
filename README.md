## English

# RHYTHM — v1.1

A personal task and state tracking PWA. It can be used offline once installed on the iPhone Home Screen. It is purely static, with no dependencies and no build steps.

## Structure

**Today** — Main Task (Blue) / Fixed Tasks (Orange) / Additional Tasks (Green) / Today's State / Today's Rating

**Review** — Monthly calendar. Three-color dots indicate whether the three types of tasks are completed, and the bottom color bar represents the state level of the day. Tap any date to backfill records. Below are the monthly summary and the progress of each main task.

**Schedule** — Schedule Main Tasks / Fixed Tasks / Additional Tasks / Task Management (Edit, Delete, Archive)

## Three Types of Tasks

| | When it appears | Planned Amount |
|---|---|---|
| Main Task (Blue) | Can be multiple; the Today page only shows the one with the **closest deadline** | Planned amount within the deadline |
| Fixed Task (Orange) | Repeats by **days of the week** | Weekly planned amount |
| Additional Task (Green) | Specifies **exact dates**, does not repeat weekly | Daily planned amount |

Main tasks will not automatically disappear after expiration; they will stay on the Today page prompting to be archived. The next main task will only move up after the current one is archived.

## Recording Rules

- Unit in **hours**: Record duration + start time (end time is calculated automatically)
- Unit in **times/sessions**: Record completed amount + time period (start → end)
- Each task can be recorded once a day; tap again to modify or cancel.
- Today's state can be modified repeatedly on the same day but is locked after crossing midnight; unrecorded past dates can still be backfilled.

## State Scoring

The scores of each option are directly summed: Mood -2 to +2 (single choice), Mental and Physical items -1 / 0 / +1 (multiple choice).

| Total Score | State |
|------|------|
| ≥ 3 | Excellent |
| 1 ~ 2 | Good |
| 0 | Normal |
| -1 ~ -2 | Poor |
| ≤ -3 | Extremely Poor |

"Calm" is mutually exclusive with other items in the mental group, and "Normal" is mutually exclusive with other items in the physical group.

## Today's Rating

Self-rating and Others' rating, from 0 to 10 each. Others' rating can be left blank. Saved immediately upon selection; the monthly average will appear on the Review page.

## Files

```
index.html              All UI and logic
manifest.webmanifest    PWA configuration
sw.js                   Offline caching (increment VERSION by 1 if index.html is modified)
icon-180.png            apple-touch-icon (iOS only recognizes PNG)
icon-192.png / icon-512.png / icon-512-maskable.png
```

## Deployment

**Netlify Drop**: Pack these files (without the outer folder) and drag them to https://app.netlify.com/drop
**GitHub Pages**: Place files in the repository root → Settings → Pages → main / root

Both provide HTTPS — which is required for both the service worker and the "Add to Home Screen" feature.

## Installing on iPhone

Open the URL in Safari → Share → Add to Home Screen.
The localStorage of normal Safari tabs will be cleared by ITP after 7 days of inactivity; installed PWAs have isolated storage space and are not subject to this restriction.

## Data

Data is stored in the local device's `localStorage` under the key `rhythm:v1`. At the bottom of the Review page, you can **copy all data** as a JSON backup and **paste it to restore** when changing devices.
Upgrading from v1 will trigger an automatic migration (the old single main task becomes a list, and the "days of the week" setting for additional tasks is cleared and changed to specific dates).

## Roadmap

- **v1.1** (Current): Multiple main tasks, date-specific additional tasks, daily ratings.
- **v2**: IndexedDB + Cloudflare Worker/D1 sync + Claude API for automatic weekly reviews.
- **v3**: Web Push reminders; iOS Shortcuts for automatically writing sleep/exercise data.

<br>

---

## 日本語 (Japanese)

# RHYTHM — v1.1

個人のタスクと状態を記録するPWA（プログレッシブウェブアプリ）。iPhoneのホーム画面に追加するとオフラインで使用可能です。完全に静的で、依存関係やビルドのプロセスはありません。

## 構成

**今日 (Today)** — メインタスク（青）／固定タスク（オレンジ）／追加タスク（緑）／今日の状態／今日の評価

**振り返り (Review)** — 月間カレンダー。3色のドットは3種類のタスクの完了状況を示し、下部のカラーバーはその日の状態レベルを示します。任意の日付をタップして過去の記録を追加できます。下部には今月のまとめと各メインタスクの進捗が表示されます。

**スケジュール (Schedule)** — メインタスクの予定／固定タスクの予定／追加タスクの予定／タスク管理（編集、削除、アーカイブ）

## 3種類のタスク

| | 表示されるタイミング | 計画量 |
|---|---|---|
| メインタスク（青） | 複数設定可能。今日ページには**期限が最も近い**ものだけを表示 | 期限内の計画量 |
| 固定タスク（オレンジ） | **毎週指定した曜日**に繰り返し | 週間の計画量 |
| 追加タスク（緑） | **指定した具体的な日付**のみ。毎週の繰り返しはなし | 1日あたりの計画量 |

メインタスクは期限切れになっても自動的に消えず、今日ページに残り続けてアーカイブを促します。アーカイブされて初めて次のタスクが繰り上がります。

## 記録のルール

- 単位が**時間**の場合：所要時間 ＋ 開始時刻を記録（終了時刻は自動計算）
- 単位が**回数**の場合：完了量 ＋ 時間帯（開始 → 終了）を記録
- 各タスクは1日1回記録。もう一度タップすると修正やキャンセルが可能。
- 今日の状態は当日の間は何度でも修正できますが、日を跨ぐとロックされます。未記録の過去の日付は後から記録可能です。

## 状態のスコア化

各項目のスコアを単純に合計します：気分 -2～+2（単一選択）、精神と身体の各項目 -1 / 0 / +1（複数選択）。

| 合計スコア | 状態 |
|------|------|
| ≥ 3 | 絶好調 |
| 1 ~ 2 | 良好 |
| 0 | 普通 |
| -1 ~ -2 | 不調 |
| ≤ -3 | 最悪 |

精神グループの「穏やか」は他の項目と同時に選べません。身体グループの「普通」も他の項目と同時に選べません。

## 今日の評価

自己評価と他者評価（各0～10点）。他者評価は空欄のままでも可能です。選択するとすぐに保存され、振り返りページに今月の平均値が表示されます。

## ファイル

```
index.html              すべてのUIとロジック
manifest.webmanifest    PWAの設定
sw.js                   オフラインキャッシュ（index.htmlを変更したらVERSIONを1増やす）
icon-180.png            apple-touch-icon（iOSはPNGのみ認識）
icon-192.png / icon-512.png / icon-512-maskable.png
```

## デプロイ（公開）

**Netlify Drop**: これらのファイル（外側のフォルダを含めず）をZIP化して https://app.netlify.com/drop にドラッグ＆ドロップ。
**GitHub Pages**: ファイルをリポジトリのルートに配置 → Settings → Pages → main / root

どちらもHTTPSを提供します。Service Workerや「ホーム画面に追加」機能にはHTTPSが必須です。

## iPhoneへのインストール

SafariでURLを開く → 共有（シェア）アイコン → 「ホーム画面に追加」。
通常のSafariのタブのlocalStorageは、7日間アクセスがないとITPによって消去されますが、インストールされたPWAには独立したストレージ領域があるため、この制限を受けません。

## データ

デバイスの `localStorage` に `rhythm:v1` というキー名で保存されます。振り返りページの下部から**すべてのデータをJSON形式でコピー**してバックアップでき、機種変更時などに**貼り付けて復元**できます。
v1からアップグレードすると自動でデータが移行されます（旧バージョンの単一メインタスクはリスト化され、追加タスクの「曜日」設定はクリアされて具体的な日付選択に変更されます）。

## ロードマップ (Roadmap)

- **v1.1**（現在）: 複数のメインタスク、日付指定の追加タスク、毎日の評価
- **v2**: IndexedDB + Cloudflare Worker/D1同期 + Claude APIによる自動週間振り返り
- **v3**: Web Push通知、iOSショートカットによる睡眠/運動データの自動書き込み

<br>

---

## 中文 (Chinese)

# RHYTHM — v1.1

个人任务与状态记录 PWA。装到 iPhone 主屏幕后可离线使用，纯静态、无依赖、无构建步骤。

## 结构

**今日** — 主任务（蓝）／固定任务（橙）／附加任务（绿）／今日状态／今日评分

**回顾** — 月历，三色圆点表示三类任务是否完成，底部色条表示当日状态等级。点任一日期可补记。下方是本月总结与各主任务进度。

**日程安排** — 安排主任务／固定任务／附加任务／任务管理（编辑、删除、归档）

## 三类任务

| | 何时出现 | 计划量 |
|---|---|---|
| 主任务（蓝） | 可以有多个；今日页只显示**截止日最近**的一个 | 期限内计划量 |
| 固定任务（橙） | 按**每周几**重复 | 周计划量 |
| 附加任务（绿） | 指定**具体哪几天**，不按周重复 | 每天的计划量 |

主任务过期后不会自动消失，会一直占着今日页并提示归档；归档后下一个才顶上来。

## 记录规则

- 单位为**小时**：记 时长 + 开始时刻（结束时刻自动算出）
- 单位为**次**：记 完成量 + 时间段（开始 → 结束）
- 每个任务每天记录一次；再点一次可修改或取消
- 今日状态当天可反复修改，跨天后锁定；未记录的过去日期仍可补记

## 状态打分

各选项分数直接相加：心情 -2~+2（单选）、心理与身体各项 -1 / 0 / +1（多选）。

| 总分 | 状态 |
|------|------|
| ≥ 3 | 极好 |
| 1 ~ 2 | 好 |
| 0 | 普通 |
| -1 ~ -2 | 差 |
| ≤ -3 | 极差 |

「平静」与心理组其他项互斥，「普通」与身体组其他项互斥。

## 今日评分

自我评分与他人评分，各 0–10。他人评分可留空。选中即保存，本月均值出现在回顾页。

## 文件

```
index.html              全部界面和逻辑
manifest.webmanifest    PWA 配置
sw.js                   离线缓存（改了 index.html 就把 VERSION 加 1）
icon-180.png            apple-touch-icon（iOS 只认 PNG）
icon-192.png / icon-512.png / icon-512-maskable.png
```

## 上线

**Netlify Drop**：把这些文件（不要外层文件夹）打包拖到 https://app.netlify.com/drop
**GitHub Pages**：文件放仓库根目录 → Settings → Pages → main / root

两者都提供 HTTPS —— service worker 和「添加到主屏幕」都需要 HTTPS。

## 装到 iPhone

Safari 打开网址 → 分享 → 添加到主屏幕。
普通 Safari 标签页的 localStorage 会被 ITP 在 7 天不访问后清除；已安装的 PWA 有独立存储空间，不受此限制。

## 数据

存在本机 localStorage，键名 `rhythm:v1`。回顾页底部可**复制全部数据**成 JSON 备份，换机时**粘贴恢复**。
从 v1 升级会自动迁移（旧的单个主任务变成列表，附加任务的「每周几」清空、改为选具体日期）。

## Roadmap

- **v1.1**（当前）：多主任务、按日期的附加任务、每日评分
- **v2**：IndexedDB + Cloudflare Worker/D1 同步 + Claude API 自动周复盘
- **v3**：Web Push 提醒；iOS 快捷指令自动写入睡眠/运动数据
