---
title: 取消 IRP
description: 取消 IRP
keywords:
- Irp WDK 内核，取消
- 正在取消 Irp
- 取消例程
- 用户取消的 i/o 请求 WDK 内核
- 完成 Irp WDK 内核，取消 Irp
- 未处理的 IRP 取消 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 537c989b3ce77f8c6e73a044cbfcd205ad5d2eba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828559"
---
# <a name="canceling-irps"></a>取消 IRP





Irp 可能会保持排队等候无限间隔的驱动程序， (这样用户就可以取消以前提交的 i/o 请求) 必须有一个或多个 [*cancel*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel) 例程才能完成用户取消的 i/o 请求。 例如，键盘、鼠标、并行、串行和声音设备驱动程序 (或其上分层的驱动程序) 和文件系统驱动程序应具有 *取消* 例程。

适用于 Microsoft Windows XP 和更高版本操作系统的驱动程序可以使用 [取消安全 IRP 队列](cancel-safe-irp-queues.md) ，而不是实现自己的 *取消* 例程。

若要 "取消 IRP"，请尽可能快地完成 IRP，同时仍保持系统的完整性。 有关 IRP 完成的一般讨论，请参阅 [完成 irp](completing-irps.md)。

当系统或驱动程序调用 [**IoCancelIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)时，取消过程开始。 对于与尚未完全完成的线程关联的每个 IRP，将调用此例程。 如果启动 i/o 请求的线程退出，系统会取消未处理的 Irp。 驱动程序只能取消已创建的 Irp (请参阅 [为 Lower-Level 驱动程序创建 irp](creating-irps-for-lower-level-drivers.md)。 ) 

如果在5分钟内未完成 IRP，i/o 管理器会将 IRP 视为超时。此类 Irp 与线程解除关联，并为当前拥有 IRP 的设备记录错误。 你应确保在你的驱动程序中可能需要很长时间才能完成的任何请求都是可取消的。 若要确保可能的长时间请求可取消，可以使用 " [取消安全 IRP 队列](cancel-safe-irp-queues.md) " 或 " [内核模式驱动程序框架](../wdf/index.md)"，它将取消从驱动程序开发人员中取消。

本部分提供下列主题：

[Cancel 例程简介](introduction-to-cancel-routines.md)

[注册 Cancel 例程](registering-a-cancel-routine.md)

[同步 IRP 取消](synchronizing-irp-cancellation.md)

[实现 Cancel 例程](implementing-a-cancel-routine.md)

[取消 IRP 时要考虑的要点](points-to-consider-when-canceling-irps.md)

 

