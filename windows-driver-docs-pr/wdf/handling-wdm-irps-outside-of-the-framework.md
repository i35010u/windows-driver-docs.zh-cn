---
title: 在框架外部处理 WDM IRP
description: 在框架外部处理 WDM IRP
ms.assetid: 43e1df0c-c0d1-4d41-87de-9f8f5831fb19
keywords:
- WDM Irp WDK KMDF
- WDM Irp WDK KMDF，framework 外部
- Irp WDK KMDF
- Irp WDK KMDF，framework 外部
- I/O 请求数据包 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8dc11d49c35f418e56a9fb14287339b2150ce51f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391879"
---
# <a name="handling-wdm-irps-outside-of-the-framework"></a>在框架外部处理 WDM IRP


\[仅适用于 KMDF\]

时 I/O 管理器提供对基于 framework 的驱动程序的 I/O 请求数据包 (IRP)，框架截获 IRP，然后进行以下项之一：

-   处理 IRP。 例如，框架处理包含的 Irp [ **IRP\_MJ\_PNP** ](https://msdn.microsoft.com/library/windows/hardware/ff550772)并[ **IRP\_MJ\_电源** ](https://msdn.microsoft.com/library/windows/hardware/ff550784)主要 I/O 函数代码。 在处理这些 Irp，框架可以通过调用回调函数的驱动程序的事件通信与驱动程序。

-   为 IRP 创建一个框架请求对象，并将请求对象传递给驱动程序的 I/O 队列之一，以便该驱动程序可以接收它，通常在请求处理程序，并对其进行处理。 该框架将处理这种方式中的读取、 写入和设备 I/O 控制请求。

-   将 IRP 传递给下一个较低驱动程序 （如果您的驱动程序筛选器驱动程序） 或完成状态将 status 值 IRP\_无效\_设备\_因为 IRP 包含 I/O 请求 （如果您的驱动程序不是筛选器驱动程序）框架不支持的函数代码。

有时一个驱动程序必须处理框架不支持一个 I/O 函数代码。

很少，驱动程序可能需要进行预处理 IRP，该框架将处理它，或该驱动程序可能需要后 framework postprocess IRP 和较低级别的驱动程序已完成处理之前。

预处理的一部分，驱动程序可能需要将转发到特定的 I/O 队列 IRP。

以下主题介绍了这些情况下：

-   [处理 IRP 框架不支持](handling-an-irp-that-the-framework-does-not-support.md)
-   [预处理和后处理 Irp](preprocessing-and-postprocessing-irps.md)
-   [调度到的 I/O 队列的 Irp](dispatching-irps-to-i-o-queues.md)

 

 





