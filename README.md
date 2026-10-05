# KB78 ZMK 設定

自作キーボード KB78（78キー、MacBook Air 配列、XIAO nRF52840 Plus）の ZMK ファームウェア設定。
計画全体は親フォルダの `CLAUDE.md` を参照。

## 中身

| 場所 | 内容 |
|---|---|
| `boards/shields/kb78/` | キーボード本体の定義（ピン割り当て、物理配列） |
| `config/kb78.keymap` | キーマップ（通常レイヤーと Fn レイヤー） |
| `config/kb78.conf` | 機能の ON/OFF |
| `config/west.yml` | 使う ZMK のバージョン（main） |
| `tests/` | 実機なしで動くキーマップのテスト |
| `keymap-drawer/` | キーマップの図（GitHub が自動で作る） |

## GitHub Actions

- **Build ZMK firmware**: ファームウェア（`.uf2`）を作る。実行結果の Artifacts からダウンロードできる
- **Keymap tests**: `tests/` のテストを実行する。キーを押したときにパソコンへ送られる信号が、期待どおりかを確かめる
- **Draw keymap**: キーマップの図を作り、`keymap-drawer/` に追加する（自動でコミットされるので、手元では `git pull` が必要）

## テストの追加方法

`tests/<名前>/` に3つのファイルを置く。

- `native_sim.keymap`: どのキーをどの順で押すか（`ZMK_MOCK_PRESS(0, キー番号, 待ち時間ms)`）
- `events.patterns`: ログから取り出す行（他のテストからコピー）
- `keycode_events.snapshot`: 期待される出力

キー番号は `config/kb78.keymap` の先頭のコメントを参照。
