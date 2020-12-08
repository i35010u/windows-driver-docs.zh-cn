---
title: Windows 协议
description: Windows 协议
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c05059791954d0da5d53a800ea3eb5f00f25c94c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812685"
---
# <a name="windows-protocol"></a>Windows 协议


为了确保启用了 NFC 的 NFP 提供程序的互操作性，本部分准确定义了如何在 NDEF 消息中封装 Windows 消息。 本节还将 NFP 发布/订阅模型映射到已发布的 NFC 论坛协议，以交换 NDEF 消息。 仅当邻近技术被播发为 NFC 时，这些要求才适用。

## <a name="encapsulation"></a>封装


必须满足以下要求才能确保适当的 Windows 消息封装以便 NFC 互操作性。

### <a name="required-actions"></a>必需的措施

-   如果近程技术被播发为 NFC，则驱动程序必须将每个 "Windows" 封装。 &lt;SomeSubType &gt; "TNF 字段值为0x03 的 NDEF 消息中的发布。
    -   NDEF TYPE 字段必须包含 SomeSubType 字符串的直接映射 &lt; &gt; ，其中每个宽字符被解释为单字节。
    -   NDEF 负载必须包含发布消息负载的直接二进制内容。
-   如果近程技术被播发为 NFC，则驱动程序必须与 "Windows" 的订阅匹配。 &lt;SomeSubType &gt; "只包含 TNF 字段值为0x03 的 NDEF 消息和一个等于" SomeSubType "的类型字段， &lt; &gt; 其中每个宽字符被解释为单字节

    驱动程序必须仅将匹配的 NDEF 消息的负载返回到此类型的订阅服务器。

## <a name="windowswritetag-publications"></a>"Windows： WriteTag"。 发布


"Windows： WriteTag"。 发布是一种应用程序，只需将 Windows 类型的负载写入标记。

### <a name="required-actions"></a>必需的措施

-   \*其他地方所述的常见 "： WriteTag" 要求适用。
-   "Windows. &lt;SomeSubType &gt; "发布要求也适用于" Windows： WriteTag。 &lt;SomeSubType &gt; "发布。

## <a name="launchappwritetag-publications"></a>"LaunchApp： WriteTag" 发布


"LaunchApp： WriteTag" 发布是一种方法，用于将 "Windows.windows.com/LaunchApp" 消息直接写入标记。

客户端将发送制表符分隔 (或以 null 分隔的字符串) 列表作为此发布的有效负载编码在 UTF-16LE 中。 第一个字符串是应用程序的参数列表。 后面的参数字符串将是字符串对。 每个对中的第一个字符串定义应用程序 ID 的平台限定符，下一个字符串是要在该平台上启动的实际应用程序 ID。 此机制支持跨 Windows 以外的应用程序平台之间的互操作性。

### <a name="required-actions"></a>必需的措施

-   必须将消息的类型编码为 "Windows.windows.com/LaunchApp"。
-   如果缓冲区包含的字符串少于三个，则驱动程序必须完成具有状态 \_ 无效 \_ 参数的 IOCTL。
-   如果缓冲区的长度超过3000个字符，则驱动程序必须完成具有 \_ 无效参数的 IOCTL \_ 。
-   如果缓冲区包含一个或多个长度为零的字符串 (两个连续制表符) 则驱动程序必须完成具有状态 \_ 无效 \_ 参数的 IOCTL。
-   如果缓冲区包含偶数个字符串，则驱动程序必须完成具有状态 \_ 无效参数的 IOCTL \_ 。
-   驱动程序必须将缓冲区分析为参数字符串和平台/AppID 元组的列表。
-   如果任何平台或 AppID 字符串长度超过255个字符，则驱动程序必须完成具有 \_ 无效参数的 IOCTL \_ 。
-   写入到标记的有效负载的第一个 USHORT 必须包含以大字节序编码的平台/AppID 元组的数目。
-   所有字符串必须从 UTF-16LE 转换为 UTF-8。
-   有效负载中写入的字符串长度必须以字节为单位。
-   对于每个平台/AppID 元组，驱动程序必须向负载中添加一个字节，该字节的长度 (以字节为) 单位，后跟平台字符串本身，后面跟有一个字节，其长度 (以) 字节为单位，后跟 AppID 字符串本身。
-   驱动程序必须添加一个 USHORT，其中包含参数字符串的长度，后跟参数字符串本身。

 

 





