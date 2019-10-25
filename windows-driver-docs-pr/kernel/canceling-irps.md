---
title: 取消 IRP
description: 取消 IRP
ms.assetid: da199435-f6c3-44f4-b1ed-0280f39ee452
keywords:
- Irp WDK 内核，取消
- 正在取消 Irp
- 取消例程
- 用户取消的 i/o 请求 WDK 内核
- 完成 Irp WDK 内核，取消 Irp
- 未处理的 IRP 取消 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 717abfac19a7ed0564344f56e71a847581a745e1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828547"
---
# <a name="canceling-irps"></a>取消 IRP





Irp 可能会持续排队等候的驱动程序（因此用户可以取消以前提交的 i/o 请求）必须有一个或多个[*cancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)例程来完成用户取消的 i/o 请求。 例如，键盘、鼠标、并行、串行和声音设备驱动程序（或其上分层的驱动程序）和文件系统驱动程序应具有*取消*例程。

适用于 Microsoft Windows XP 和更高版本操作系统的驱动程序可以使用[取消安全 IRP 队列](cancel-safe-irp-queues.md)，而不是实现自己的*取消*例程。

若要 "取消 IRP"，请尽可能快地完成 IRP，同时仍保持系统的完整性。 有关 IRP 完成的一般讨论，请参阅[完成 irp](completing-irps.md)。

当系统或驱动程序调用[**IoCancelIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)时，取消过程开始。 对于与尚未完全完成的线程关联的每个 IRP，将调用此例程。 如果启动 i/o 请求的线程退出，系统会取消未处理的 Irp。 驱动程序只能取消已创建的 Irp （请参阅[为低级驱动程序创建 irp](creating-irps-for-lower-level-drivers.md)。）

如果在5分钟内未完成 IRP，i/o 管理器会将 IRP 视为超时。此类 Irp 与线程解除关联，并为当前拥有 IRP 的设备记录错误。 你应确保在你的驱动程序中可能需要很长时间才能完成的任何请求都是可取消的。 若要确保可能的长时间请求可取消，可以使用 "[取消安全 IRP 队列](cancel-safe-irp-queues.md)" 或 "[内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/design-guide)"，它将取消从驱动程序开发人员中取消。

本部分提供下列主题：

[取消例程简介](introduction-to-cancel-routines.md)

[注册取消例程](registering-a-cancel-routine.md)

[正在同步 IRP 取消](synchronizing-irp-cancellation.md)

[实现取消例程](implementing-a-cancel-routine.md)

[取消 Irp 时要考虑的要点](points-to-consider-when-canceling-irps.md)

 

 




