# Etsy 文档配图清单（26 张）

全部放进 `/home/rokeyzki/mockspark/mockspark-docs/images/connections/etsy/`，文件名照抄下表，正文里的 `{/* IMAGE-TODO ... */}` 会按这个文件名替换成 `<Frame>` 块。

按「在哪截」分组，一次坐下能截完一组。

---

## A. Etsy 后台 Shop Manager（4 张）

Settings → Partners you work with

- [ ] `pp-settings-nav.png` 左侧 Settings 展开，Partners you work with 高亮
- [ ] `pp-add-form-top.png` Add a production partner 弹窗上半部分：名称、Show this to buyers 开关、Location
- [ ] `pp-what-they-do.png` 弹窗里 What they do for you 那一段，含描述输入框（**框里最好填上文档给的范例句**）
- [ ] `pp-more-about.png` More about your partner 两个下拉框已选好的状态

## B. Etsy 网站其他位置（4 张）

- [ ] `etsy-oauth-consent.png` Etsy 授权页，权限列表 + Allow Access 按钮（连店时顺手截）
- [ ] `etsy-account-apps.png` Etsy 账号 → Your Account → Apps，能看到已授权的 Mockspark 和移除入口
- [ ] `etsy-listing-personalization-field.png` 商品页上买家看到的 Personalization 输入框与提示文字
- [ ] `etsy-personalization-filled.png` 结算流程中 Personalization 已粘好定制 ID 的状态

## C. Mockspark 连接页（6 张）

Connections → Etsy

- [ ] `nav-connections-etsy.png` 顶部导航 Connections 下拉展开，鼠标停在 Etsy 上
- [ ] `empty-state.png` 一个店都没连时的页面，只有虚线加号卡片 ⚠️ 见下方「不好截的」
- [ ] `confirm-modal.png` Confirm Connection to Etsy 确认弹窗
- [ ] `connected-card.png` 连接成功的店铺卡片：Shop name / Status: Available / Updated at / Default 角标
- [ ] `card-hover-actions.png` 卡片 hover 露出 View shop、Set as default、Reconnect、Disconnect
- [ ] `reconnect-required.png` 卡片显示红色 Reconnect required 标签 ⚠️ 见下方

## D. Mockspark 发布页（4 张）

- [ ] `publish-form-full.png` Etsy 分支完整表单，从 Store 到 Buyer personalization
- [ ] `shipping-profile-sentinel.png` 下拉里出现 Mockspark Shipping (free shipping)，下方解释文案 + 邮编输入框 ⚠️ 见下方
- [ ] `publish-success.png` 发布成功状态，含指向 Etsy listing 的链接
- [ ] `personalization-toggle.png` Buyer personalization 区块，开关打开

## E. 买家自助定制页（2 张）

`/guest/customize?p=etsy&ref=<listing_id>`

- [ ] `guest-designer.png` 设计器界面
- [ ] `guest-success-id.png` 提交成功页，显示定制 ID 与复制按钮

## F. Mockspark 订单页（5 张）

- [ ] `order-list.png` Order Items 列表，含 Etsy 订单和平台标识
- [ ] `order-detail-ready.png` Etsy 订单详情，状态 Ready to fulfill，可见发往履约平台的按钮
- [ ] `order-unfulfillable.png` 订单详情显示 Unfulfillable，以及买家实际填写的内容 ⚠️ 见下方
- [ ] `order-redesign-link.png` 订单详情上「给买家补设计」链接的复制入口
- [ ] `multi-item-notice.png` 「This Etsy order has more than one item」提示条 ⚠️ 见下方

## G. 需要制作，不是截图（1 张）

- [ ] `hero.png` introduction 首屏配图，Mockspark 编辑器 + Etsy 商品页并排，风格参考现有 `/images/introduction.jpg`

---

## ⚠️ 五张不好直接截的，处理办法

| 图 | 为什么难 | 建议 |
| --- | --- | --- |
| `empty-state.png` | 你账号已经连了 sparktest 和 LefxeijWander | 用一个新注册的空账号截，或临时断开再连回来（断开不影响已上架 listing） |
| `reconnect-required.png` | 要令牌刷新失败才出现 | 之前冒烟验过的办法：临时把 integrations 那行的 `config.refreshFailedFor` 设成当前 refreshToken，截完删掉。不会动到真 token |
| `shipping-profile-sentinel.png` | LefxeijWander 已有运费档案 310430297046，虚拟项不出现 | 需要一个没有任何 shipping profile 的店。这条路径本来也一直没真机跑过，截图正好顺带补验一次 |
| `order-unfulfillable.png` | 要一张买家没填对定制 ID 的订单 | 自己下一单，Personalization 随便填几个字符（不满 36 位也行），等轮询入库 |
| `multi-item-notice.png` | 要一张含两个及以上商品的 Etsy 订单 | 自己下单时加购两件 |

后三张都要真实下单，可以合并成一次：**下一单填错 ID 的**，再**下一单买两件**，两张图一起拿到。

---

## 截完之后

丢进 `images/connections/etsy/` 就行，告诉我一声，我把正文里的占位注释换成 `<Frame>` 块并补上 `alt`。也可以你自己换，格式是：

```mdx
<Frame>
  <img src="/images/connections/etsy/connected-card.png" alt="A connected Etsy shop card" />
</Frame>
```
