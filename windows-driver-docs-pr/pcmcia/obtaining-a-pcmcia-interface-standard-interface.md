---
title: 获取 PCMCIA_INTERFACE_STANDARD 接口
description: 获取 PCMCIA_INTERFACE_STANDARD 接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5f063a26204b7dfce1a916185644ab83e77fce3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812493"
---
# <a name="obtaining-a-pcmcia_interface_standard-interface"></a>获取 PCMCIA \_ 接口 \_ 标准接口





本部分介绍了驱动程序如何 \_ \_ 从 pcmcia 总线驱动程序获取 pcmcia 内存卡的 pcmcia 接口标准接口。

驱动程序 \_ \_ 通过创建和发送 irp MJ PNP 请求来获取 PCMCIA 接口标准接口， \_ \_ 该请求指定了 [**irp \_ MN \_ 查询 \_ 接口**](../kernel/irp-mn-query-interface.md) 次要函数代码。 驱动程序执行以下操作：

-   分配并在分页内存池中填充 [PCMCIA \_ 接口 \_ 标准接口内存卡例程](/windows-hardware/drivers/ddi/index) 结构。

-   为查询接口请求创建 IRP，并获取新 IRP 的下一个堆栈位置。

-   设置新堆栈位置中的以下成员：
    -   **参数. QueryInterface. 接口** 成员指向驱动程序分配的驱动程序分配的 PCMCIA \_ 接口 \_ 标准结构。
    -   **InterfaceType** 成员按 GUID 值 guid \_ PCMCIA \_ 接口 \_ 标准指定标准 PCMCIA 接口。
-   设置完成例程，并沿驱动程序堆栈向下发送请求。

如果请求成功，PCMCIA 总线驱动程序将填充 \_ \_ **参数 QueryInterface** 所指向的 PCMCIA 接口标准结构。

驱动程序必须以 IRQL &lt; 调度级别运行 \_ ，才能将此请求沿驱动程序堆栈向下发送。

 

