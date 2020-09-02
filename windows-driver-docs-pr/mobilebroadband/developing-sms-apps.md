---
title: 开发短信应用程序的简介
description: 开发短信应用程序的简介
ms.assetid: 052eb3cc-4a39-4667-8678-b18650f3b5c9
ms.date: 07/05/2019
ms.localizationpriority: medium
ms.openlocfilehash: b89acf58b507e39fd6468279d973b1e9c93d8d28
ms.sourcegitcommit: 7e4d9508198a30bdc1cb6eda83852dda4e42213e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89304286"
---
# <a name="introduction-to-developing-sms-apps"></a>开发短信应用程序的简介


Windows 8、Windows 8.1 和 Windows 10 提供短消息服务， (SMS) 文本消息传递平台，用于移动网络操作员、移动宽带适配器 Ihv、Oem 以及其合作软件供应商的应用，并将 SMS 访问到 UWP 应用。

**注意**   移动宽带应用要求在收到短信时向最终用户显示通知。 还可能需要 SMS 来符合特定市场的法规要求或最佳做法。

 

移动宽带 SMS 平台提供以下功能：

-   在文本模式或 PDU 模式下发送和读取 SMS 数据 (二进制) 

-   筛选数据上限超额、漫游和其他管理 SMS 操作员通知

-   新的 SMS 接收了后台事件

-   从移动宽带设备消息存储中读取和删除邮件

-   获取移动宽带设备的属性

-   SMS API 访问提示

本主题中的部分包括：

