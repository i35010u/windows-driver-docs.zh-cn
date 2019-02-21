---
title: 正在取消 Irp
description: 正在取消 Irp
ms.assetid: da199435-f6c3-44f4-b1ed-0280f39ee452
keywords:
- Irp WDK 内核，取消
- 正在取消 Irp
- 取消例程
- 用户已取消 I/O 请求 WDK 内核
- 完成 Irp WDK 内核，取消 Irp
- 未处理的 IRP 取消 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e2888c0913c923a2d46c52ee80ffd45967ac6b0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526152"
---
# <a name="canceling-irps"></a>正在取消 Irp





无限期的时间间隔 （因此，用户可以取消以前提交的 I/O 请求） 必须具有一个或多个驱动程序 Irp 可能会保持排入队列[*取消*](https://msdn.microsoft.com/library/windows/hardware/ff540742)例程来完成用户已取消 I/O请求数。 例如，键盘、 鼠标、 并行、 串行、 和声音设备驱动程序 （或它们的上层的驱动程序） 和文件系统驱动程序应具有*取消*例程。

Microsoft Windows XP 和更高版本操作系统的驱动程序可以使用[取消安全 IRP 队列](cancel-safe-irp-queues.md)而不是实现其自己*取消*例程。

"取消 IRP"意味着尽可能快地完成 IRP，同时仍保持系统的完整性。 IRP 完成的一般讨论，请参阅[完成 Irp](completing-irps.md)。

取消过程开始时系统或驱动程序调用[ **IoCancelIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548338)。 此例程称为为每个 IRP 与未完全完成的线程相关联。 如果发起 I/O 请求的线程退出，系统将取消未处理的 Irp。 驱动程序可以取消他们所创建的 Irp (请参阅[较低级别驱动程序创建 Irp](creating-irps-for-lower-level-drivers.md)。)

如果未在 5 分钟内完成 IRP，I/O 管理器会考虑 IRP 操作已超时。此类 Irp 断开线程，并针对当前拥有 IRP 设备记录一个错误。 您应确保可能需要很长时间才能完成驱动程序中的所有请求可取消。 若要确保可取消可能很长的请求，可以使用[取消安全 IRP 队列](cancel-safe-irp-queues.md)或[内核模式驱动程序框架](https://msdn.microsoft.com/library/windows/hardware/dn265580)，其中提取了驱动程序开发人员面临的取消。

本部分提供了以下主题：

[若要取消例程的简介](introduction-to-cancel-routines.md)

[注册在取消例程](registering-a-cancel-routine.md)

[同步 IRP 取消](synchronizing-irp-cancellation.md)

[实现取消例程](implementing-a-cancel-routine.md)

[在取消 Irp 时应考虑事项](points-to-consider-when-canceling-irps.md)

 

 




