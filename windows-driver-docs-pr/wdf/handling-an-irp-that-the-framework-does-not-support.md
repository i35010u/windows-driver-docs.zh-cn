---
title: 处理框架不支持的 IRP
description: 处理框架不支持的 IRP
ms.assetid: 0481f335-f63b-4f93-8eb4-523a70082302
keywords:
- 不支持的 WDM Irp WDK KMDF
- Irp WDK KMDF，不受支持
- WDM Irp WDK KMDF，不支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 520878652f5e5fad65476c6ea266b0e816292b61
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844430"
---
# <a name="handling-an-irp-that-the-framework-does-not-support"></a>处理框架不支持的 IRP


\[仅适用于 KMDF\]

此框架不支持具有以下主要 IRP 代码的 i/o 请求：

-   IRP\_MJ\_创建\_MAILSLOT
-   IRP\_MJ\_创建名为\_管道的\_
-   IRP\_MJ\_设备\_更改
-   [**IRP\_MJ\_DIRECTORY\_控件**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-directory-control)
-   [**IRP\_MJ\_文件\_系统\_控件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-file-system-control)
-   [**IRP\_MJ\_刷新\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)
-   [**IRP\_MJ\_锁定\_控件**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-lock-control)
-   [**IRP\_MJ\_QUERY\_EA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-ea)
-   [**IRP\_MJ\_查询\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-information)
-   [**IRP\_MJ\_QUERY\_配额**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-quota)
-   [**IRP\_MJ\_QUERY\_安全性**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-security)
-   [**IRP\_MJ\_查询\_卷\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-volume-information)
-   [**IRP\_MJ\_集\_EA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-ea)
-   [**IRP\_MJ\_集\_信息**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-set-information)
-   [**IRP\_MJ\_集\_配额**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-quota)
-   [**IRP\_MJ\_集\_安全性**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-security)
-   [**IRP\_MJ\_设置\_卷\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-volume-information)

如果框架收到的 IRP 包含其中一个 i/o 函数代码，则该框架不处理 IRP。 如果你的驱动程序是筛选器驱动程序，则该框架会将 IRP 传递到驱动程序堆栈中的下一个较低版本的驱动程序。 如果你的驱动程序不是筛选器驱动程序，则框架将调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)来完成 IRP，状态值为 "\_无效\_设备\_请求"。

如果你的驱动程序必须处理包含这些 i/o 函数代码中的任何一个的 Irp，则驱动程序必须调用[**WdfDeviceInitAssignWdmIrpPreprocessCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback) ，以便为 i/o 函数代码注册[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)事件回调函数。

当驱动程序收到一个 IRP，其中包含驱动程序已为其注册了[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)回调函数的 i/o 函数代码时，框架会将 IRP 传递到回调函数。 然后，回调函数必须遵循[用于处理 irp 的 WDM 规则](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)来处理 irp。 驱动程序必须调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)来完成 irp，或者必须调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)将 irp 传递到下一个较低的驱动程序。

有关处理框架不支持的 IRP 的[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)回调函数的示例，请参阅[串行](sample-kmdf-drivers.md)示例驱动程序。

 

 





