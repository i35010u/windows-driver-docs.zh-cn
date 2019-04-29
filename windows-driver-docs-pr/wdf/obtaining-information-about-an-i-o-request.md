---
title: 获取有关 I/O 请求的信息
description: 获取有关 I/O 请求的信息
ms.assetid: a686ea00-6987-480a-a4ce-892e1efbed87
keywords:
- 请求处理 WDK KMDF，获取有关的信息
- I/O 请求 WDK KMDF，获取有关的信息
- WDK KMDF 的状态信息
- 状态信息 WDK KMDF，I/O 请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4462c2f603f5d7c6e6ce57017fe9048961c2e8f9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390128"
---
# <a name="obtaining-information-about-an-io-request"></a>获取有关 I/O 请求的信息


在处理前的 I/O 请求，驱动程序必须确定请求类型。 当基于 framework 的驱动程序[创建的 I/O 队列](creating-i-o-queues.md)对于设备，它通常设置的 I/O 队列和请求处理程序，以便每个队列或请求的处理程序接收特定类型 （读取、 写入或设备 I/O 控制） 的请求。

之后确定请求类型时，该驱动程序必须获取请求的输入和输出缓冲区，如果需要它们。 有关获取请求的缓冲区的信息，请参阅[基于 Framework 的驱动程序中访问数据缓冲区](https://msdn.microsoft.com/library/windows/hardware/ff540701)。

若要提供有关驱动程序已接收的 I/O 请求的其他信息，framework 请求对象定义以下方法：

-   [**WdfRequestGetIoQueue**](https://msdn.microsoft.com/library/windows/hardware/ff549968)，其中返回的句柄从其发送的 I/O 请求的 I/O 队列。

-   [**WdfRequestGetRequestorMode**](https://msdn.microsoft.com/library/windows/hardware/ff549971)，这会返回请求的原始发件人的处理器访问模式 （用户或内核）。

-   [**WdfRequestGetFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff549963)，其中返回的句柄与请求关联的框架文件对象。

-   [**WdfRequestWdmGetIrp**](https://msdn.microsoft.com/library/windows/hardware/ff550037)，这会返回 WDM [ **IRP** ](https://msdn.microsoft.com/library/windows/hardware/ff550694)结构，它是与请求关联。

-   [**WdfRequestGetParameters**](https://msdn.microsoft.com/library/windows/hardware/ff549969)，检索非 IRP WDM 格式的请求参数。

驱动程序完成的 I/O 请求后，驱动程序堆栈中的其他驱动程序可以调用其他请求对象方法以获取请求完成信息。 有关这些其他方法的详细信息，请参阅[完成 I/O 请求](completing-i-o-requests.md)。

 

 





