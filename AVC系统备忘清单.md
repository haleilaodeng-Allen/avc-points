# AVC 积分查询系统 · 备忘清单

> 所有关键地址、操作流程、踩过的坑都在这里。以后忘了照着看就行。

---

## 一、线上网址(收藏到浏览器书签)

**积分查询(自己用)**
```
https://haleilaodeng-allen.github.io/avc-points/avc-query.html
```

**促销展示(给客户看)**
```
https://haleilaodeng-allen.github.io/avc-points/promo.html
```

---

## 二、数据地址(系统首次打开要填的)

**酒店积分数据 — hotels 文件夹地址**
```
https://raw.githubusercontent.com/haleilaodeng-Allen/avc-points/main/hotels/
```

**促销数据 — promos 文件夹地址**
```
https://raw.githubusercontent.com/haleilaodeng-Allen/avc-points/main/promos/
```

⚠️ 关键:地址结尾**必须有 `/`**!少了斜杠会"找不到数据"。

---

## 三、GitHub 仓库

- 用户名:`haleilaodeng-Allen`
- 仓库名:`avc-points`(Public 公开)
- 仓库地址:https://github.com/haleilaodeng-Allen/avc-points

仓库结构:
```
avc-points/
  ├─ avc-query.html        积分查询页
  ├─ promo.html            促销展示页
  ├─ hotels/               酒店积分数据
  │    ├─ index.json       清单(列出所有酒店文件名)
  │    └─ 各酒店.json
  └─ promos/               促销数据
       ├─ promo1.json      住宿促销
       ├─ promo2.json      Club Escapes
       └─ promo3.json      限时优惠
```

---

## 四、加新酒店的流程

1. 打开酒店页面,**先看有没有 1-12月柱状图**
   - 有柱状图 → 固定积分,可以加
   - 没柱状图 → 浮动价,**不要加**(会查到错价)
2. F12 → Network → Fetch/XHR → 找 `seasonality-data` → Copy response → 存成 txt
3. 用**清洗工具**清洗 → 下载酒店 json
4. 把 json 放进本地 `hotels` 文件夹
5. 编辑 `hotels/index.json`,加一行新文件名
6. GitHub Desktop:Commit + Push
7. 等 1-3 分钟,刷新查询页

---

## 五、更新促销的流程

1. 扒促销数据(F12 找 `resort-promotions` 接口)
2. 存成 `promo1.json` / `promo2.json` / `promo3.json`(覆盖旧的)
3. 放进 `promos` 文件夹
4. Commit + Push
5. 刷新促销页

促销页会自动算"还剩几天",每天打开自动更新。

---

## 六、踩过的坑(以后避免)

| 坑 | 正确做法 |
|---|---|
| index.json 文件名少 `.json` | 文件名必须带 `.json` 后缀 |
| index.json 行尾逗号 | 每行末尾有逗号,**最后一行不要**逗号(或新酒店加在中间最稳) |
| 文件名要和实际一致 | index.json 里的名字 = 实际文件名(复制,别手打) |
| 大小写 | GitHub 区分大小写,清单和文件必须一致 |
| 文件夹地址结尾 | **必须带 `/`** (如 `/hotels/`) |
| 改文件后看不到更新 | GitHub 有 1-3 分钟延时,Ctrl+Shift+R 强刷 |
| 中文引号 | JSON 只认英文双引号 `"`,别用中文 `"" |
| 重名酒店 | 加新酒店前先查有没有重复(可让 Claude 帮比对) |
| 改文件名后缀 | 先在 Windows 显示"文件扩展名",再改 |

---

## 七、工具清单(本地用,不耗 Claude 额度)

- **清洗工具** `avc-cleaner.html` — 原始数据 → 干净酒店 json
- **打包工具** `avc-packer.html` — 批量打包多个酒店 + 生成 index.json
- **促销汇总** `avc-promo.html` — 本地速查促销(自己看)

---

## 八、数据维护提醒

- 酒店积分:AVC 滚动放价,大约覆盖未来 12 个月。**每季度重扒一次**主力酒店,保持数据新鲜。
- 促销:变化快,**想看最新就重扒一次** `resort-promotions`,覆盖 promo1~3。
