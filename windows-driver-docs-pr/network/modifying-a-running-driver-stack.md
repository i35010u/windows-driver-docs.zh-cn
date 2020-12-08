---
title: 修改正在运行的驱动程序堆栈
description: 修改正在运行的驱动程序堆栈
keywords:
- 驱动程序堆栈 WDK 网络，修改正在运行的堆栈
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 110eaaa23d66c66642e75713636127bf466c2ce5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782247"
---
# <a name="modifying-a-running-driver-stack"></a>修改正在运行的驱动程序堆栈





NDIS 为操作（例如插入、删除或重新配置筛选器模块）修改了驱动程序堆栈。 NDIS 可以在筛选器模块中激活或停用旁路模式。 有关筛选器驱动程序中旁路模式的详细信息，请参阅 [数据绕过模式](data-bypass-mode.md)。

**注意**  如果筛选器驱动程序入口点更改 (即因为绕过模式) ，NDIS 将暂停并重启驱动程序堆栈。 暂停和重新启动可能会导致某些网络数据包被丢弃到传输路径或接收路径上。 如果数据包丢失，则提供可靠传输机制的网络协议可能会重试网络 i/o 操作，但是其他不保证可靠性的协议不会重试该操作。

 

NDIS 按如下方式修改正在运行的驱动程序堆栈：

1.  NDIS 暂停驱动程序堆栈。

    有关详细信息，请参阅 [暂停驱动程序堆栈](pausing-a-driver-stack.md)。

2.  NDIS 修改堆栈。

    例如，若要添加筛选器模块，NDIS 确定将新筛选模块插入到堆栈中的位置，并创建、插入和附加筛选器模块。

3.  插入或删除筛选器模块时，驱动程序堆栈的特性可能会改变。 在这种情况下，NDIS 会将即插即用事件通知发送到驱动程序堆栈中的所有协议绑定和筛选器模块，以通知驱动程序此更改。

4.  NDIS 重启驱动程序堆栈。

    有关详细信息，请参阅 [重新启动驱动程序堆栈](restarting-a-driver-stack.md)。

 

 





