---
title: WindowsMime 协议
description: WindowsMime 协议
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 074d61ce0dda4bcdd062b0b05bd58d445e574729
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97091014"
---
# <a name="windowsmime-protocol"></a>WindowsMime 协议


## <a name="windowsmime-subscriptions"></a>"WindowsMime" 订阅


"WindowsMime" 订阅是一种为所有可能的 MIME 类型的负载抽象订阅的方法。 Windows 订阅此类型是为了向 Windows 要接收用户可能想要使用的 MIME 类型化数据的驱动程序注册。 由于这是针对所有可能的 MIME 类型的有效负载的订阅，因此驱动程序必须返回类型以及负载。

### <a name="required-actions"></a>必需的措施

-   驱动程序必须将有效负载的 MIME 类型作为 ASCII 编码且以 NULL 结尾的字符串返回到输出缓冲区的前256个字节内。
-   驱动程序必须在输出缓冲区的前256字节后返回消息负载。
-   驱动程序必须将已完成 IRP 的信息字段设置为 256 +**sizeof** (负载) 。
-   如果邻近技术被播发为 NFC，则驱动程序必须将 "WindowsMime" 的订阅与具有 TNF 字段值0x02 的所有 NDEF 消息匹配。
    -   驱动程序必须仅将匹配的 NDEF 消息的负载返回到此类型的订阅服务器。
    -   驱动程序不得将完整编码的 NDEF 消息返回到此类型的订阅服务器。
-   提供程序还可以支持其他兼容方案。

## <a name="windowsmime-protocol"></a>"WindowsMime." 协议


"WindowsMime"。 发布是将 MIME 类型的负载发布到对等设备的一种方法。 "WindowsMime"。 订阅是一种订阅负载特定 MIME 类型的方式。 当用户指导你执行此操作时，Windows 将向近程设备发布简单的 MIME 类型的消息。

泛型示例类型： "WindowsMime"。 &lt;SomeMimeType &gt; "

具体示例类型： "WindowsMime/jpeg"

### <a name="required-actions"></a>必需的措施

-   如果近程技术被播发为 NFC，则驱动程序必须与 "WindowsMime" 的订阅匹配。 &lt;&gt;"SomeMimeType" 仅具有 TNF 字段值为0x02 并且具有与 "SomeMimeType" 匹配的类型字段（ &lt; &gt; 基于 NDEF 中指定的等效规则）的已接收 NDEF \[ 消息 \] 。

    驱动程序必须仅将单个匹配的 NDEF 消息的负载返回到此类型的订阅服务器。

-   如果近程技术被播发为 NFC，则驱动程序必须将每个 "WindowsMime" 封装。 &lt;SomeSubType &gt; "NDEF 消息中的发布，TNF 字段值为0x02。
    -   NDEF TYPE 字段必须包含 SomeSubType 字符串的直接映射 &lt; &gt; ，其中每个宽字符被解释为单字节。
    -   NDEF 负载必须包含发布消息负载的直接二进制内容。

## <a name="windowsmimewritetag-publications"></a>"WindowsMime:WriteTag." 发布


"WindowsMime： WriteTag"。 发布是一种应用程序，只需将 MIME 类型的负载写入标记。

### <a name="required-actions"></a>必需的措施

-   \*其他地方所述的常见 "： WriteTag" 要求适用。
-   "WindowsMime"。 &lt;SomeMimeType &gt; "其他地方所述的发布要求适用于" WindowsMime： WriteTag。 &lt;SomeMimeType &gt; "发布。

 

 
## <a name="related-topics"></a>相关主题
[近现场通信 (NFC) API 参考](/windows-hardware/drivers/ddi/_nfpdrivers/)
