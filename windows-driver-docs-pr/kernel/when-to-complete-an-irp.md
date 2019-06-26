---
title: 何时完成 IRP
description: 何时完成 IRP
ms.assetid: 6986b24c-e7e5-43f2-861d-b84e4c131a8a
keywords:
- 完成 Irp WDK 内核何时完成
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0174051868ff1bf4c5bdeb1a3b775cd39cfb951
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358076"
---
# <a name="when-to-complete-an-irp"></a>何时完成 IRP





当满足任何以下条件时，驱动程序应启动 IRP 完成：

-   该驱动程序确定 IRP 处理无法进行由于无效的参数或其他条件。

-   该驱动程序能够处理请求的 I/O 操作而无需传递 IRP 堆栈的下层驱动程序，并在操作完成后。

-   正在取消 IRP。 (请参阅[取消 Irp](canceling-irps.md)。)

如果不满足这些条件，驱动程序的调度例程必须传递到下一个较低的驱动程序，IRP 或它必须处理 I/O 请求的处理。 如果满足条件之一，则该驱动程序必须调用[ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)。

如果驱动程序完成请求，因为无法进行处理，或者如果它通过处理请求的操作而无需实际访问设备完成请求，则通常会调用**IoCompleteRequest**从其中一个其调度例程。 有关详细信息，请参阅[调度例程中完成 Irp](completing-irps-in-dispatch-routines.md)。

如果驱动程序必须访问的设备来满足请求，则通常会调用**IoCompleteRequest**从[ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)例程。 中广泛讨论了这些例程[服务会中断](servicing-interrupts.md)。

 

 




