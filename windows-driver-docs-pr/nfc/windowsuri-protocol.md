---
title: WindowsUri 协议
description: WindowsUri 协议
ms.assetid: 79589ECE-9DF9-40C8-897D-95B432C4C9C8
keywords:
- NFC
- 附近通信
- 近程
- 邻近附近
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 797993c17701545864de6d0ee61fc4c202999b72
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521771"
---
# <a name="windowsuri-protocol"></a>WindowsUri 协议


"WindowsUri"协议是一种抽象出来也一点简单的 URI 字符串的订阅。 若要注册的 Windows 有兴趣接收的 Uri，用户可能感兴趣启动的驱动程序，Windows 将订阅此类型。

### <a name="required-actions"></a>所需的操作

-   "WindowsUri"订阅服务器，则驱动程序必须以 NULL 结尾-16LE 编码字符串形式返回的 URI 字符串。
-   该驱动程序必须将输入的"WindowsUri"发布负载视为 UTF 16LE 编码字符串。 该驱动程序必须安全地接受以 NULL 结尾或非 null 值结束的输入。
-   如果邻近技术公布为 NFC，然后该驱动程序必须将订阅"WindowsUri"类型视为等效于"NDEF:wkt 中 URI 有效负载订阅。U"或者"NDEF:wkt。Sp"消息。
    -   该驱动程序也必须匹配"WindowsUri"订阅"NDEF:wkt 中 URI 有效负载。Sp"消息。 所有订阅的"NDEF:wkt。Sp"必须为填充"NDEF:wkt 完整负载。Sp"消息。 如果 NDEF 消息包含智能海报和非嵌套 URI 记录，必须忽略 URI 记录。
    -   该驱动程序必须返回到此类型的订阅服务器仅 URI 字符串的此消息有效负载。 驱动程序都不能返回到此类型的订阅服务器的完整 NDEF 消息。
-   如果邻近技术公布为 NFC，则该驱动程序必须封装在 NDEF 中指定的消息中每个"WindowsUri"发布的有效负载\[NFC URI\]。
-   提供程序可能支持其他兼容的方案。

## <a name="publications-for-windowsuriwritetag"></a>Publications for “WindowsUri:WriteTag”


这是一种特殊类型的允许要写入到任何可写入标记的 URI 的 WindowsUri 发布。

### <a name="required-actions"></a>所需的操作

-   常见"\*: WriteTag"其他部分所述的要求适用。
-   上面的"WindowsUri"发布要求也适用于"WindowsUri:WriteTag"发布。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[邻近 DDI 引用附近](https://msdn.microsoft.com/library/windows/hardware/jj866056)  

