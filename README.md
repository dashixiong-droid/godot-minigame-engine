# Godot Minigame Engine

定制编译 Godot Web 引擎，适配微信小游戏运行时。

## 为什么需要这个？

上游 godothub 的 `.tpz` 模板中，`godot.wasm` 使用了 WebAssembly Exception Handling (Wasm EH) 指令，
但微信小游戏的 WASM 运行时不支持该特性，导致报错：

```
CompileError: WebAssembly.instantiate(): Compiling function failed: Invalid opcode 0x6
```

本仓库用 `exceptions=disabled` 重新编译 Godot 引擎，解决此兼容性问题。

## 工作流

1. 从 `godotengine/godot` 官方源码编译 Web 版
2. 禁用 Wasm EH（`exceptions=disabled`）
3. 保留 GDExtension 支持（`dlink_enabled=yes`）
4. 用编译产物替换上游 `.tpz` 模板中的 `engine/godot.wasm.br` + `engine/godot.js`
5. 打包为新的 `.tpz` 发布到 Release

## 支持版本

| Godot | 上游模板 | 状态 |
|-------|---------|------|
| 4.3 | minigame4.3.0.3.tpz | ✅ |
| 4.4 | minigame4.4.0.1.tpz | ✅ |
| 4.5 | minigame4.5.1.tpz | ✅ |

## 使用

1. 从 [Releases](https://github.com/dashixiong-droid/godot-minigame-engine/releases) 下载对应版本的 `.tpz`
2. 替换 `addons/godot-minigame/templates/` 中的上游模板
3. 或直接解压到微信小游戏导出目录

## 相关仓库

- [godot-minigame](https://github.com/dashixiong-droid/godot-minigame) — 编辑器插件编译 + 模板分发
- [godothub/godot-minigame](https://github.com/godothub/godot-minigame) — 上游插件源码

## License

Godot 引擎遵循 [MIT License](https://github.com/godotengine/godot/blob/master/LICENSE.txt)。
