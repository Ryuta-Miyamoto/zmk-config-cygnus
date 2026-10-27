# zmk-config-cygnus

Cygnus キーボード用の ZMK ファームウェア設定です。全機種を `main` ブランチ 1 本で管理し、push すると GitHub Actions が全機種のファームウェアをまとめてビルドします。

## 機種とファイル

| 機種 | コントローラ | キーマップ | 設定 | ファームウェア名 |
|---|---|---|---|---|
| Cygnus 3x5 | XIAO BLE | `config/cygnus3x5_xiao.keymap` | `config/cygnus3x5_xiao.conf` | `cygnus3x5_xiao_left/right` |
| Cygnus 3x6 | XIAO BLE | `config/cygnus_xiao.keymap` | `config/cygnus_xiao.conf` | `cygnus3x6_xiao_left/right` |
| Cygnus 3x6 | nice!nano | `config/cygnus_xiao.keymap`（3x6 XIAO と共通） | `config/corne.conf` | `cygnus3x6_nicenano_left/right` |

- XIAO BLE 版のシールド（配線）は `boards/shields/cygnus3x5_xiao/` と `boards/shields/cygnus_xiao/` にあります。
- nice!nano 版は ZMK 標準の `corne` シールドを使い、キーマップは `build.yaml` で 3x6 XIAO 版のものを指定しています。3x6 のキーマップを直すと、XIAO 版と nice!nano 版の両方に反映されます。
- Mac / Windows の切り替えは、キーマップ内の Bluetooth プロファイル（0・1 = Mac、2・3 = Windows）で行います。
- `settings_reset_xiao_ble` / `settings_reset_nice_nano` は、ペアリング情報などを消すためのファームウェアです。

## 電池・充電 LED（XIAO BLE 版のみ）

`src/battery_led.c` で、XIAO BLE 内蔵の RGB LED に電池と充電の状態を表示します（`CONFIG_CYGNUS_BATTERY_LED=y` で有効）。

| タイミング | 色 |
|---|---|
| 電源オン時（2 秒間） | 緑：80% 以上／黄：20〜80%／赤：20% 未満 |
| USB 接続中・充電中 | シアンの点滅 |
| USB 接続中・充電完了 | 緑の点灯 |

## キー配置図

`config/*.keymap` を変更して push すると、`keymap-drawer/` の画像が自動で更新されます。

## 書き込み（macOS）

リセットボタンを 2 回押してドライブが出たら、ターミナルから `-X` 付きでコピーします（Finder だとエラー -36 が出ることがあります）。

```sh
cp -X cygnus3x5_xiao_left.uf2 /Volumes/XIAO-SENSE/
```
