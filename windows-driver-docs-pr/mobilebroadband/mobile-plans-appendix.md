---
title: 移动计划附录
description: 本主题介绍附录移动计划程序的信息。
ms.assetid: B3B478DB-78F4-4031-B041-DCBAACC15D6F
keywords:
- Windows Mobile 计划附录，移动计划附录移动运算符
ms.date: 09/17/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: f6a2edbb0ed48e11383401b0e35249263a49276f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522187"
---
# <a name="mobile-plans-appendix"></a>移动计划附录

[!include[Mobile Plans Beta Prerelease](../mobile-plans-beta-prerelease.md)]

## <a name="web-portal-flow-and-reference-design"></a>Web 门户的流和引用设计

此参考设计是可以更改以最好地表示您的品牌和产品的模板。 此参考设计显示了与导航元素，品牌位置和网站功能的建议的 UX 设计。

### <a name="mo-direct-reference-site-walkthrough"></a>MO 直接引用站点演练

1. 用户单击"继续"按钮：

    <img src="images/dynamo_appendix_mo_direct_1_continue.png" alt="MO Direct walkthrough: user clicks on the continue button" title="MO 直接演练： 用户单击继续按钮" width="600" />

    - 此对话框会提示通过计划移动应用。

2. 用户输入 MO 直接门户，并使用其 MO 帐户登录：

    <img src="images/dynamo_appendix_mo_direct_2_sign_in.png" alt="MO Direct walkthrough: user enters MO Direct portal and signs in with their MO account" title="MO 直接演练： 用户输入 MO 直接门户和使用其 MO 帐户符号" width="600" />

    - 页面布局是在所有页面保持一致。 例如，徽标和品牌元素位于左上方，并导航元素位于底部。
    - 登录页可以链接到注册新帐户。
    - "忘记了密码"是可选的。 请注意，窗体是 Walled Garden，仅计划移动应用可以访问 internet。 如果你想要支持通过 MO 直接门户重置密码，请确保，用户可以重置其两个或三个步骤中而无需启动浏览器或设备上的电子邮件应用。

3. 用户会选取一个选项：

    <img src="images/dynamo_appendix_mo_direct_3_options.png" alt="MO Direct walkthrough: user picks an option" title="MO 直接演练： 用户选取一个选项" width="600" />

    - 显示最重要内容，提供服务，在页面的中心。
    - 徽标和品牌元素位于左上角。
    - 导航按钮位于右下角。
    - 有关可用选项，使用的标题和服务类别的简短说明，使用大磁贴。
    - 可供用户向前导航或退出"下一步"和"取消"按钮。 MO 直接预期服务的数据分类可能包含预付的计划重复执行的每月计划，并将新设备附加到现有的计划。

4. 在用户提交顺序：

    <img src="images/dynamo_appendix_mo_direct_4_submit_order.png" alt="MO Direct walkthrough: user submits an order" title="MO 直接演练： 用户提交订单" width="600" />

    - 页面布局是在所有页面保持一致。 例如，徽标和品牌元素位于左上方，并导航元素位于底部。
    - 服务条款链接必须在网页上可见。
    - 订单确认页列出了用户提交订单，包括数据服务，付款方法的付款等量的详细信息之前查看的关键信息。

5. 如果用户在任何时候取消 MO 直接流：

    <img src="images/dynamo_appendix_mo_direct_5_cancel.png" alt="MO Direct walkthrough: user cancels MO Direct flow" title="MO 直接演练： 用户取消 MO 直接流" width="600" />

    - 通过计划移动应用系统会提示确认对话框中，将保留 MO 直接体验。

6. 完成订单：

    <img src="images/dynamo_appendix_mo_direct_6_order_complete.png" alt="MO Direct walkthrough: order complete" title="MO 直接演练： 订单完成" width="600" />

    - 这将显示事务确认，这是移动运营商门户的一部分的示例。
    - 顺序处理成功，在这种情况下，单击"继续"后应将通知发送到移动计划应用程序与购买结果、 esim 卡激活代码和 API 中所需的其他信息。 用户将自动定向到计划移动应用 PDP （产品详细信息页）。
    - 如果事务是物理的 SIM 卡或活动 esim 卡配置文件已到位，你应激活后端中的计划。
    - 如果事务需要一个新的配置文件，要下载，转到下一步。

7. 正在下载 esim 卡配置文件 （如果适用）：

    <img src="images/dynamo_appendix_mo_direct_7_downloading_esim_profile.png" alt="MO Direct walkthrough: downloading an eSIM profile (if applicable)" title="MO 直接演练： 下载 esim 卡配置文件 （如果适用）" width="600" />

    - 正在下载 esim 卡配置文件。

