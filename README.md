# ai-dev-env-report

Windows 本机 AI 开发环境安装清单 —— 单文件 HTML 报告，表格化呈现每一步的环境状态。

## 内容

按安装链路逐项列出：

| 环节 | 检查点 |
|------|--------|
| Python 运行时 | 版本、venv 隔离、PATH 优先级 |
| llama.cpp / llama-cpp-python | wheel 构建、CPU 线程绑定（`LLAMA_NUM_THREADS`） |
| Ollama | 服务可用性、模型拉取 |
| 长路径 / 编码 | Windows 长路径策略、UTF-8 输出 |

每项带状态标记与修复命令，可直接照着执行。

## 状态标记约定

- `PASS` 通过
- `WARN` 需留意（通常不影响主流程）
- `FAIL` 阻塞项，必须先修

## 已知坑

| 现象 | 根因 | 修法 |
|------|------|------|
| 小量化模型在 CPU 上极慢 | llama.cpp 默认线程数 = `cpu_count - 1`，小模型瓶颈在内存带宽不在算力 | 把线程锁到 2–4 |
| wheel 构建失败 | 缺 MSVC 构建工具 / 长路径未开 | 开长路径策略 + 装 Build Tools |
| 控制台乱码 | GBK 默认代码页 | 强制 UTF-8 输出后重跑 |

## License

MIT
