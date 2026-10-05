# gitignore

离线生成 `.gitignore` 的小工具：技术栈进，合并好的忽略规则出。

纯标准库、纯本地——不用联网查模板，10 个常用模板全部内置。

## 快速开始

```bash
# 直接输出到终端
python -m gitignore python node

# 写入当前目录的 .gitignore
python -m gitignore python node --write

# 追加到已有的 .gitignore
python -m gitignore macos --append

# 覆盖已存在的文件
python -m gitignore python --write --force

# 看看有哪些模板
python -m gitignore --list
```

## 内置模板（10 个）

| 模板名    | 覆盖内容                          |
|-----------|-----------------------------------|
| python    | `__pycache__`、虚拟环境、dist、覆盖率 |
| node      | `node_modules/`、日志、构建产物、缓存 |
| java      | `*.class`、`target/`、Maven/Gradle  |
| go        | 二进制、vendor、`go.work`           |
| rust      | `target/`、`*.rs.bk`                |
| macos     | `.DS_Store`、`.Trashes`             |
| windows   | `Thumbs.db`、`Desktop.ini`          |
| linux     | `*~`、`.Trash-*`、`.nfs*`           |
| vscode    | `.vscode/`（保留常用配置文件）      |
| jetbrains | `.idea/`、`cmake-build-*/`          |

多模板合并时按 `### 模板名 ###` 分节，重复指定同一个模板会自动去重。

## 参数

- `--list`：列出所有可用模板
- `--write [PATH]`：写入文件（默认 `./.gitignore`）；文件已存在时拒绝覆盖，除非加 `--force`
- `--append`：追加到 `./.gitignore` 末尾（stdout 模式下不使用）
- `--force`：允许 `--write` 覆盖已存在的文件
- 未知模板名会给出中文报错 + 近似建议（`pythno` → 你是不是想找：`python`？）

## 退出码

| 码 | 含义             |
|----|------------------|
| 0  | 成功             |
| 1  | 未知模板 / 拒绝覆盖 |
| 2  | 用法错误（没给模板名） |

## 诚实说明

- 模板是**人工精选的快照**，不是从上游实时同步的：日常项目够用，但如果你依赖某语言生态的最新忽略规则，请以官方模板为准核对一次。
- vscode 模板默认保留 `settings.json` / `tasks.json` / `launch.json` / `extensions.json`（团队共享的配置）；只想全忽略的话删掉那几行 `!` 即可。
- 本工具只生成文本，不检测项目里实际存在的文件——生成前建议先看一眼输出。
