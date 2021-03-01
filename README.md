# 快速架設OdooERP (透過Docker建置)

### 前言
還記得在2017年第一次在自家電腦Win 7裡，安裝官方提供的快速安裝版，突然多出一個奇怪的帳號(後來才知道該帳號是給odoo使用)當時是非常不知所措。

回想前幾年的時間裡，OdooERP在台灣的資源是非常少的，光是要在電腦上順利安裝可以執行的環境，是非常不容易的。


如今能在國內/外巨人肩膀上，歸納出這一版快速架設OdooERP的方式，希望能提供給對於odooERP有興趣的新朋友，在一開始能更快、更方便踏入odooERP這個領域，也趁這個機會紀錄並作為GitHub上的第一篇文章。


---

#### Step1：安裝Docker

首先安裝**Docker**，透過Docker來做為我們的odoo主機，一來可減少安裝odoo複雜度，二來可加快跨入odoo的門檻。
>Docker支援作業系統：https://docs.docker.com/engine/install/#supported-platforms


在Mac/Windows環境下，可透過**Docker Desktop**更簡易、更快速進行Docker的安裝，
這是也為了讓初次接觸的Odoo的新朋友，未來能透過圖形使用者介面(圖一)進行學習操作(START/STOP)，減少需要學習Docker指令的門檻。

