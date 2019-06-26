---
title: 获取 PCMCIA_INTERFACE_STANDARD 接口
description: 获取 PCMCIA_INTERFACE_STANDARD 接口
ms.assetid: 475bf66a-5b6e-4a06-95f7-b7280dd7276d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebb212e4dfe405ccb4e4d93bc8e7f6facc41d7a1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386196"
---
# <a name="obtaining-a-pcmciainterfacestandard-interface"></a>获取 PCMCIA\_接口\_标准接口





本部分介绍如何将驱动程序可以获取 PCMCIA\_接口\_标准接口，用于从 PCMCIA 总线驱动程序内存 PCMCIA 卡。

驱动程序将获取 PCMCIA\_接口\_标准接口，通过创建并发送 IRP\_MJ\_指定的即插即用请求[ **IRP\_MN\_查询\_接口**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)次要函数代码。 该驱动程序将执行以下操作：

-   分配和零填充[PCMCIA\_界面\_标准接口内存卡例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)结构中的分页的内存池。

-   创建查询接口请求 IRP 并获取新的 IRP 的下一步的堆栈位置。

-   在新的堆栈位置中设置的以下成员：
    -   **Parameters.QueryInterface.Interface**成员将指向驱动程序分配 PCMCIA\_接口\_标准驱动程序分配的结构。
    -   **Parameters.QueryInterface.InterfaceType**成员指定 GUID 的 GUID 值的标准接口，PCMCIA\_PCMCIA\_接口\_标准。
-   设置完成例程，然后将驱动程序堆栈请求。

如果请求成功，PCMCIA 总线驱动程序填充 PCMCIA\_接口\_指向标准结构**Parameters.QueryInterface.Interface**。

驱动程序必须运行在 IRQL&lt;调度\_要发送此请求关闭驱动程序堆栈级别。

 

 





