---
title: 移动计划常规附录
description: 本主题介绍了移动计划计划的附录信息。
ms.assetid: B3B478DB-78F4-4031-B041-DCBAACC15D6F
keywords:
- Windows Mobile 计划附录，移动计划附录移动运营商
ms.date: 07/05/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0a1af5c5101a1493efedce5339a32495e632aa50
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242744"
---
# <a name="mobile-plans-general-appendix"></a>移动计划常规附录

## <a name="web-portal-flow-and-reference-design"></a>Web 门户流和引用设计

此参考设计是一个模板，您可以对其进行更改以最好地表示您的品牌和产品。 此参考设计显示了建议的 UX 设计，其中包含导航元素、品牌位置和网站功能。

### <a name="mo-direct-reference-site-walkthrough"></a>MO 直接引用站点演练

1. 用户单击 "继续" 按钮：

    <img src="images/dynamo_appendix_mo_direct_1_continue.png" alt="MO Direct walkthrough: user clicks on the continue button" title="MO 直接演练：用户单击 "继续" 按钮" width="600" />

    - 移动计划应用会提示此对话框。

2. 用户输入 MO 直接门户并通过其 MO 帐户登录：

    <img src="images/dynamo_appendix_mo_direct_2_sign_in.png" alt="MO Direct walkthrough: user enters MO Direct portal and signs in with their MO account" title="MO Direct 演练：用户输入 MO Direct 门户并以 MO 帐户登录" width="600" />

    - 页面布局在所有页面中都是一致的。 例如，徽标和品牌元素位于左上角，导航元素位于底部。
    - 登录页可以链接到注册新帐户。
    - "忘记密码" 是可选的。 请注意，用户在围墙菜园中，只有移动计划应用可以访问 internet。 如果希望通过 MO Direct 门户支持密码重置，请确保用户可以在两个或三个步骤中将其重置，而无需在设备上启动浏览器或电子邮件应用。

3. 用户选择一个选项：

    <img src="images/dynamo_appendix_mo_direct_3_options.png" alt="MO Direct walkthrough: user picks an option" title="MO 直接演练：用户选择一个选项" width="600" />

    - 在页面的中心提供最重要的内容 "可用服务"。
    - 徽标和品牌元素位于左上角。
    - 导航按钮位于右下角。
    - 对可用选项使用大磁贴，其中包含服务类别的标题和简短说明。
    - 用户可以通过 "下一步" 和 "取消" 按钮向前或向后导航。 MO Direct 预期数据服务类别可能包括预付计划、定期每月计划，以及将新设备附加到现有计划。

4. 用户提交订单：

    <img src="images/dynamo_appendix_mo_direct_4_submit_order.png" alt="MO Direct walkthrough: user submits an order" title="MO 直接演练：用户提交订单" width="600" />

    - 页面布局在所有页面中都是一致的。 例如，徽标和品牌元素位于左上角，导航元素位于底部。
    - 服务条款链接必须在网页上可见。
    - "订单确认" 页列出了用户在提交订单之前要查看的重要信息，包括有关数据服务、付款方式、付款量等的详细信息。

5. 如果用户随时取消 MO 直接流：

    <img src="images/dynamo_appendix_mo_direct_5_cancel.png" alt="MO Direct walkthrough: user cancels MO Direct flow" title="MO 直接演练：用户取消 MO 直接流" width="600" />

    - 移动计划应用程序会提示保留 MO 直接体验的确认对话框。

6. 订单已完成：

    <img src="images/dynamo_appendix_mo_direct_6_order_complete.png" alt="MO Direct walkthrough: order complete" title="MO 直接演练：订单完成" width="600" />

    - 这会显示一个事务确认示例，它是移动运营商门户的一部分。
    - 成功处理该订单后，在这种情况下，单击 "继续" 后，应将通知发布到带有购买结果、eSIM 激活代码和 API 中所需的其他信息的移动计划应用。 用户将自动重定向到移动计划应用 PDP （产品详细信息页）。
    - 如果事务适用于物理 SIM 卡或活动 eSIM 配置文件已准备就绪，则应在后端激活该计划。
    - 如果事务需要下载新的配置文件，请转到下一步。

