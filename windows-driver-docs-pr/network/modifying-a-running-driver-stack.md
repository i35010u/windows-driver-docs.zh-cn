---
title: 修改运行驱动程序堆栈
description: 修改运行驱动程序堆栈
ms.assetid: b8279471-50f4-46f5-8c77-d354dd9b94b5
keywords:
- 驱动程序堆栈 WDK 网络，修改正在运行的堆栈
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4db538bebf285924c017166a6aca7cca9448e4ac
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520712"
---
# <a name="modifying-a-running-driver-stack"></a>修改运行驱动程序堆栈





NDIS 修改操作，例如插入、 删除或重新配置筛选器模块的驱动程序堆栈。 NDIS 可以激活或停用筛选器模块中的绕过模式。 有关筛选器驱动程序中的绕过模式的详细信息，请参阅[数据绕过模式](data-bypass-mode.md)。

**请注意**  如果筛选器驱动程序入口点更改 (即，由于旁路模式)，NDIS 暂停和重新启动驱动程序堆栈。 暂停和重启可能导致某些网络数据包被删除的传输路径，或者接收路径。 提供一种可靠的传输机制的网络协议可能会重试网络 I/O 操作对于丢失的数据包，但并不能保证可靠性其他协议不重试该操作。

 

NDIS 会修改正在运行的驱动程序堆栈，如下所示：

1.  NDIS 暂停驱动程序堆栈。

    有关详细信息，请参阅[暂停驱动程序堆栈](pausing-a-driver-stack.md)。

2.  NDIS 修改堆栈。

    例如，若要添加筛选器模块，NDIS 确定位置堆栈中插入新的筛选器模块和创建、 插入，并且将附加筛选器模块。

3.  当插入或删除筛选器模块时，可能会更改驱动程序堆栈的特征。 在这种情况下，NDIS 将插事件通知发送到的所有协议绑定和驱动程序堆栈中的筛选器模块以通知此更改的驱动程序。

4.  NDIS 驱动程序堆栈，重新启动。

    有关详细信息，请参阅[重新启动驱动程序堆栈](restarting-a-driver-stack.md)。

 

 





