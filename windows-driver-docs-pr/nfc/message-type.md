---
title: 消息类型
description: 消息类型
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f21997d9d1ce3361459cc2aaf118ab94ca7790b3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813553"
---
# <a name="message-type"></a>消息类型


消息类型是用句点分隔的以 null 结尾的字符串，用于定义消息的内容、含义和目标使用者。 示例如下：

``` syntax
    Windows.contoso.com:t
```

消息类型必须始终以协议组件开头，后面可以跟更具体的子类型信息。 从 NFP 提供程序的角度来看，只需由提供程序分析并评估协议组件。 其余部分可能是不透明的，只需将已发布的消息与订阅服务器进行匹配。

## <a name="protocol-component"></a>协议组件


消息类型的协议部分定义为消息类型中第一个点之前的所有内容，如果不包含任何点，则定义整个字符串。 例如， **Windows**.com： t 的突出显示部分显示协议组件。

协议组件是一种标准化的唯一字符串，用于定义提供程序消息处理的主要分支级别。 该字符串区分大小写。 参数向 NFP 提供程序指示 *messageData* 的内容以及传输消息时使用的协议。

旨在通过 NFC 传输或接收的消息将使用 "NDEF" 协议，应假定 *messageData* 已根据特定 NDEF 标准进行格式设置。

支持 "Windows" 协议需要所有 NFP 提供程序。 如果指定 "Windows"，则 *messageData* 的格式设置为 Windows 可以对消息进行解码和理解。 但是， *messageData* 不会编码为任何 NFP 技术标准。 NFP 提供程序需要将消息参数包装在适当的协议标头中，以便可以将其传输到 Windows 设备上的接收方。

协议组件对应于 NFP 提供商理解并支持的标准类型。 当调用方指定了驱动程序不需要的协议时，NFP 提供程序必须返回错误。 这样就避免了调用方在消息未编码为预期协议的原因之间出现混淆。

协议组件的最大长度为250个字符，不包括点或 NULL 终止符)  (。

## <a name="subtype-component"></a>子类型组件


*MessageType* 的子类型组件定义为第一个点后面的所有内容。 例如，Windows<strong>.com： t</strong> 的突出显示部分显示子类型组件。

子类型组件可以由 Windows 或应用程序定义。 NFP 提供程序应使用它将消息只传递到指定 *messageType* 的订阅服务器。

子类型字符串区分大小写，并描述消息的内容。

提供程序至少必须支持以下字符;对于已发布的类型，建议限制使用以下字符：

-   字符

    `[A-Za-z0-9]`

-   加上以下非字母数字字符：

    `- . _~ : / ? # [ ] @ ! $ & ‘ ( ) * + , ; = %`

对于 "Windows" 协议，子类型字符串应遵循 URI 命名方案。 这允许两个不同的实现程序单独创建类型，同时确保它们不会意外使用同一类型。

子类型组件的最大长度为250个字符， (不包括 NULL 终止符) 。 但是，建议使用较短的类型名称，因为典型的邻近技术的消息性质很短。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[近字段邻近 DDI 引用](/windows-hardware/drivers/ddi/index)
