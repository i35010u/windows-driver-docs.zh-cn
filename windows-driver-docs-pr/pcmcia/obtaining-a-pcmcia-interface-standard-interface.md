---
title: 获取 PCMCIA_INTERFACE_STANDARD 接口
description: 获取 PCMCIA_INTERFACE_STANDARD 接口
ms.assetid: 475bf66a-5b6e-4a06-95f7-b7280dd7276d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f18880760a6c6bc682ec5a940afed73c5127b2d0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837727"
---
# <a name="obtaining-a-pcmcia_interface_standard-interface"></a>\_标准接口获取 PCMCIA\_接口





本部分介绍了驱动程序如何从 PCMCIA 总线驱动程序获取 pcmcia 内存卡的 PCMCIA\_接口\_标准接口。

驱动程序通过创建和发送\_IRP\_接口\_标准接口，\_PNP 请求指定[**irp\_\_查询\_INTERFACE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)小调函数代码，从而获取 PCMCIA 接口。 驱动程序执行以下操作：

-   在分页内存池中，分配并零填充[PCMCIA\_接口\_标准接口内存卡例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)结构。

-   为查询接口请求创建 IRP，并获取新 IRP 的下一个堆栈位置。

-   设置新堆栈位置中的以下成员：
    -   **参数. QueryInterface. 接口**成员指向驱动程序分配的 PCMCIA\_接口\_标准结构，该结构是由驱动程序分配的。
    -   **InterfaceType**成员通过 GUID 值 guid 指定标准 pcmcia 接口\_PCMCIA\_INTERFACE\_standard。
-   设置完成例程，并沿驱动程序堆栈向下发送请求。

如果请求成功，PCMCIA 总线驱动程序将填充 PCMCIA\_接口\_标准结构中由**参数**指向的标准结构。

驱动程序必须以 IRQL 运行 &lt; 调度\_级别以便向下发送此请求，使驱动程序堆栈向下发送。

 

 