7. 下载 eSIM 配置文件（如果适用）：

    <img src="images/dynamo_appendix_mo_direct_7_downloading_esim_profile.png" alt="MO Direct walkthrough: downloading an eSIM profile (if applicable)" title="MO 直接演练：下载 eSIM 配置文件（如果适用）" width="600" />

    - 正在下载 eSIM 配置文件。

8. 已激活 MO 直接计划：

    <img src="images/dynamo_appendix_mo_direct_8_activated.png" alt="MO Direct walkthrough: MO Direct plan is activated" title="MO 直接演练：已激活 MO 直接计划" width="600" />

    - 设备已连接。
    - 用户具有活动的 MO 直接帐户。

### <a name="hyperlink-experience"></a>超链接体验

如果某个超链接指向 MO Direct 门户中的新页面，并且用户单击它，则 web 视图控件将在同一窗口中呈现该页面。 用户必须单击移动计划应用中的 "后退" 按钮，才能返回到上一页。

或者，您可以使用超链接在 Web 视图控件的上下文中启动对话框。

### <a name="back-button-experience"></a>后退按钮体验

移动计划应用菜单栏上的 "后退" 按钮会将用户导航到上一页，就像在 web 浏览器中一样。 

> [!IMPORTANT]
> 如果希望用户恢复到以前的状态，而不会丢失输入的任何数据，则可以构建 MO 直接门户，就像生成购物车体验一样。

<img src="images/dynamo_appendix_mo_direct_9_back_button.png" alt="MO Direct walkthrough: back button example" title="MO 直接演练：后退按钮示例" width="600" />

### <a name="error-while-loading-the-mo-direct-experience"></a>加载 MO 直接体验时出错

当 MO 直接门户上出现任何导致移动计划应用无法加载 MO 直接体验的未处理错误或异常时，将显示以下错误：

<img src="images/dynamo_appendix_mo_direct_10_error.png" alt="MO Direct walkthrough: error example" title="MO Direct 演练：错误示例" width="600" />

## <a name="high-level-integration-schedule"></a>高级集成计划

下表提供了*移动计划*项目集成计划的高级概述。

| 阶段 | 活动 | 所有者 | 估计时间 |
| --- | --- | --- | --- |
| 实现 | eSIM 配置文件可在 Windows 设备上安装。 使用 SMDP + 进行测试，用于过渡环境和生产环境。 | MO |  |
|                | 提供载入清单文档，包括过渡环境服务配置 | MO |  |
|                | 在*移动计划*过渡环境中启用移动运营商过渡环境 | MSFT | 每个月的第一个和第三个星期五发生了配置更新 |
|                | 提交 COSA 数据库更新 | MO | 大约3个月 |
|                | MO 直接门户开发入门 |  |
|                | `GetBalance` API 开发入门 |  |
| Integration | 启用围墙园 | MO |  |
|             | 验证 COSA 更新 | MO |  |
|             | MO 直接门户开发完成 | MO |  |
|             | `GetBalance` API 开发完成 | MO |  |
|             | MO 开发完成-代码完成（检查点） | MO |  |
|             | 验证 `GetBalance` API 功能 | MO |  |
|             | MO 过渡环境（检查点）中的端到端体验功能 | MO |  |
|             | 更新服务配置文档以反映生产环境设置（如果以前未提供） | MO |  |
|             | 提供 Iccid 用于 `GetBalance` 负载测试 | MO |  |
|             | 在*移动计划*过渡环境中启用移动运营商生产环境环境 | MSFT | 每个月的第一个和第三个星期五发生了配置更新 |
|             | MO 生产环境（检查点）中的端到端体验功能 | MO |  |
| 验证 | 出口标准测试用例数完成 | MO |  |
|           | 验证测试用例结果 | MSFT |  |
|           | 测试签名（检查点） | MSFT |  |
| 推广 | `GetBalance` API 负载测试 | MSFT 和 MO | 1 周 |
|         | 就地监视和升级路径 | MSFT | 1 周 |
|         | 就地客户支持 | MSFT 和 MO |  |
|         | 已完成商业协议 | MO |  |
|         | Windows 中可用的 COSA 更新 | MSFT |  |
|         | 开始/不操作（最终检查点） | MSFT 和 MO |  |
|         | 在*移动计划*生产环境中配置 MO 生产环境环境 | MSFT |  |
|         | 从 | MSFT 和 MO | 必须同意启动日期和时间以确保发生本地验证 |