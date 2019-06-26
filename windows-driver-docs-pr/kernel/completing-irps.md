---
title: 完成 IRP
description: 完成 IRP
ms.assetid: 4b4be95e-ebf5-4726-87fc-20c3e6c94f52
keywords:
- Irp WDK 内核完成
- 完成 Irp WDK 内核
- 已完成的 Irp WDK 内核
- I/O WDK 内核，操作已完成
- 完成 Irp WDK 内核，有关如何完成 Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6992c9a14567b204bde1d7d76f6d01944217ebb0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383356"
---
# <a name="completing-irps"></a>完成 IRP





"完成 IRP"是一种简写形式短语表示"允许所有成员的驱动程序堆栈，来完成某个 I/O 操作。" IRP 已经完成后，I/O 管理器会通知起始应用程序请求的 I/O 操作已完成。

当驱动程序已完成处理 IRP 时，它将调用[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest) (通常是从内部[ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)例程)。 这会导致 I/O 管理器，以确定任何更高级别的驱动程序已设置了[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine) IRP 的例程。 如果是这样，每个*IoCompletion*调用例程时，反过来，直到完成 IRP 链中的每个分层驱动程序。

IRP 的所有驱动程序完成，I/O 管理器将返回到原始请求方操作的状态。 请注意，必须提供一个更高级别的驱动程序，设置了驱动程序创建 IRP *IoCompletion*例程来释放 IRP 创建它。

本部分包含以下主题：

[何时完成 IRP](when-to-complete-an-irp.md)

[完成调度例程中的 Irp](completing-irps-in-dispatch-routines.md)

[使用 IoCompletion 例程](using-iocompletion-routines.md)

 

 




