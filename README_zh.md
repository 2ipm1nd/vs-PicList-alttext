# vs-piclist

> 基於 [PicList](https://github.com/Kuingsmile/PicList) 的強大 VSCode 圖床外掛。

[![version](https://img.shields.io/vscode-marketplace/v/Kuingsmile.vs-piclist.svg?style=flat-square&label=vscode%20marketplace)](https://marketplace.visualstudio.com/items?itemName=Kuingsmile.vs-piclist)
![Visual Studio Marketplace Rating](https://img.shields.io/visual-studio-marketplace/r/Kuingsmile.vs-piclist?style=flat-square)
[![installs](https://img.shields.io/vscode-marketplace/d/Kuingsmile.vs-piclist.svg?style=flat-square)](https://marketplace.visualstudio.com/items?itemName=Kuingsmile.vs-piclist)
[![GitHub stars](https://img.shields.io/github/stars/Kuingsmile/vs-piclist.svg?style=flat-square&label=github%20stars)](https://github.com/Kuingsmile/vs-piclist)

## 概覽

`vs-piclist` 是一款功能豐富的 VSCode 圖床擴充套件，支援一鍵上傳圖片到遠端圖床，並自動插入圖片連結到目前的檔案。

相較於其他方案，`vs-piclist` 支援圖片壓縮、水印等進階處理，功能更全面。

## 與原版（vs-piclist）的異同比較

本版本是針對原版 `vs-piclist` 進行深度優化與功能改良的自用/社群加強版本。以下是主要的改進與差異對照表：

| 功能與修復項目                   | 原版 (`vs-piclist`)                                                                                                               | 本加強版 (`vs-piclist-alttext`)                                                                                                       |
| :------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------ |
| **支援 `file://` 本地路徑上傳**  | 被判定為遠端 URL。當 `skipRemoteImages` 啟用時會被直接忽略；即使未啟用也會因為 Node 檔案系統不支援 `file://` 格式而導致上傳失敗。 | **完美支援。** 自動將 Markdown 中的 `file:///` 協定網址解析並還原為作業系統的原生絕對路徑，確保本地圖片能夠被正常讀取、上傳並替換。   |
| **保留自訂 Alt Text (圖片描述)** | 上傳成功後會直接以新圖片的格式整行替換，導致原本手動寫好的 `alt text` 被預設檔名覆蓋。                                            | **自動保留。** 智慧偵測目前行既有的 `![alt text](url)` 結構，**只替換網址部分**，完整保留你精心撰寫的圖片描述。                       |
| **GitHub Actions 自動化發行**    | 每次發佈 Release 時，必須手動在本地修改 `package.json` 的版本號，否則打包檔名出錯或打包出舊版本。                                 | **100% 全自動化。** GitHub Actions 會在打包前自動將 `package.json` 的版本號與你推送的 Git Tag 同步，直接打 Tag 推送即可完成正確發行。 |

### 先決條件

使用前請先安裝 [PicList](https://github.com/Kuingsmile/PicList) 桌面端或 [PicList-Core](https://github.com/Kuingsmile/piclist-core)。

### 為什麼選擇 vs-piclist？

雖然有如 [vs-picgo](https://github.com/PicGo/vs-picgo)（基於 [PicGo-Core](https://github.com/PicGo/PicGo-Core)），但 `vs-piclist` 提供了更豐富的功能，滿足更全面的圖片管理需求。

## 功能

- **一鍵上傳**：輕鬆上傳圖片到任意圖床。
- **拖曳上傳**：直接拖曳圖片到編輯器即可上傳。
- **全部上傳**：一鍵上傳目前檔案所有圖片。
- **右鍵上傳選中圖片**：右鍵上傳選中的圖片。
- **自動插入連結**：上傳後自動插入圖片連結。
- **圖片管理**：在 VSCode 內直接刪除遠端圖床圖片。
- **進階處理**：支援圖片壓縮、水印等後處理。
- **遠端伺服器模式**：支援透過遠端 PicList 或 PicList-Core 服務上傳。

### 演示

<details>
<summary>剪貼板上傳</summary>
<img src="https://s2.loli.net/2023/08/31/XvZrtgiuWwLYIHy.gif" alt="clipboard.gif">
</details>

<details>
<summary>資源管理器上傳</summary>
<img src="https://s2.loli.net/2023/08/31/npvwQoT4Ucr5mPN.gif" alt="explorer.gif">
</details>

<details>
<summary>本地路徑或 URL 上傳</summary>
<img src="https://s2.loli.net/2023/08/31/tAW54rVFhO2KSTo.gif" alt="input box.gif">
</details>

<details>
<summary>拖曳上傳</summary>
<img src="https://s2.loli.net/2023/09/01/rflXoJLsR5heDqK.gif" alt="drag-and-drop.gif">
</details>

<details>
<summary>雲端刪除圖片</summary>
<img src="https://s2.loli.net/2023/09/01/8oYzJinhgajLfdI.gif" alt="delete.gif">
</details>

<details>
<summary>上傳檔案中所有圖片</summary>
<img src="https://s2.loli.net/2024/06/16/9JDyICxZ3mUEBio.gif" alt="upload-all.gif">
</details>

<details>
<summary>右鍵上傳選中圖片</summary>
<img src="https://s2.loli.net/2024/06/16/GUVjraIWTuX2wgn.gif" alt="upload-selected.gif">
</details>

## 設定

![setting](https://s2.loli.net/2023/08/31/vL7WgcDrxIGzZBR.webp)

### 上傳 API 地址

PicList 上傳介面，預設：`http://127.0.0.1:36677/upload`。詳見 [PicList Server](https://piclist.cn/en/advanced.html#use-of-built-in-server)。

### 刪除 API 地址

PicList 刪除介面，預設：`http://127.0.0.1:36677/delete`。詳見 [PicList Server](https://piclist.cn/en/advanced.html#use-of-built-in-server)。

### 粘貼格式

預設：markdown。

| 類型   | 格式                     |
| ------ | ------------------------ |
| url    | `url`                    |
| markdown | `![alt](url)`           |
| html   | `<img src=url alt=alt>` |
| ubb    | `[img]url[/img]`        |
| custom | `custom`                 |

### 自訂格式

預設：`![$filename]($url)`。

### URL 編碼

插入連結時是否編碼 URL。預設：`false`。

### 拖曳上傳

是否啟用拖曳上傳。預設：`true`。

### 遠端伺服器模式

如在伺服器或其他機器部署 PicList 或 PicList-Core，可開啟遠端模式，上傳將以檔案方式傳送。

## 作者

- [Kuingsmile](https://github.com/Kuingsmile)

## 依賴

- [PicList](https://github.com/Kuingsmile/PicList)
- [PicList-Core](https://github.com/Kuingsmile/piclist-core)
