---
title: NFP 提供程序模型
description: 附近字段邻近 (NFP) 提供程序的驱动程序模型提供了用于 Windows 使用 NFP 功能还可以启用 NFP 方案和用例的常见面。
ms.assetid: AD8DC80F-5CE2-4547-B951-A82A280F18ED
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82eb4adefbfb7ea4001863cac229eaa072d2ec7a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378834"
---
# <a name="nfp-provider-model"></a>NFP 提供程序模型


附近字段邻近 (NFP) 提供程序的驱动程序模型提供了用于 Windows 使用 NFP 功能还可以启用 NFP 方案和用例的常见面。

若要公开这些功能为 Windows，兼容的设备的实施者必须提供实现的设备驱动程序**GUID\_DEVINTERFACE\_NFP**设备接口。 此驱动程序适用于在软件和/或设备以形成 NFP 提供程序上的硬件中实现的基础 NFP 技术。

**GUID\_DEVINTERFACE\_NFP**设备接口，Windows 使用各种 NFP 技术。 此设备接口的实现者公开的最常见功能是一般并不特定于任何基础 NFP 技术。 编程到此通用功能与其他 Windows 应用进行通信的应用程序应该能够使用任何 NFP 提供程序而无需修改应用程序的代码。 由于 NFC NFP 空间中的前导标准，设备接口通过让 NFP 提供程序能够处理本机 NDEF 数据包支持 NFC 的特定行为。 应用程序可能依赖于此 NFC 特有的功能，并限制其自身的功能对 nfc 的 NFP 提供程序。

使用不兼容 NFP 提供程序的两台 Pc 不能通过其 NFP 提供程序进行通信。 此规范提供了指导原则不足以支持的两个经过认证的 Windows 系统的互操作，因为支持 nfc 的至少一个提供程序是必需的 Windows 系统证书。

NFP 提供商预暂存使用发布/订阅模型的基础 NFP 技术准确性无法保证事件触发其传输其通信。 消息发布和订阅到根据消息类型。 当两个设备变得近程 NFP 技术时，邻近状态时触发，目前已发布的所有消息都传输到另一台设备上的当前订户。 此机制提供了模型，其中用户在其设备上，设置一些上下文，然后点击与其他设备来完成的方案中的简单方法。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[邻近 DDI 引用附近](https://msdn.microsoft.com/library/windows/hardware/jj866056)  

