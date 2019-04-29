---
title: WindowsMime 协议
description: WindowsMime 协议
ms.assetid: 03C5A31F-269A-45B3-9359-B6FFF4823190
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f8aaf09f59956fea80fd3fece13b8c072dadef8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373587"
---
# <a name="windowsmime-protocol"></a>WindowsMime 协议


## <a name="windowsmime-subscriptions"></a>"WindowsMime"订阅


"WindowsMime"订阅是一种提取所有可能的 MIME 类型负载的订阅。 Windows 订阅以向驱动程序注册 Windows 兴趣接收 MIME 类型化数据，用户可能感兴趣使用此类型。 由于这是所有可能的 MIME 类型负载的订阅，则驱动程序必须返回类型，以及有效负载。

### <a name="required-actions"></a>所需的操作

-   作为 ASCII 编码，并且以 NULL 结尾的字符串中的输出缓冲区的前 256 个字节，则驱动程序必须返回有效负载的 MIME 类型。
-   输出缓冲区的前 256 字节之后，驱动程序必须返回消息负载。
-   该驱动程序必须设置的信息字段的已完成的 IRP 为 256 +**sizeof**（有效负载）。
-   如果邻近技术公布为 NFC，驱动程序必须匹配与具有 0x02 TNF 字段值的所有 NDEF 消息"WindowsMime"的订阅。
    -   该驱动程序必须返回到此类型的订阅服务器仅匹配 NDEF 消息的有效负载。
    -   驱动程序都不能返回到此类型的订阅服务器的完整编码的 NDEF 消息。
-   提供程序可能支持其他兼容的方案。

## <a name="windowsmime-protocol"></a>"WindowsMime。" 协议


"WindowsMime。" 发布是一种只需发布到对等设备的 MIME 类型的有效负载。 "WindowsMime。" 订阅是一种订阅于与特定的 MIME 类型的负载。 Windows 将向近程设备时用户定向为此，发布一个简单的 MIME 类型化消息。

一般示例类型："WindowsMime。&lt;SomeMimeType&gt;"

具体的示例类型：“WindowsMime.image/jpeg”

### <a name="required-actions"></a>所需的操作

-   如果邻近技术公布为 NFC，则该驱动程序必须与匹配订阅"WindowsMime。&lt;SomeMimeType&gt;"仅与接收的 NDEF 消息 0x02 TNF 字段值和具有匹配的类型字段"&lt;SomeMimeType&gt;"中指定的等效性规则基于\[NDEF\]。

    该驱动程序必须返回到此类型的订阅服务器仅的各个匹配 NDEF 消息有效负载。

-   如果邻近技术公布为 NFC，然后该驱动程序必须将封装每个"WindowsMime。&lt;SomeSubType&gt;"NDEF 中的发布消息的 0x02 TNF 字段值。
    -   NDEF 类型字段必须包含的直接映射&lt;SomeSubType&gt;其中每个宽字符被解释为一个字节的字符串。
    -   NDEF 有效负载必须包含发布消息负载的直接二进制内容。

## <a name="windowsmimewritetag-publications"></a>"WindowsMime:WriteTag。" 发布


"WindowsMime:WriteTag。" 发布是用于只是写入到一个标记的 MIME 类型的有效负载的应用的方式。

### <a name="required-actions"></a>所需的操作

-   常见"\*: WriteTag"其他部分所述的要求适用。
-   "WindowsMime。&lt;SomeMimeType&gt;"发布要求其他部分的说明适用于"WindowsMime:WriteTag。&lt;SomeMimeType&gt;"发布。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[邻近 DDI 引用附近](https://msdn.microsoft.com/library/windows/hardware/jj866056)  

