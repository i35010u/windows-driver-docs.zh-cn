---
title: Windows 协议
description: Windows 协议
ms.assetid: 9D28589E-FA19-43F2-BE22-438795807657
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 938bd8b8bb4f202cd4431662cb3b598af05951c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373551"
---
# <a name="windows-protocol"></a>Windows 协议


为了确保 nfc 的 NFP 提供程序的互操作性，此节定义完全如何 Windows 消息应封装在一个 NDEF 消息中。 本部分还将 NFP 发布/订阅模型映射到已发布的 NFC 论坛协议 NDEF 消息交换。 邻近技术公布为 NFC，这些要求才适用。

## <a name="encapsulation"></a>封装


必须满足以下要求，以确保正确封装的 NFC 互操作性的 Windows 消息。

### <a name="required-actions"></a>所需的操作

-   如果邻近技术公布为 NFC，然后该驱动程序必须将封装每个"Windows。&lt;SomeSubType&gt;"与 TNF NDEF 消息中的发布字段的 0x03 的值。
    -   NDEF 类型字段必须包含的直接映射&lt;SomeSubType&gt;其中每个宽字符被解释为一个字节的字符串。
    -   NDEF 有效负载必须包含发布消息负载的直接二进制内容。
-   如果邻近技术公布为 NFC，则该驱动程序必须与匹配订阅的"Windows。&lt;SomeSubType&gt;"仅使用 NDEF 消息 0x03 TNF 字段值和类型字段，它等于"&lt;SomeSubType&gt;"其中的每个宽字符被解释为单字节

    该驱动程序必须返回到此类型的订阅服务器仅匹配 NDEF 消息的有效负载。

## <a name="windowswritetag-publications"></a>"Windows: WriteTag。" 发布


"Windows: WriteTag。" 发布是一种方法只需向标记写入 Windows 类型的有效负载的应用。

### <a name="required-actions"></a>所需的操作

-   常见"\*: WriteTag"其他部分所述的要求适用。
-   "Windows。&lt;SomeSubType&gt;"发布要求也适用于"Windows: WriteTag。&lt;SomeSubType&gt;"发布。

## <a name="launchappwritetag-publications"></a>"LaunchApp:WriteTag"发布


"LaunchApp:WriteTag"发布是用于只需写入标记"Windows.windows.com/LaunchApp"消息的应用的方式。

客户端将发送以 UTF 16LE 编码此发布的有效负载的制表符分隔 （或 null 分隔） 列表的字符串。 第一个字符串是该应用程序的参数列表。 参数字符串后面将对的字符串。 每个对中的第一个字符串的应用 id 定义的平台限定符下, 一个字符串是实际的应用程序 ID，以便在该平台上启动。 此机制支持跨 Windows 之外的应用平台的互操作性。

### <a name="required-actions"></a>所需的操作

-   类型好像"Windows.windows.com/LaunchApp"，必须进行编码的消息的类型。
-   如果缓冲区包含少于三个字符串驱动程序必须完成状态 IOCTL\_无效\_参数。
-   如果缓冲区的长度超过 3,000 个字符，驱动程序必须完成状态 IOCTL\_无效\_参数。
-   如果在缓冲区中包含一个或多个零长度字符串 （两个连续的选项卡字符） 驱动程序必须完成状态 IOCTL\_无效\_参数。
-   如果缓冲区包含偶数个字符串驱动程序必须完成状态 IOCTL\_无效\_参数。
-   该驱动程序必须分析缓冲区为参数字符串和平台/应用程序 Id 的元组的列表。
-   如果任何平台或应用程序标识字符串的长度超过 255 个字符，驱动程序必须完成状态 IOCTL\_无效\_参数。
-   写入标记的有效负载的第一个 USHORT 必须包含 big endian 编码中的平台/应用程序 Id 元组数目。
-   为 utf-8，必须从 UTF 16LE 转换所有字符串。
-   编写有效负载中的字符串长度必须是以字节为单位。
-   每个平台/应用程序 Id 元组驱动程序必须将添加到负载字节跟平台字符串本身跟 AppID 字符串本身的应用程序标识字符串的长度 （以字节为单位） 字节后跟的平台字符串的长度 （以字节为单位）。
-   该驱动程序必须添加包含跟参数字符串本身的参数字符串的长度 USHORT。

 

 





