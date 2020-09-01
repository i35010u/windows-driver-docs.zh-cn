---
title: 获取有关 I/O 请求的信息
description: 获取有关 I/O 请求的信息
ms.assetid: a686ea00-6987-480a-a4ce-892e1efbed87
keywords:
- 请求处理 WDK KMDF，获取有关
- I/o 请求 WDK KMDF，获取有关
- 状态信息 WDK KMDF
- 状态信息 WDK KMDF、i/o 请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24730640373e995887b8a7388097294cf59806fc
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184613"
---
# <a name="obtaining-information-about-an-io-request"></a>获取有关 I/O 请求的信息


在处理 i/o 请求之前，驱动程序必须确定请求类型。 当基于框架的驱动程序为设备 [创建 i/o 队列](creating-i-o-queues.md) 时，它通常会设置 i/o 队列和请求处理程序，以便每个队列或请求处理程序收到特定类型的请求 (读取、写入或设备 i/o 控制) 。

确定请求类型后，驱动程序必须获取请求的输入和输出缓冲区（如果需要）。 有关获取请求的缓冲区的信息，请参阅 [在基于框架的驱动程序中访问数据缓冲区](./accessing-data-buffers-in-wdf-drivers.md)。

为了提供有关驱动程序已收到的 i/o 请求的其他信息，框架请求对象定义以下方法：

-   [**WdfRequestGetIoQueue**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetioqueue)，它返回传递 i/o 请求的 i/o 队列的句柄。

-   [**WdfRequestGetRequestorMode**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetrequestormode)，它返回请求的发起方 (用户或内核) 的处理器访问模式。

-   [**WdfRequestGetFileObject**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetfileobject)，它返回与请求关联的框架文件对象的句柄。

-   [**WdfRequestWdmGetIrp**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestwdmgetirp)，它返回与请求关联的 WDM [**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp) 结构。

-   [**WdfRequestGetParameters**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetparameters)，用于检索 WDM 格式的非 IRP 请求参数。

驱动程序完成 i/o 请求之后，驱动程序堆栈中的其他驱动程序可以调用其他请求对象方法来获取请求完成信息。 有关这些其他方法的详细信息，请参阅 [完成 I/o 请求](completing-i-o-requests.md)。

 