8. 激活 MO 直接计划：

    <img src="images/dynamo_appendix_mo_direct_8_activated.png" alt="MO Direct walkthrough: MO Direct plan is activated" title="MO 直接演练：激活 MO 直接计划" width="600" />

    - 设备连接。
    - 用户具有活动月直接帐户。

### <a name="hyperlink-experience"></a>超链接体验

如果没有为指向新页面中直接 MO 门户和用户单击超链接，在 web 视图控件将呈现该页面在同一窗口中。 用户必须单击后退按钮以返回到前一页的计划移动应用中。

或者，可能会使用超链接以启动一个对话框，WebView 控件的上下文中。

### <a name="back-button-experience"></a>后退按钮体验

计划移动应用的菜单栏上的后退按钮将导航到上一页的用户就像在 web 浏览器中。 

> [!IMPORTANT]
> 生成 MO 直接门户，因为如果您正在构建购物车体验，如果你想要返回到以前的状态，而不会丢失它们以前输入的任何数据的用户。

<img src="images/dynamo_appendix_mo_direct_9_back_button.png" alt="MO Direct walkthrough: back button example" title="MO 直接演练： 后退按钮示例" width="600" />

### <a name="error-while-loading-the-mo-direct-experience"></a>加载 MO 直接体验时出错

当没有任何未处理的错误或遇到导致计划移动应用程序无法加载 MO 直接 MO 直接门户上的异常时，将显示以下错误：

<img src="images/dynamo_appendix_mo_direct_10_error.png" alt="MO Direct walkthrough: error example" title="MO 直接演练： 错误示例" width="600" />

## <a name="mobile-plans-user-journey"></a>移动计划用户旅程

用户附加到参与计划移动计划移动运营商的 esim 卡支持的 Windows 已连接设备时下, 图显示了旅程。

<img src="images/dynamo_appendix_user_journey.png" alt="Mobile Plans user journey" title="移动计划用户旅程" width="400" />

## <a name="high-level-integration-schedule"></a>高级集成计划

下表提供了移动计划项目集成计划的高级概述。

| 阶段 | 活动 | 所有者 | 估计时间 |
| --- | --- | --- | --- |
| 配置 | 定义 ICCID 范围 | MO | 不适用 |
| 配置 | 提交 COSA 数据库更新 <p>这是为了确保您在 Windows 上的 APN 配置会自动，并且是 Windows 版本中包含的硬截止时间。 在此之前必须配置和验证设置。</p> | MO | 约 2 个月 |
| 配置 | 创建开发人员中心帐户和提交应用程序 | MO | 不适用 |
| 配置 | 白名单 MO 应用和帐户 | MS | 2 天 |
| 配置 | 提供服务配置电子邮件 | MO | 不适用 |
| 配置 | 在开发人员中心中发布元数据包 | MO | 不适用 |
| 实现 | 实现移动运营商的 Api | MO | 不适用 |
| 实现 | 启用的围墙的花园 | MO | 不适用 |
| 实现 | 生成 MO 直接 web 体验 | MO | 不适用 |
| 验证 | MO Api 代码完成 | MO | 不适用 |
| 验证 | 验证 MO API 实现 | MO | 不适用 |
| 集成 | 提供 SIM/esim 卡集成阶段期间要使用的列表 | MO | 1 天 |
| 集成 | 配置 SIM/esim 卡来验证 | MS | 最多 1 周 |
| 集成 | DM PPE 环境中配置 MO API 过渡终结点 | MS | 最多 1 周 |
| 集成 | MO API 测试完成的活动 SIM （检查点） | MS | 2 周 |
| 集成 | MO API 可用于生产 （检查点） | 月 （&AMP; M) | 不适用 |
| 启动 | 提交到数据挖掘的生产月 API 终结点 | MO | 不适用 |
| 启动 | DM PPE 环境中配置 MO API 生产终结点 | MS | 最多 1 周 |
| 启动 | 负载测试 | 月 （&AMP; M) | 1 周 |
| 启动 | 在位置监视和升级路径 | MS | 1 周 |
| 启动 | 使用数据挖掘生产环境中的月 API 生产终结点配置测试 SIM 范围更小 | MS | 最多 1 周 |
| 启动 | 端到端验证 （检查点） | MO | 不适用 |
| 启动 | 转到/无转 （最后一个检查点） | 月 （&AMP; M) | 不适用 |
| 启动 | 使用数据挖掘生产环境中的月 API 生产终结点配置完整 SIM 范围 | MS | 最多 1 周 |
| 启动 | 版本查看启动准备情况 | MS | 2 天 |
| 启动 | 启动 | 月 （&AMP; M) | 不适用 |