---
title: 开发 SMS 应用程序
description: 开发 SMS 应用程序
ms.assetid: 052eb3cc-4a39-4667-8678-b18650f3b5c9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a557fd4fd86601539752af582208ead05fe5ae2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540441"
---
# <a name="developing-sms-apps"></a>开发 SMS 应用程序


Windows 8、 Windows 8.1 和 Windows 10 UWP 应用到为移动网络运营商，移动宽带卡 Ihv、 Oem 和其合作的软件供应商的应用程序短信访问提供短消息服务 (SMS) 文本消息传递平台。

**请注意**  移动宽带应用要求 SMS 支持时收到短信向最终用户显示通知。 SMS 可能还需要符合法规要求或某些市场中的最佳做法。

 

移动宽带短信平台提供了以下功能：

-   发送和读取 SMS 数据以文本模式还是 PDU 模式 （二进制）

-   筛选的数据上限超额、 漫游，和其他管理 SMS 运营商通知

-   新的短信接收到的后台事件

-   读取和从移动宽带设备消息存储中删除消息

-   获取移动宽带设备的属性

-   短信 API 访问提示

本主题中的部分包括：

-   [移动宽带短信支持设备](#supporteddevices)

-   [移动宽带短信访问](#smsaccess)

-   [筛选的短信通知](#filtering)

-   [开发 SMS 应用](#developsmsapp)

## <a name="span-idsupporteddevicesspanspan-idsupporteddevicesspanspan-idsupporteddevicesspanmobile-broadband-sms-supported-devices"></a><span id="SupportedDevices"></span><span id="supporteddevices"></span><span id="SUPPORTEDDEVICES"></span>移动宽带短信支持设备


下面是有关 SMS 如何处理移动宽带连接概述关系图：

![短信平台概述](images/fig1-mb-sms-platformoverview.jpg)

### <a name="span-idbasreqspanspan-idbasreqspanbasic-requirements"></a><span id="basreq"></span><span id="BASREQ"></span>基本要求

-   必须从移动网络运营商中运行 Windows 8、 Windows 8.1 或 Windows 10 中，移动宽带设备和频繁使用的服务的计算机。

-   设备应放置硬件的认证 Windows 8、 Windows 8.1 或 Windows 10 使用短信发送/接收功能集。

-   支持内部和外部设备。

-   全局系统的移动通信 (GSM)-和码多址访问 (CDMA)-同时支持基于的设备。

### <a name="span-idadditionalguidanceforabetteruserexperiencespanspan-idadditionalguidanceforabetteruserexperiencespanspan-idadditionalguidanceforabetteruserexperiencespanadditional-guidance-for-a-better-user-experience"></a><span id="Additional_guidance_for_a_better_user_experience"></span><span id="additional_guidance_for_a_better_user_experience"></span><span id="ADDITIONAL_GUIDANCE_FOR_A_BETTER_USER_EXPERIENCE"></span>获得更好的用户体验的更多指导

-   可以发送短信或设备处于受支持的运算符的网络覆盖区域时，收到的应用。 设备必须注册到网络服务提供商，但无需连接到数据服务以发送或接收消息。

-   发送或接收短信漫游网络上的数据受到基于移动网络运算符 (MNO) 策略需要支付额外费用。

-   设备不能发送或接收 SMS 数据，如果设备是锁定的 PIN。

## <a name="span-idsmsaccessspanspan-idsmsaccessspanspan-idsmsaccessspanaccess-to-mobile-broadband-sms"></a><span id="SMSAccess"></span><span id="smsaccess"></span><span id="SMSACCESS"></span>移动宽带短信访问


### <a name="span-idstorespanspan-idstorespanuwp-app-access-to-sms"></a><span id="store"></span><span id="STORE"></span>SMS UWP 应用访问权限

对移动宽带短信功能的访问现已推出的以下方法：

-   移动网络运营商可以向用户提供 SMS 功能通过使用移动宽带应用。

-   移动宽带卡生成公开市场移动宽带适配器的 Ihv 可以让移动宽带应用程序访问 SMS。

-   生成嵌入了移动宽带适配器的计算机的 Oem 可以让移动宽带应用程序访问 SMS。

-   UWP 应用可以被赋予特权的访问 SMS 由移动运营商，移动宽带卡 IHV 或 OEM。

在服务元数据或设备元数据中指定了访问权限短信。 设备元数据包是一组特定的设备和其 UWP 设备应用程序之间创建链接的 XML 文件。 链接基于移动宽带卡 IHV 硬件 Id 或计算机硬件的计算机设备容器的 Id 的 oem 必须生成嵌入了移动宽带适配器的计算机。

有关服务元数据的详细信息，请参阅[服务元数据](service-metadata.md)。

移动网络运营和 Ihv、 Windows 8、 Windows 8.1 和 Windows 10 的移动宽带适配器自动下载并安装从 Microsoft Store 的移动宽带应用程序，当用户首次连接其设备时。 在 Windows 8.1 和 Windows 10 的移动宽带应用添加到**所有应用**视图。

移动宽带应用程序和 IHV 应用同时具有访问权限 SMS 单个移动宽带设备。 如果安装了移动宽带应用和 IHV 或 OEM UWP 应用并收到新的短信时同时显示通知用户界面，用户将看到两个通知 Ui。 用户可以关闭通知，或者卸载其中一个应用。

### <a name="span-iduserspanspan-iduserspanuser-consent-to-sms-access"></a><span id="user"></span><span id="USER"></span>短信访问权限的用户同意

移动宽带应用程序必须获得用户同意使用短信，因为发送来自用户的设备的消息可能会导致用户通过其移动电话服务提供商支付发送或接收消息。

用户运行 Windows 8，Windows 8.1 或 Windows 10 可以控制对在应用级别的短信功能的访问通过使用设置超级按钮。

**请注意**  以及用户同意的情况下，应用程序还必须具有访问权限授予设备的设备或服务的元数据中添加应用程序名称。

 

## <a name="span-idfilteringspanspan-idfilteringspanspan-idfilteringspansms-notifications-filtering"></a><span id="Filtering"></span><span id="filtering"></span><span id="FILTERING"></span>筛选的短信通知


移动宽带短信平台新收到短信对数据进行筛选到两种类型： 管理从移动网络运营商 (MNO) 和常规短信的短信通知。 管理 m n O 从收到的短信通知仅移动宽带应用中，可以访问，而隐藏的常规 SMS 客户端应用程序。

Mno 预配 Windows 平台中指定管理的短信通知的自定义筛选的规则。 如果未不指定任何消息筛选规则，短信平台将所有短信都分类为可供任何应用程序的常规短信。

有关通知筛选的详细信息，请参阅[启用移动运营商通知和系统事件](enabling-mobile-operator-notifications-and-system-events.md)。

## <a name="span-iddevelopsmsappspanspan-iddevelopsmsappspanspan-iddevelopsmsappspandeveloping-your-sms-app"></a><span id="DevelopSMSApp"></span><span id="developsmsapp"></span><span id="DEVELOPSMSAPP"></span>开发 SMS 应用


您可以编写 JavaScript 中， C#，或使用 c + + 应用程序[ **Windows.Devices.Sms** ](https://msdn.microsoft.com/library/windows/apps/br206567) API 来发送、 读取和删除消息。

**请注意**   Windows 7 移动宽带短信 API 提供只有低级别的调制解调器接口对于短信。 Windows 8、 Windows 8.1 和 Windows 10 提供适用于常规应用开发的备用文本模式接口。

 

-   [SMS 设备存储限制](sms-device-storage-limits.md)

-   [枚举短信设备](enumerate-sms-devices.md)

-   [获取短信设备信息](get-sms-device-information.md)

-   [使用文本模式界面读取收到的短信](read-received-sms-by-using-the-text-mode-interface.md)

-   [运行短信接收到的新后台事件](run-new-sms-received-background-events.md)

-   [通过使用自定义字符集发送短信](send-sms-by-using-custom-character-sets.md)

-   [使用文本模式界面发送短信](send-sms-by-using-the-text-mode-interface.md)

-   [集 SMS 声明](set-sms-declarations.md)

 

 





