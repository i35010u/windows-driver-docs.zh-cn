---
title: 完成 IRP
description: 完成 IRP
ms.assetid: 4b4be95e-ebf5-4726-87fc-20c3e6c94f52
keywords:
- Irp WDK 内核，完成
- 完成 Irp WDK 内核
- 已完成 Irp WDK 内核
- I/o WDK 内核，操作已完成
- 完成 irp WDK 内核，关于完成 Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d3026668e238c8fe5691a24deeb55e6e515dbcf
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89402762"
---
# <a name="completing-irps"></a>完成 IRP





"完成 IRP" 是一种简写短语，这意味着 "允许驱动程序堆栈的所有成员完成 i/o 操作"。 完成 IRP 后，i/o 管理器将通知启动的应用程序，请求的 i/o 操作已完成。

当驱动程序完成了 IRP 处理后，它将从[*DpcForIsr*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)例程) 中调用[**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) (。 这会导致 i/o 管理器确定是否有任何更高级别的驱动程序为 IRP 设置了 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程。 如果是这样，则将依次调用每个 *IoCompletion* 例程，直到该链中的每个分层驱动程序都完成 IRP。

所有驱动程序都完成 IRP 后，i/o 管理器会将状态返回给操作的原始请求者。 请注意，设置驱动程序创建的 IRP 的较高级别的驱动程序必须提供 *IoCompletion* 例程，才能释放它创建的 IRP。

本节包含下列主题：

[何时完成 IRP](when-to-complete-an-irp.md)

[在 Dispatch 例程中完成 IRP](how-to-complete-an-irp-in-a-dispatch-routine.md)

[使用 IoCompletion 例程](using-iocompletion-routines.md)

 