| ![Docker Engine](https://lh3.googleusercontent.com/A5CpkXNPFszRCIm5HCD-_y4XdOKJYWEUplQhET7GDAQEf6haMG9ZiCH8rItw50kketPoYVyle7MhTPz1h-Y3mUZvo3wz9mKsrkhY9Eet12Oy78T0HBxztigIqLwgofdw4bOT0wHHk4SvljBtveYRdAg09M9S_bpQYBJYsTfHqKCpN2t_XGEedhZpJfRAb93RkShQwcXxi8s9Bb2Deu8MaAkjb1kvuLZBjnbhQXyMRAIUgwMc4hafeOJB-78i0_87ePKLVaCcu8Ql0qkvH8N5_G8saxj9vT_v71A6cJ4J3Iifhnke2kZ07P7kBEZfAel7Hf62XrZ75UwWkR2T2AR-AzREzRShm-Ylea3_4rvXdY38Eq1W8nAWV_rs8kvCj3pvrHPPqE_EaxkCfVMWZSfu50KHafK4so8iJebxL6ljj8NTVqHY3LEfO1qdVdMK_lnvQ0hDJ88_5irlzkkCNT8Z1rwLExF2IntHMTyiw7Cg0P7o3BjR_f9wNTsxGrKDbMzMZx-NqcruxVPGJKGKTP9pPLoyhB-yNGMHLwCJCvPK1TY3YqvlLRIzTmGNvnOGgQRhVwgC88X053jbdQFhFaf2RZH3qt_OzpnEW1jzCcTCOUPE0Gw1P3x2qpt5rq7HOHQx0vxh8rT0wUB9kXj83JtAEYDZAbJQQES9xosjOKUFDNTpLGuvVxZinou8PQE0jw=w2619-h1600-no?authuser=0 "Docker Engine")  |
| :------------: |
|圖一   |


這裡先檢查自己電腦的作業系統是否支援：
1. Mac：https://docs.docker.com/docker-for-mac/install/
   >系統要求：macOS 10.14起。
   >詳細說明：https://docs.docker.com/docker-for-mac/install/#system-requirements
2. Windows 10 Pro：https://docs.docker.com/docker-for-windows/install/
   >系統要求： 64-bit: Pro, Enterprise, or Education (Build 17134 or later)。
   >詳細說明：https://docs.docker.com/docker-for-windows/install/#system-requirements*
3. Windows 10家用版：https://docs.docker.com/docker-for-windows/install/
   >系統要求：Windows 10, version 1903 or higher.。
   >詳細說明：https://docs.docker.com/docker-for-windows/install-windows-home/#system-requirements*


**如果WIN 10家用版的朋友還是<font color="#FF0000">無法安裝</font>，那只能考慮安裝Docker Toolbox了。**
>參考來源：https://github.com/docker/toolbox/releases

---

#### Step2：檔案下載

下載本文[odoo-docker-build](https://github.com/jerryxu4j/odoo-docker-build)檔案，
點選[Code]後，會如圖二所示，可以透過兩種方式把檔案下載下來
1. 入門：點選`Download Zip`下載後，解壓縮zip即可。
2. 進階：透過`git clone`指令下載。


| ![Download Code](https://lh3.googleusercontent.com/FNCtYCW0A5jL6-kkUyzTuez_YKZxczMacfejmXqmcPWh9O6Bi2fEYowxIz07a1KQNYWCTR0f3y6m_FSqeQzuSPdMf1gBYLn7ZAAMWAh4KwzTOPsNBkjCq7YjlZII_pdfbnz-HaUXvUDLFSygk8hpEoKWLvUSF6Z9H2jD3ASmmG3ll1SpeNggWWcxGHNO7d_MinNOopxHfqMkRzTHWZQ3dD1I8GCRcSWi9V9QtfSQcQSQNvz7CsEOfbqiplQhzQ3zdbs8pf2orPiDIitoGbYf360trmy6LM3fys0ZWA7Kiwt0MCnaMIheckiuVvzjEzn_-taPNY44vpDkB8kNrkkxELVCGoUzTE6ejG8y0H21jdByN0ABxuybqEj4p3GFkt5uu_roAj1B1q_DqeLd2LQH0GNGGw0DO4jHGrLxbwKnGct42K_vsC2LZLB5XZnC-kSj8D4EVin1_-swMDEbQHLIjlq9LOHIhuWFFZDyMg2xRd1qwduiic-_9b-t7KuflotXxigNLLligbFW58XM6iZubIyp7or9eND1yzFOYUhdBu87w1_izpYPo__4mRbw-gU4FeVPxWZT7u1at0pVmkCGcrgu8vUma6Yd58ZAvi0RL7e9766WAZtRZG8Ixlw9NMeLolhF9X2OND5qsynnYVFu8w8g4D203Wk55qiBk-_uIPFRB-F1eUUkKfv2sBsSFg=w708-h596-no?authuser=0 "Download Code")  |
| :------------: |
|圖二   |

---

#### Step3：認識目錄、檔案

下載(解壓縮)後的目錄如下，此階段先認識每個檔案及目錄的用途。
- odoo-for-docker
   - docker-compose.yml```使用該檔案並且透過docker快速安裝OdooERP系統```
   - config```放置設定檔的目錄```
     - odoo.conf ```OdooERP使用到的系統設定檔```
   - addons```放置第三方(客製)addon的目錄```
     - purchase_request```示範用addon```

---

#### Step4：執行docker compose進行OdooERP安裝

安裝步驟：
1. 執行Docker Desktop
2. 打開Terminal(圖三)切換目錄到`odoo-docker-build`下，並且輸入以下指令進行啟動
    >docker-compose up -d
3. 安裝完畢，並可透過網頁輸入`127.0.0.1:8069`或`localhost:8069`進入OdooERP(圖四)
4. 若需要移除本系統，可輸入以下指令進行完整移除
    >docker-compose down

| ![Terminal](https://lh3.googleusercontent.com/PnWtTXY_jfLgkC_juOz6sE3-ZGI-lRy8m4Xb0VbHTiVHBSBP5K6lW8HuHzAyKmbrJNtF_1JvsHmN2aUplQJIjw1tZTm_15sJWa_9n4i2i3iqmKkQM-bp6K1sJb_ZXauJ-VtDjc0_rWjo4e_zhd28kEaYRVf9IUotvnKSfhGw_JnMxtsvniIKSRwswzJZgyt5_rLs6wjmOOdC2f904w931mpQsBuTS6FEYzvCkGlEMtjj3u6F4XbkedQVcTeJfze9yTGkSvDldsxmYxOmUyTXejG86WTj4CGZ58vFwmlaE6mR6FZoZW_Y0P4Hs2jIC3PN3ohimGure46xWme0lMeBJ1MiUdORYN7psd1zH0c7R-0qSd0kA-yctMXQbF1cHx60f_jjHvRBtCV0SRJpsCVIvCAk0eShBn52gOS0MGKmdO_MZ8RTMjrY-pg5fIFtyoqKvLxMDiTjv8dDOlkFup8ne5_IkpDgJlzETCmmm0Qti-ecP1T-TIWMNHiklr9k-s1J0JGVrphmPiCxHab2NwKouh6GN9x0eRJumX0fsG7zEK65hf3vMl2_lZcPwnRc-VWeF7QUzm7Lcs_s_g3F_aK-JxdaSxK1rtztWinC1jsWTu3qTD7QVtQnhl62YPbdOcZrXkpg_MQtEWGJPPRcmveMyTp6SZzHZs-LepBKM29qHaMsVrhXd_L_cBKLCicGMA=w2094-h1214-no?authuser=0 "Terminal") |
| :------------: |
|圖三   |

| ![Create DB](https://lh3.googleusercontent.com/zpO55Vhuh5yuB5FRzJXV10yURcRybrPePFgR5cJInfwayxf1lEjReSJt6FQo-Z_sWm18W0QAzLe1dV6785oyCZso4h_W2UGnq0eXwmaRKZNvjZmtpt4u6xeFMX85laUBAsIH7pof6yE8sNHHD50v-qVZiw8GNhhkiEsDlfM2ppU_QE-eIchQd4Tea1FS9Kx-7LmMu5MbOWeHc0TygtqM7fDsH0VvtacghvUD3dPg7Lx_P9glu7cz4DcaQB7uhC_80YpaM5WAVJ9jEmQ9RySq8B1daxJ5Pn-8__7f86UMFsYLkTYTDJ3hP-S2tEU2muCKFwZYqm3jiTIPjHB11NN021ohh6uq1tzzcj8UQMafyKFp1V6EItbjAAi34dBOKUPUFAG6YNQUuxsVoDsoJffYqgkQYmM1qVvdS7XZL18oyNYfWj0agcxo-MlGWGpVvMThmb8B6X5xHzVlbeEi2ja6eXSVZFOM17dRzqouLBeSsLffMsPFaNmD44XH087C1UbSLiBFGDfhnjDjqqlJi-vTNiaBKuIraT4bhowzKj-PYQEnSv7bUIBIZ3uKjGn1NBofrPRVJN8k_fsYgWIvgp-AB9thqz-GjCkiXCn2ve7drBYGhifupY6Lzeyp0HH2aINLDVrrr-SD9YrwVya-pB7tO0RGiNRdil8o1rOoQXFn_CULfAeubcy2DZegUTSsLg=w1946-h1536-no?authuser=0 "Create DB") |
| :------------: |
|圖四   |

---

Reference: https://hub.docker.com/_/odoo

License: [CC-BY](https://creativecommons.org/licenses/by/3.0/)