-   [移动宽带 SMS 支持的设备](#supporteddevices)

-   [访问移动宽带短信](#smsaccess)

-   [SMS 通知筛选](#filtering)

-   [开发 SMS 应用](#developsmsapp)

## <a name="span-idsupporteddevicesspanspan-idsupporteddevicesspanspan-idsupporteddevicesspanmobile-broadband-sms-supported-devices"></a><span id="SupportedDevices"></span><span id="supporteddevices"></span><span id="SUPPORTEDDEVICES"></span>移动宽带 SMS 支持的设备


下面是有关 SMS 如何使用移动宽带连接的概述示意图：

![sms 平台概述](images/fig1-mb-sms-platformoverview.jpg)

### <a name="span-idbasreqspanspan-idbasreqspanbasic-requirements"></a><span id="basreq"></span><span id="BASREQ"></span>基本要求

-   此计算机必须运行 Windows 8、Windows 8.1 或 Windows 10、移动宽带设备以及来自移动网络操作员的活动服务。

-   设备应对 Windows 8、Windows 8.1 或 Windows 10 进行硬件认证，并设置了 SMS 发送/接收功能。

-   支持内部和外部设备。

-   移动通信的全球系统 (GSM) -和代码划分多个访问 (CDMA) 基于的设备都受支持。

### <a name="span-idadditional_guidance_for_a_better_user_experiencespanspan-idadditional_guidance_for_a_better_user_experiencespanspan-idadditional_guidance_for_a_better_user_experiencespanadditional-guidance-for-a-better-user-experience"></a><span id="Additional_guidance_for_a_better_user_experience"></span><span id="additional_guidance_for_a_better_user_experience"></span><span id="ADDITIONAL_GUIDANCE_FOR_A_BETTER_USER_EXPERIENCE"></span>更好的用户体验的其他指南

-   当设备处于受支持的操作员的网络覆盖区域时，应用程序可以发送或接收短信。 设备必须注册到网络服务提供商，但不需要连接到数据服务来发送或接收消息。

-   在漫游网络中发送或接收 SMS 数据时，根据移动网络运营商 (o) 策略，需要支付额外的费用。

-   如果设备处于 PIN 锁定状态，则设备无法发送或接收短信数据。

## <a name="span-idsmsaccessspanspan-idsmsaccessspanspan-idsmsaccessspanaccess-to-mobile-broadband-sms"></a><span id="SMSAccess"></span><span id="smsaccess"></span><span id="SMSACCESS"></span>访问移动宽带短信


### <a name="span-idstorespanspan-idstorespanuwp-app-access-to-sms"></a><span id="store"></span><span id="STORE"></span>UWP 应用对短信的访问

可以通过以下方式访问移动宽带短信功能：

-   移动网络运营商可以使用移动宽带应用为用户提供短信功能。

-   构建开放式市场移动宽带适配器的移动宽带适配器 Ihv 可以使移动宽带应用访问短信。

-   构建具有嵌入移动宽带适配器的计算机的 Oem 可以启用移动宽带应用来访问 SMS。

-   可以通过移动运营商、移动宽带适配器 IHV 或 OEM 授予 UWP 应用对短信的特权访问权限。

服务元数据或设备元数据中指定了对短信的访问。 设备元数据包是一组 XML 文件，用于创建特定设备与其 UWP 设备应用之间的链接。 该链接基于 IHV 移动宽带适配器的 HardwareId，或用于构建具有嵌入移动宽带适配器的计算机的 Oem 的计算机设备容器的计算机硬件 Id。

有关服务元数据的详细信息，请参阅 [服务元数据](service-metadata.md)。

对于移动网络操作员和移动宽带适配器 Ihv，Windows 8、Windows 8.1 和 Windows 10 会在用户首次连接其设备时，自动从 Microsoft Store 下载并安装移动宽带应用。 在 Windows 8.1 和 Windows 10 中，移动宽带应用会添加到 " **所有应用** " 视图。

移动宽带应用和 IHV 应用对单个移动宽带设备具有同时访问的短信。 如果移动宽带应用和 IHV 或 OEM UWP 应用都已安装，并且在收到新的短信时显示通知用户界面，则用户会看到两个通知 Ui。 用户可以关闭通知或卸载其中一个应用。

### <a name="span-iduserspanspan-iduserspanuser-consent-to-sms-access"></a><span id="user"></span><span id="USER"></span>用户同意使用短信

移动宽带应用必须获得用户许可才能使用短信，因为从用户的设备发送消息会导致用户通过手机网络服务提供商发送或接收消息。

运行 Windows 8、Windows 8.1 或 Windows 10 的用户可以通过使用 "设置" 超级按钮，在应用级别控制对 SMS 功能的访问。

**注意**   与用户许可一起使用时，应用程序还必须通过在设备或服务元数据中添加应用程序名称来授予访问权限。

 

## <a name="span-idfilteringspanspan-idfilteringspanspan-idfilteringspansms-notifications-filtering"></a><span id="Filtering"></span><span id="filtering"></span><span id="FILTERING"></span>SMS 通知筛选


移动宽带 SMS 平台筛选新接收的 SMS 数据到两种类型：来自移动网络操作员的管理短信通知 (o) 和常规 SMS 消息。 从 o 接收的管理短信通知只能访问移动宽带应用，并且不会从常规 SMS 客户端应用中隐藏。

Mno 为 Windows 预配平台中的管理短信通知指定自定义筛选规则。 如果未指定消息筛选规则，则 SMS 平台会将所有 SMS 消息分类为适用于任何应用程序的常规 SMS 消息。

有关通知筛选的详细信息，请参阅 [启用移动运营商通知和系统事件](enabling-mobile-operator-notifications-and-system-events.md)。

## <a name="span-iddevelopsmsappspanspan-iddevelopsmsappspanspan-iddevelopsmsappspandeveloping-your-sms-app"></a><span id="DevelopSMSApp"></span><span id="developsmsapp"></span><span id="DEVELOPSMSAPP"></span>开发 SMS 应用


您可以编写使用 [**Windows. Sms**](/uwp/api/Windows.Devices.Sms) API 发送、读取和删除消息的 JavaScript、c # 或 c + + 应用程序。

**注意**   Windows 7 Mobile 宽带 SMS API 只为 SMS 提供低级别的调制解调器接口。 Windows 8、Windows 8.1 和 Windows 10 提供适用于常规应用程序开发的备用文本模式接口。

 

-   [短信设备存储限制](sms-device-storage-limits.md)

-   [枚举短信设备](enumerate-sms-devices.md)

-   [获取短信设备信息](get-sms-device-information.md)

-   [使用文本模式界面读取收到的短信](read-received-sms-by-using-the-text-mode-interface.md)

-   [运行收到短信后的新后台事件](run-new-sms-received-background-events.md)

-   [使用自定义字符集发送短信](send-sms-by-using-custom-character-sets.md)

-   [使用文本模式界面发送短信](calculate-characters-and-segments-of-a-draft-sms.md)

-   [设置短信声明](set-sms-declarations.md)

 

