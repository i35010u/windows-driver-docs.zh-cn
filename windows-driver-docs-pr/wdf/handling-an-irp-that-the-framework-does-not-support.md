---
title: 处理框架不支持的 IRP
description: 处理框架不支持的 IRP
ms.assetid: 0481f335-f63b-4f93-8eb4-523a70082302
keywords:
- 不受支持的 WDM Irp WDK KMDF
- Irp WDK KMDF，不受支持
- WDM Irp WDK KMDF，不受支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6a7ab11484a4e6ab0ecb5f4202c5c4d03e7d3b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569468"
---
# <a name="handling-an-irp-that-the-framework-does-not-support"></a>处理框架不支持的 IRP


\[仅适用于 KMDF\]

框架不支持具有以下主要 IRP 代码的 I/O 请求：

-   IRP\_MJ\_CREATE\_MAILSLOT
-   IRP\_MJ\_CREATE\_NAMED\_PIPE
-   IRP\_MJ\_DEVICE\_CHANGE
-   [**IRP\_MJ\_DIRECTORY\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff548658)
-   [**IRP\_MJ\_文件\_系统\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff550751)
-   [**IRP\_MJ\_刷新\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff550760)
-   [**IRP\_MJ\_锁\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff549251)
-   [**IRP\_MJ\_查询\_EA**](https://msdn.microsoft.com/library/windows/hardware/ff549279)
-   [**IRP\_MJ\_查询\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff549283)
-   [**IRP\_MJ\_查询\_配额**](https://msdn.microsoft.com/library/windows/hardware/ff549293)
-   [**IRP\_MJ\_QUERY\_SECURITY**](https://msdn.microsoft.com/library/windows/hardware/ff549298)
-   [**IRP\_MJ\_查询\_卷\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff549318)
-   [**IRP\_MJ\_SET\_EA**](https://msdn.microsoft.com/library/windows/hardware/ff549346)
-   [**IRP\_MJ\_SET\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff550799)
-   [**IRP\_MJ\_SET\_QUOTA**](https://msdn.microsoft.com/library/windows/hardware/ff549401)
-   [**IRP\_MJ\_SET\_SECURITY**](https://msdn.microsoft.com/library/windows/hardware/ff549407)
-   [**IRP\_MJ\_设置\_卷\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff549415)

如果框架接收 IRP，其中包含这些 I/O 函数代码之一，该框架不会处理 IRP。 如果您的驱动程序筛选器驱动程序，该框架会将 IRP 传递给驱动程序堆栈中的下一步低驱动程序。 如果您的驱动程序不是筛选器驱动程序，框架将调用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)若要完成的状态将 status 值 IRP\_无效\_设备\_请求。

如果您的驱动程序必须处理包含任何这些 I/O 函数代码的 Irp，驱动程序必须调用[ **WdfDeviceInitAssignWdmIrpPreprocessCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff546043)注册[ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925) I/O 函数代码的事件回调函数。

当驱动程序收到包含一个 I/O 函数代码，该驱动程序已注册的 IRP [ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)为回调的 framework 阶段 IRP 的回调函数函数。 回调函数然后必须按照处理 IRP [WDM 规则处理 Irp](https://msdn.microsoft.com/library/windows/hardware/ff546847)。 该驱动程序必须调用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)到完整 IRP，或它必须调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)将 IRP 传递到下一步越低驱动程序。

有关的示例[ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)回调函数处理 IRP 框架不支持，请参阅[串行](sample-kmdf-drivers.md)示例驱动程序。

 

 





