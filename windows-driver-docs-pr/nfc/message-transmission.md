---
title: 消息传输
description: 消息传输
ms.assetid: 96C5CE38-25EE-425A-A7C5-05990CBE2C3E
keywords:
- NFC
- 附近通信
- 近程
- 邻近附近
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0de859385c7290117af64cdfdf66b3a705fbb06a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554765"
---
# <a name="message-transmission"></a>消息传输


当 NFP 技术确定，定义的邻近性技术是近似，另一台设备时，这应充当触发器来传输设备之间的已发布的消息。

在邻近设备时，应仅一次传输已发布的消息。

当前发布的所有消息都应都传输设备来自内在邻近每次。

如果消息已发布近程设备并且该触发器，则仍处于活动状态时，应将该消息传输。

传递到近程设备发布的并不意味着应由 NFP 提供程序已取消发布发布。 该发布将保持活动状态的下一步的近程事件，直到客户端取消发布它。

NFP 设备驱动程序接口不需要已发布的消息能传输的已发布的顺序。 NFP 设备驱动程序接口不需要所有已发布的消息将传输作为单个块。 NFC 专门提供了详细防止这种情况的互操作要求： 传输多个消息，不允许单个块的方式。 但是，它是一项要求完全和不包含错误的情况下接收单个已发布的消息或它们不应传递到已订阅的客户端。

没有 NFP 设备驱动程序接口，如果接收的设备上的任何应用已订阅该消息告诉客户端中定义的机制。 还有告诉客户端接收到它们未订阅到消息的机制。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[邻近 DDI 引用附近](https://msdn.microsoft.com/library/windows/hardware/jj866056)  

