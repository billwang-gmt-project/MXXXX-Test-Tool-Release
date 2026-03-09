## APP版本編碼規則

XX.YY.DDDD.ZZZZZ
•	第一碼:大改版
•	第二碼:小改版
•	第三碼:編譯日期(from 2000)
•	第四碼:流水號
•	測試版(尚未做完整全面測試)只會改後兩碼

## V1.1.9564.22609

[M8421]
- 修正: 在自動偵測M8421後,燒錄板會重置TX/RX極性設定為LOW

## V1.1.9561.22582
[M8322CA]
- Fix: online test 調整 Ratio值時，計算的轉速沒有跟著計算
[M8421]

- Fix: Speed curve
OOO
Linear_sw 在 OFF時，應該要把XMD & YMD的階數寫入RP1、RP2 (XMD跟RP1是共用Register、YMD跟RP2是共用Register)
且畫面要更新 (目前只有切 ON、OFF不會更新，還要調一下XMD的數值才會更新)
COO:
- Linear_sw 在 OFF or ON 時，XMD都固定在75%且反白，且不能寫入值至RP1
YMD的規則和OOO相同
- Fix: zero_sw在on & off 時都還要動一下別的選項畫面才會更新
- Fix: M8421B有些GUI項目不見

[MXXXX]
- ADD M8421BB support

[M8323]
- 加入轉速比
<img width="625" height="467" alt="image" src="https://github.com/user-attachments/assets/a567ec28-9ef9-43c3-a4c6-a676dfcb2f48" />

## V1.1.9532.22557

[M8323]

- GUI客製化
修改ApplicationSetting.ini中的CustomId
```
{
  "FirmwareVersion": "26010200",
  "_ChipFamily": "G8XXX",
  "IsBbMode": true,
  "CustomId": 2,
  "_IsFactoryMode": true,
  "_IsCheckAppUpdated": true,
  "ReadProtectionKey": "305419896",
  "ReadProtectionToken": "THIS IS READ PROTECTION TOKEN"
}
```

CustomId :0 => 舊介面
CustomId :1 => 擎宇
<img width="312" height="236" alt="image" src="https://github.com/user-attachments/assets/8f40ff9a-ae4a-4c3a-a0e2-ae1e9947fa05" />

CustomId 2 => 華盈
<img width="313" height="236" alt="image" src="https://github.com/user-attachments/assets/80fa29c1-bb88-40a4-8afc-e62c59b5449b" />

## V1.1.9525.22506

[M8322CA]

- Fix 全弦後銜接duty選項相反
- Fix 在 OOO 時不顯示 Min duty

## V1.1.9523.22503

### 啟動頁面修改需求清單 (Startup Page UI/UX Optimization)

### 1\. 圖形介面調整 (Graphic Adjustments)

- [x] **新增波形圖示**：在圖形位置 **6** 與 **7** 之間，加入「小方波」圖形(![][image1])，用以表示銜接狀態。  
- [x] **同步編號標註**：在圖形關鍵點位與下方對應的文字元件旁，統一標註數字 **1 \~ 8**。

### 2\. 顯示邏輯與隱藏項目 (Visibility & Logic)

**隱藏特定設定**：

- [x] 隱藏 **LA 設定** 與其對應的設定值。(Default code改為 0X02 \= 0X14)  
- [x] 隱藏 **Option\_ss\_double** 下拉選單 (SS time整合成一個表單\=\> 先不做)  
- [x] 隱藏 **位置 6 (啟用)** 相關控制項。

**選單功能整併**：\=\> 先不做

- [x] 將 **Enable** 項目整併至「緩變 (Soft Start)」選單內。  
- [x] 剔除選單中重複的選項，確保介面簡潔。

**銜接參數設定**：

- [x] 「全弦後銜接 duty」選項 1 設為 **15%**。  
- [x] 「全弦後銜接 duty」選項 2 設為 **曲線內差**（此數值 22.5deg 需隱藏）。  
- [x] Align SS slope 1/8 or 1/4 ss time \=\> 選單相反\=\> 定位電流斜率動態調整

### 3\. 文字描述修正 (Labeling)

- [x] **位置 1**：描述文字修改為「**定位電流斜率**」。  
- [x] **位置 3**：描述文字修改為「**縮短啟動時間**」。  
- [x] **其餘描述**：檢查並優化所有與編號對應的參數說明文字。

### 4\. 排版與順序 (Layout Reordering)

- [x] **元件重排**：下方文字與輸入框需嚴格依照數字編號 **1 ➔ 8** 的順序進行排版。

### 5\. M8322CA Default code更改

- [x] **Byte 0x02 \= 0X14**  
- [x] **Byte 0x09 \= 0X3F**  
- [x] **Byte 0x0A \= 0X7F**

### 6\. YP1在COO、CCO、COP選單顯示更改

- [x] **原本在close loop名稱會變為 Min duty且數值變一半，現在變回原本的YP1且值恢復0\~50，另外在旁邊顯示 Min duty，值為YP1\*0.5**

### 7\. 以下隨啟動設定動態調整

- [x] **切換 全弦後銜接duty(%),  啟動後銜接duty(%) 名稱**  
- [x] **定位電流斜率列表**

### 曲線頁面

- [x] ## 說明曲線  - - - - Open Loop ────── CLose Loop

- [x] ## 預設值帶入不要讓軟體一打開就警示不合理的設定\=\> 先不做

M8323
修改溫度公式
增加溫度moving average
