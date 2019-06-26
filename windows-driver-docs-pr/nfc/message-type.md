---
title: 消息类型
description: 消息类型
ms.assetid: 3C64F85F-D8AE-4448-A75C-965DCCD85216
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ce38566a9ddd7e92e8a0528b01fa075ac6c3dae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375080"
---
# <a name="message-type"></a>消息类型


消息类型是一个圆点分隔的以 null 结尾定义字符串的内容、 含义和消息的预期使用者。 是一个示例：

``` syntax
    Windows.contoso.com:t
```

消息类型必须始终以开头的协议组件，还可以通过更具体的子类型信息。 从 NFP 提供程序的角度来看，仅协议组件需要解析结果并评估由提供程序。 其余部分可以是不透明，并仅需要用于匹配与订阅服务器的已发布的消息。

## <a name="protocol-component"></a>协议组件


如果它不包含点的消息类型的协议组件定义为消息类型或整个字符串中的第一个点前的所有内容。 例如，突出显示部分的**Windows**。 contoso.com:t 显示的协议组件。

协议组件是一个标准化的唯一字符串，定义的主分支的提供程序消息处理的级别。 该字符串区分大小写。 参数指示 NFP 提供程序的内容*messageData*以及传输消息时要使用哪种协议。

用于传输或通过 NFC 接收一条消息将使用"NDEF"协议和*messageData*应假定要根据特定的 NDEF 标准格式化。

支持的"Windows"协议所需所有 NFP 提供程序。 当指定"Windows"时， *messageData* ，以便 Windows 可以解码并了解消息格式。 但是， *messageData*不到任何 NFP 技术标准进行编码。 NFP 提供程序将需要包装在适当的协议标头中的消息参数，以便它可以传输到 Windows 设备上接收方。

与标准化 NFP 提供程序能够理解和支持的类型相对应的协议组件。 调用方指定一种协议，该驱动程序不应为 NFP 提供程序必须返回一个错误。 这样可避免在调用方有关为什么一条消息不进行编码到预期的协议之间的混淆。

协议组件的最大长度为 250 个字符 （不包括圆点或 NULL 终止符）。

## <a name="subtype-component"></a>子类型组件


子类型组成部分*messageType*后的第一个点定义为所有内容。 例如，Windows 的突出显示部分<strong>。 contoso.com:t</strong>显示子类型组件。

由 Windows 或应用程序，可能会定义子类型组件。 NFP 提供程序应使用它来将消息传递到指定的订阅服务器仅*messageType*。

子类型字符串是区分大小写，并且描述消息的内容。

提供程序必须至少支持以下字符;对于已发布的类型，建议限制为以下字符的使用：

-   字母数字：

    `[A-Za-z0-9]`

-   加上以下非字母数字字符：

    `- . _~ : / ? # [ ] @ ! $ & ‘ ( ) * + , ; = %`

对于"Windows"的协议，子类型字符串应遵循 URI 命名方案。 这允许两个不同的实施者能独立地创建类型，同时确保他们不会意外地最终会使用相同的类型。

子类型组件的最大长度为 250 个字符 （不包括 NULL 终止符）。 但是，由于典型邻近技术短消息建议较短的类型名称。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[邻近 DDI 引用附近](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

