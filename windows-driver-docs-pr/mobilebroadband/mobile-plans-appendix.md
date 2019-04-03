---
title: 移动计划附录
description: 本主题介绍附录移动计划程序的信息。
ms.assetid: B3B478DB-78F4-4031-B041-DCBAACC15D6F
keywords:
- Windows Mobile 计划附录，移动计划附录移动运算符
ms.date: 03/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0451a6ad8243ed59e7209edfcdf09d8c5d042471
ms.sourcegitcommit: 1a1a78575e89bf8cd713bf1dac8a698db3cddfe2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2019
ms.locfileid: "58845537"
---
# <a name="mobile-plans-appendix"></a>移动计划附录

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

## <a name="high-level-integration-schedule"></a>高级别集成计划

下表提供了高级概述*移动计划*项目集成计划。

| 阶段 | 活动 | 所有者 | 估计时间 |
| --- | --- | --- | --- |
| 实现 | esim 卡配置文件可在 Windows 设备上安装。 使用 SMDP + 用于暂存环境与生产环境进行测试。 | MO |  |
|                | 提供载入清单文档，包括过渡环境服务配置 | MO |  |
|                | 启用移动运营商过渡环境中*移动计划*过渡环境 | MSFT | 在每个月的第一个和第三个星期五发生配置更新 |
|                | 提交 COSA 数据库更新 | MO | 大约 3 个月 |
|                | MO 直接门户开发入门 |  |
|                | `GetBalance` API 开发入门 |  |
| 集成 | 启用的围墙的花园 | MO |  |
|             | 验证 COSA 更新 | MO |  |
|             | MO 直接门户开发完成 | MO |  |
|             | `GetBalance` 完整的 API 开发 | MO |  |
|             | MO 开发完整的代码完成 （检查点） | MO |  |
|             | 验证`GetBalance`API 功能 | MO |  |
|             | 端到端体验是月暂存环境 （检查点） 中的功能 | MO |  |
|             | 更新服务配置记录以反映生产环境设置 （如果未提供以前） | MO |  |
|             | 提供 ICCIDs 用于`GetBalance`负载测试 | MO |  |
|             | 移动运营商生产环境中的新环境中实现了*移动计划*过渡环境 | MSFT | 在每个月的第一个和第三个星期五发生配置更新 |
|             | 端到端体验是月生产环境 （检查点） 中的功能 | MO |  |
| 验证 | 退出条件的测试用例完成 | MO |  |
|           | 验证测试用例结果 | MSFT |  |
|           | 测试签字认可 （检查点） | MSFT |  |
| 推出 | `GetBalance` 负载测试 API | MSFT 和 MO | 1 周 |
|         | 在位置监视和升级路径 | MSFT | 1 周 |
|         | 在位置的客户支持 | MSFT 和 MO |  |
|         | 已完成的商业协议 | MO |  |
|         | 在 Windows 中可用的 COSA 更新 | MSFT |  |
|         | 转到/不可行 （最后一个检查点） | MSFT 和 MO |  |
|         | MO 生产环境中配置环境*移动计划*生产环境 | MSFT |  |
|         | 启动 | MSFT 和 MO | 启动日期和时间必须同意以确保执行本地验证 |