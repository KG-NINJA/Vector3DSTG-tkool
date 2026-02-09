# STGbuilder (Vector Wireframe City Shooter Builder)

HTML single-file builder to create a vector-scan / wireframe style forward-scrolling 3D shooter.
ブラウザで開くだけで、`wireframe_cityshooter` 風のワイヤーフレームSTGを「ノブ+プリセット」で作って、単体 `index.html` として書き出せます。

## Features / 特徴

- No install, no deps: just open `STGbuilder/index.html` (no npm, no build tools)
- Export as a **single** `index.html` (offline-playable, no external files)
- Deterministic generation: same `Seed` + same config => same city / gates / enemy spawns
- Knobs + presets only (beginner-friendly / 破綻しにくい)

## Quick Start / 使い方

1. Open `STGbuilder/index.html` in a modern browser.
2. Adjust knobs (Seed, Building Density, Gate Interval, Enemy Density, Colors, etc.)
3. Click `Export Game` to download a standalone `index.html`
4. Open the exported `index.html` to play.

ローカルファイルの制限で挙動が怪しい場合は、ローカルサーバで開くのが確実です。

```bash
cd STGbuilder
python3 -m http.server 8080
```

Then open `http://localhost:8080/` and click `index.html`.

## Controls (Preview & Exported Game) / 操作

- Move: `WASD` / Arrow keys
- Shot: `Space`
- Missile: `F`

## Config Format / 設定データ

The builder and the exported game communicate via `GAME_CONFIG` only.
ビルダーと生成ゲームの境界は `GAME_CONFIG` のみです（互換性のため、ここを公開仕様として扱います）。

- Exported games include a fixed signature watermark: `#KGNINJA`
- 生成したゲームには署名ウォーターマーク `#KGNINJA` が表示されます

- `Save Config` downloads `stgbuilder-config.json`
- `Load Config` restores it (validated)

`Seed` is used for procedural generation (buildings / gates / spawns).
seed を変えるとレイアウトが変わり、同じ seed なら再現します。

## What This Is / これは何？

This repo includes:

- `STGbuilder/index.html`: the builder UI + live preview engine + exporter
- Exported output: a single `index.html` that embeds:
  - `const GAME_CONFIG = {...}`
  - inline game engine (Canvas2D vector-scan rendering)

## Limitations (v0) / 制限（v0）

- City-run template only (CityShooter特化)
- No timeline/wave editor yet (GUIでウェーブ配置する機能は未搭載)
- Audio is not the focus of v0 (無音でも成立優先)

## Roadmap / 今後

- More presets (Hangar launch / Space corridor style toggles)
- Optional “wave editor” mode (still safe by default)
- Mobile-friendly controls

## Notes / 注意

- The exported game is designed to run offline.
- If you modify `GAME_CONFIG` manually, keep types/ranges sane; invalid config may break gameplay.
