---
title: 移动计划通知
description: 本主题介绍如何在移动计划中配置 toast 通知。
ms.assetid: 20A59FB6-9EEF-4B55-940C-79B6FB2C99CA
keywords:
- Windows Mobile 计划 toast 通知
ms.date: 06/11/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5ec0c8a22ed1c91e08210cc6c3ee56a3bb6595bf
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207349"
---
# <a name="mobile-plans-notifications"></a>移动计划通知

## <a name="overview"></a>概述

本主题介绍移动计划中的 toast 通知，mobile 运营商可以使用文本和图像自定义这些通知，以便与最终用户进行通信。 移动计划通知基于 [Windows 10 中的 toast 通知框架](/windows/uwp/design/shell/tiles-and-notifications/adaptive-interactive-toasts)。

> [!Note]
> 在计划使用此功能之前，请联系你的 Microsoft 联系人。

移动计划应用支持显示两种不同类型的 toast 通知： SMS 触发和应用触发。

## <a name="sms-triggered-notifications"></a>SMS 触发的通知

移动运营商可以通过向设备发送短信来触发要显示在用户设备上的通知。 SMS 正文包含一个字符串标识符，该标识符将消息路由到移动计划应用，并触发通知的显示。 单击此 <accept> 按钮将启动移动计划应用，并显示移动运营商的 " [网关" 页](mobile-plans-gateway.md)。

由于移动运营商通过短信触发通知，因此设备必须具有活动配置文件，并在移动电话网络上注册才能接收短信。 设备还必须对移动计划服务进行数据访问，以便请求通知内容。

### <a name="sms-triggered-notification-content"></a>SMS 触发通知内容

移动运营商可以使用具有预定义元素的模板自定义通知内容。 以下突出显示的元素由移动运算符定义。

![SMS 通知模板](images/mobile_plans_sms_notification_template.png)

字段名称 | 说明 | 示例
---------- | ----------- | -------
通知类型 | 支持几种预定义的 SMS 通知类型。 每种类型的行为相同。 只有和按钮显示的字符串会根据 <accept> <decline> 类型的不同而变化。 | 低余额、零余额、新产品/服务、试用产品/服务、试用版、试用版
标题 | 调用操作的一行 | "您的数据即将用完"
Body | 将产品/服务值突出显示给最终用户的简短消息 | "当前数据计划的剩余时间小于5MB。 请立即采取措施以确保保持连接状态。 "
映像 | 使用 PC 作为成为的生活方式照片。 图像尺寸在 100% 缩放时为 364x180 像素。 | https://picsum.photos/id/1/364/180
徽标 | 这是在载入过程中提供的资产的一部分 | 

### <a name="sample-sms-triggered-notification"></a>SMS 触发通知示例

![SMS 通知示例](images/mobile_plans_sms_notification_sample.png)

### <a name="using-multiple-notification-templates"></a>使用多个通知模板

移动运营商可以选择定义多个 SMS 通知模板。 如果完成此操作，移动计划服务将在运行时调用移动运营商 API，以请求用于通知的模板的 ID。

由于请求包含设备上活动配置文件的标识符，因此移动运营商可以为不同的用户段或 A/B 测试定义多个模板。 SMS-通知还可与移动计划应用中显示的 [增强网关页面](mobile-plans-gateway.md#enhanced-gateway-page) 结合，以创建高度针对性的 campaings。

获取通知请求会返回要用于向用户显示的通知的模板 ID。

![移动计划获取通知 Callflow](images/mobile_plans_get_notifications_callflow.png)


### <a name="getnotifications-api-specification"></a>GetNotifications API 规范
`GetOffers`移动计划应用程序收到 SMS 消息后，将调用 API。 移动计划服务是此请求的代理。

```HTTP
GET https://{notificationUri}sims/{simmri}/notifications
```

- 在移动运营商的服务配置过程中， *{notificationUri}* 是 notificationUri 值载入。

终结点有三个查询参数：
- "*限制*" 是必需的，指定要返回的通知数。
- *imei*是可选的，它指定客户端的 imei。
- *notificationType*，这是必需的，它指定要返回的通知的类型。 *NotificationType*参数始终是移动计划的 GET 通知请求所接受的枚举字符串之一。

响应是一个 JSON 对象，其中包含一个名为 " *通知* " 的属性，其中包含一系列通知。 此列表中的通知数最多 *限制* 请求。 此列表中的每个通知都是一个对象，该对象具有单个属性 *notificationId*，该属性必须标识移动运营商的服务配置中的现有通知。

下面是使用此终结点进行交互的示例：

```HTTP
GET https://moendpoint.com/v1/sims/iccid:8988247000100003319/notifications?notificationType=lowBalance&limit=1&imei=1234
X-MS-DM-TransactionId: "MSFT-12345678-1234-1234-1234-123456789abc"

HTTP/1.1 200 OK
Content-type: application/json
X-MS-DM-TransactionId: "MSFT-12345678-1234-1234-1234-123456789abc"
{
  "notifications": [
    {
      "notificationId": 1,
      "notificationType": "lowBalance"
    }
  ]
}
```

## <a name="app-triggered-notifications"></a>应用触发的通知

某些市场中的移动运营商还可以在未安装 eSIM 配置文件的已启用 eSIM 的 Windows 10 电脑上显示促销通知。 用户在全新体验中完成设备的安装后，不久就会触发促销通知。 单击此 <accept> 按钮将启动移动计划应用，并显示移动运营商的 " [网关" 页](mobile-plans-gateway.md)。

### <a name="app-triggered-notification-content"></a>应用触发通知内容

移动运营商可以使用具有预定义元素的模板自定义促销通知内容。 以下突出显示的元素由移动运算符定义。

![促销通知模板](images/mobile_plans_promo_notification_template.png)

字段名称 | 说明 | 示例
---------- | ----------- | -------
标题 | 调用操作的一行 | "激活免费试用版"
Body | 将产品/服务值突出显示给最终用户的简短消息 | "获取30GB 的可用数据，因此您可以保持与任何地方的连接。"
映像 | 使用 PC 作为成为的生活方式照片。 图像尺寸为100% 缩放时的360x243 像素。 | https://picsum.photos/id/1/360/234
徽标 | 这是在载入过程中提供的资产的一部分 | 

[通知可视化工具应用](https://www.microsoft.com/store/productId/9NBLGGH5XSL1)可用于原型和测试通知内容。

### <a name="sample-app-triggered-notification"></a>示例应用触发的通知

![移动计划通知示例](images/mobile_plans_notifications.png)