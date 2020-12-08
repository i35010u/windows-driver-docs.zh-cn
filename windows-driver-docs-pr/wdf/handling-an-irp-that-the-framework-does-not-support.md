---
title: 处理框架不支持的 IRP
description: 处理框架不支持的 IRP
keywords:
- 不支持的 WDM Irp WDK KMDF
- Irp WDK KMDF，不受支持
- WDM Irp WDK KMDF，不支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0f461b405ab28e1cc321479506d224d2f9ad252
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795229"
---
# <a name="handling-an-irp-that-the-framework-does-not-support"></a>处理框架不支持的 IRP


\[仅适用于 KMDF\]

此框架不支持具有以下主要 IRP 代码的 i/o 请求：

-   IRP \_ MJ \_ CREATE \_ MAILSLOT
-   IRP \_ MJ \_ 创建 \_ 命名 \_ 管道
-   IRP \_ MJ \_ 设备 \_ 更改
-   [**IRP \_ MJ \_ 目录 \_ 控件**](../ifs/irp-mj-directory-control.md)
-   [**IRP \_ MJ \_ 文件 \_ 系统 \_ 控制**](../kernel/irp-mj-file-system-control.md)
-   [**IRP \_ MJ \_ 刷新 \_ 缓冲区**](../kernel/irp-mj-flush-buffers.md)
-   [**IRP \_ MJ \_ 锁定 \_ 控制**](../ifs/irp-mj-lock-control.md)
-   [**IRP \_ MJ \_ 查询 \_ EA**](../ifs/irp-mj-query-ea.md)
-   [**IRP \_ MJ \_ 查询 \_ 信息**](../ifs/irp-mj-query-information.md)
-   [**IRP \_ MJ \_ 查询 \_ 配额**](../ifs/irp-mj-query-quota.md)
-   [**IRP \_ MJ \_ 查询 \_ 安全性**](../ifs/irp-mj-query-security.md)
-   [**IRP \_ MJ \_ 查询 \_ 卷 \_ 信息**](../ifs/irp-mj-query-volume-information.md)
-   [**IRP \_ MJ \_ 设置 \_ EA**](../ifs/irp-mj-set-ea.md)
-   [**IRP \_ MJ \_ 设置 \_ 信息**](../kernel/irp-mj-set-information.md)
-   [**IRP \_ MJ \_ 设置 \_ 配额**](../ifs/irp-mj-set-quota.md)
-   [**IRP \_ MJ \_ 设置 \_ 安全性**](../ifs/irp-mj-set-security.md)
-   [**IRP \_ MJ \_ 设置 \_ 卷 \_ 信息**](../ifs/irp-mj-set-volume-information.md)

如果框架收到的 IRP 包含其中一个 i/o 函数代码，则该框架不处理 IRP。 如果你的驱动程序是筛选器驱动程序，则该框架会将 IRP 传递到驱动程序堆栈中的下一个较低版本的驱动程序。 如果驱动程序不是筛选器驱动程序，框架将调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 来完成 IRP，使其状态值为 "状态 \_ 无效的 \_ 设备请求" \_ 。

如果你的驱动程序必须处理包含这些 i/o 函数代码中的任何一个的 Irp，则驱动程序必须调用 [**WdfDeviceInitAssignWdmIrpPreprocessCallback**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback) ，以便为 i/o 函数代码注册 [*EvtDeviceWdmIrpPreprocess*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess) 事件回调函数。

当驱动程序收到一个 IRP，其中包含驱动程序已为其注册了 [*EvtDeviceWdmIrpPreprocess*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess) 回调函数的 i/o 函数代码时，框架会将 IRP 传递到回调函数。 然后，回调函数必须遵循 [用于处理 irp 的 WDM 规则](../kernel/handling-irps.md)来处理 irp。 驱动程序必须调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 来完成 irp，或者必须调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 将 irp 传递到下一个较低的驱动程序。

有关处理框架不支持的 IRP 的 [*EvtDeviceWdmIrpPreprocess*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess) 回调函数的示例，请参阅 [串行](sample-kmdf-drivers.md) 示例驱动程序。

 

