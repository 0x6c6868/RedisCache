# RedisCache 开发指引

RedisCache 是用 C 编写的 Redis 模块。项目背景见 [README.md](README.md)，首个功能的行为和验收条件见 [SPEC.md](SPEC.md)。

## 代码入口

- `rediscacheobj.c` 包含模块入口 `RedisModule_OnLoad` 和命令实现。当前只有 `rediscacheobj.hello`。
- `redismodule.h` 提供 Redis Module API。README 标注的验证目标是 Redis 6.2.3。
- `Makefile` 生成 `rediscacheobj.so`。Linux 使用 `make`，macOS 使用已验证的 `make LD=cc`。

## 本地验证

从仓库根目录构建。选一个空闲端口，在独立的本地 Redis 实例中加载模块。例如用 `6380` 启动前台实例：

```sh
redis-server --bind 127.0.0.1 --port 6380 --save '' --appendonly no \
  --loadmodule "$PWD/rediscacheobj.so"
```

确认启动日志显示模块已加载后，在另一个终端运行：

```sh
redis-cli -p 6380 rediscacheobj.hello
```

预期返回 `hello`。验证结束后停止这个测试实例。

## 修改与验收

- 改动 Redis 命令前，先核对 `SPEC.md` 中的接口和验收用例。对外行为有变化时，同步更新规格和测试。
- 触及模块代码时，验证构建、模块加载、`hello` 命令和本次改动对应的行为。报告实际运行的命令、结果和待验证项。
