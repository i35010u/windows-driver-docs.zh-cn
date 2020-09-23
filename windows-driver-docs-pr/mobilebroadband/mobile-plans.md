---
title: 移动套餐概述
description: 移动套餐概述
ms.assetid: AA432EAE-A89B-4C4C-9539-BC2763091055
keywords:
- Windows Mobile 计划移动运营商
ms.date: 07/31/2019
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: cf7c097aaf9e357afff5fec47460b07dd175d592
ms.sourcegitcommit: e6247811ff9a07070547af3d89705dae33a2f465
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "91026444"
---
# <a name="mobile-plans-overview"></a>移动套餐概述

## <a name="purpose"></a>目的

移动计划是 Windows 10 中的一个应用程序，可帮助最终用户通过移动运营商将其 Windows 设备连接到移动电话网络。 移动计划的目的是：

- 为启用手机网络的 Pc 激活提供一致和简化的用户体验。
- 通过使用 eSIM，启用用于移动电话激活的新渠道
- 通过客户和移动运营商之间的直接关系，提高 Windows 电脑上的移动服务的采用

Windows 10 版本1803及更高版本支持移动计划。

## <a name="customer-journey"></a>客户旅程

典型的移动计划客户旅程由以下步骤组成：

![移动计划客户旅程](images/mobile_plans_customer_journey.png)

步骤 | 说明
------|------------
发现 | 用户在 Windows UI 中看到若干入口点之一，并启动移动计划应用。 Windows Shell 中提供了多个可用于各种方案的入口点。
浏览 & 欢迎 | 启动移动计划应用后，用户会选择其移动运营商，并看到 "操作员网关" 页。 "网关" 页调用用于承载下一步的移动运营商 web 门户。 请注意，某些入口点将用户直接转到操作员网关页。
激活 & 结帐 | 移动运营商 web 门户会指导用户完成登录、激活和签出
合同 | 激活步骤完成后，用户将被设置为数据。 此步骤可能包括下载和激活 eSIM 配置文件。
使用情况 | 用户喜欢一个始终连接的 PC 的优点，并且能够直接在 Windows UI 中查看可用余额。 他们可以轻松返回到移动运营商 web 门户来管理其帐户，并根据需要购买额外的数据。

## <a name="user-experience"></a>用户体验

以下部分说明了移动计划用户体验。

### <a name="launching-the-app"></a>启动应用程序

可以从多个不同的入口点启动移动计划应用。 最常见的入口点是网络飞出，因为用户通常在 Windows 10 中管理其活动网络接口。 可以展开蜂窝接口以显示移动电话网络的状态。 在下面的示例中，设备未激活 SIM 配置文件，因此用户看到对操作的调用以 "与数据计划进行连接"。 选择此链接将启动移动计划应用。

有关网络飞出的行为的详细信息，请参阅 [移动计划帐户管理](mobile-plans-account-management.md) 主题。

![网络飞出已连接](images/network_flyout_get_connected.png)

还可以从 toast 通知启动该应用。 选择 "连接" 按钮将启动移动计划应用。

有关 toast 通知行为的详细信息，请参阅 [移动计划 toast 通知](mobile-plans-notifications.md) 主题。

![Toast 通知升级](images/toast_notification_promotion.png)

也可以从 "设置" 应用程序或 "开始" 菜单中启动移动计划应用程序。

### <a name="select-provider-page"></a>选择提供程序页

启动应用后，用户可以选择其移动运营商。 应用显示基于用户当前位置的可用移动运营商的列表。

有关此页面的详细信息，请参阅 [Mobile plan 操作员目录](mobile-plans-catalog.md) 主题。

![选择提供程序页](images/select_provider_page.png)

### <a name="mobile-operator-gateway-page"></a>移动运营商网关页

如果用户选择了移动运营商，则应用会显示该操作员的 "网关" 页。 此页面由移动计划应用托管。 用户可以选择此按钮以继续。

有关 "网关" 页的行为和自定义的详细信息，请参阅 " [移动计划网关" 页](mobile-plans-gateway.md) 主题。

![移动运营商网关页](images/mobile_operator_gateway_page.png)

### <a name="mobile-operator-web-portal"></a>移动运营商 Web 门户

用户选择该按钮继续后，应用程序将加载移动运营商的 web 门户。 Web 内容显示在应用程序承载的浏览器控件中，用户可以使用 web 导航来浏览门户。

有关移动运营商 web 门户的详细说明，请参阅 [移动运营商 web 门户](mobile-plans-web-portal.md) 主题。

![移动运营商 Web 门户](images/mobile_operator_web_portal.png)

### <a name="fulfillment"></a>合同

在 web 门户上完成注册流后，移动运营商可以根据注册类型触发履单。 这可能包括下载和安装新的 eSIM 配置文件，或者将新的余额添加到活动帐户。 完成执行步骤后，web 门户可以调用弹出窗口，让用户了解该过程已完成。

有关此步骤的详细信息，请参阅 [移动计划回叫通知](mobile-plans-callback-notifications.md) 主题。

![移动运营商履行](images/mobile_operator_activation.png)
