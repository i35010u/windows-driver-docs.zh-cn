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
ms.openlocfilehash: 2808940a38a5300eb50fbd7ba4b44ff61077917a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382864"
---
# <a name="handling-an-irp-that-the-framework-does-not-support"></a>处理框架不支持的 IRP


\[仅适用于 KMDF\]

框架不支持具有以下主要 IRP 代码的 I/O 请求：

-   IRP\_MJ\_CREATE\_MAILSLOT
-   IRP\_MJ\_CREATE\_NAMED\_PIPE
-   IRP\_MJ\_DEVICE\_CHANGE
-   [**IRP\_MJ\_DIRECTORY\_控件**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-directory-control)
-   [**IRP\_MJ\_文件\_系统\_控件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-file-system-control)
-   [**IRP\_MJ\_刷新\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)
-   [**IRP\_MJ\_锁\_控件**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-lock-control)
-   [**IRP\_MJ\_查询\_EA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-ea)
-   [**IRP\_MJ\_查询\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-information)
-   [**IRP\_MJ\_查询\_配额**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-quota)
-   [**IRP\_MJ\_QUERY\_SECURITY**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-security)
-   [**IRP\_MJ\_查询\_卷\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-volume-information)
-   [**IRP\_MJ\_SET\_EA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-ea)
-   [**IRP\_MJ\_SET\_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-set-information)
-   [**IRP\_MJ\_SET\_QUOTA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-quota)
-   [**IRP\_MJ\_SET\_SECURITY**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-security)
-   [**IRP\_MJ\_设置\_卷\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-volume-information)

如果框架接收 IRP，其中包含这些 I/O 函数代码之一，该框架不会处理 IRP。 如果您的驱动程序筛选器驱动程序，该框架会将 IRP 传递给驱动程序堆栈中的下一步低驱动程序。 如果您的驱动程序不是筛选器驱动程序，框架将调用[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)若要完成的状态将 status 值 IRP\_无效\_设备\_请求。

如果您的驱动程序必须处理包含任何这些 I/O 函数代码的 Irp，驱动程序必须调用[ **WdfDeviceInitAssignWdmIrpPreprocessCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback)注册[ *EvtDeviceWdmIrpPreprocess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess) I/O 函数代码的事件回调函数。

当驱动程序收到包含一个 I/O 函数代码，该驱动程序已注册的 IRP [ *EvtDeviceWdmIrpPreprocess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)为回调的 framework 阶段 IRP 的回调函数函数。 回调函数然后必须按照处理 IRP [WDM 规则处理 Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)。 该驱动程序必须调用[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)到完整 IRP，或它必须调用[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)将 IRP 传递到下一步越低驱动程序。

有关的示例[ *EvtDeviceWdmIrpPreprocess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)回调函数处理 IRP 框架不支持，请参阅[串行](sample-kmdf-drivers.md)示例驱动程序。

 

 





