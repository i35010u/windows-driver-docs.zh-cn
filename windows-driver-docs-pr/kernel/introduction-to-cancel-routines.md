---
title: Cancel 例程简介
description: Cancel 例程简介
ms.assetid: 99f7f045-2b2f-4fb3-ac1c-99ab76fa46ad
keywords:
- 有关取消 Irp 取消 Irp，
- 取消例程，有关取消例程
- 关联的 IRP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61d7998252a5806166a61ded20e1ee2e32f0497e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369765"
---
# <a name="introduction-to-cancel-routines"></a>Cancel 例程简介





在其中 Irp 可占用处于挂起状态的无限期的时间间隔必须具有一个或多个任何驱动程序[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)例程。 例如，键盘驱动程序可能会无限期地等待用户按任意键。 相反，如果驱动程序永远不会将队列详细 Irp 比它在 5 分钟内完成，它可能不需要*取消*例程。

假设用户模式线程进行的 I/O 请求，已排队的最高级别的设备驱动程序的调度例程，并请求线程终止而 IRP 排入队列。 Irp 排队代表终止应取消线程。 因此，该驱动程序必须设置驱动程序提供*取消*例程在该队列的每个 IRP。

主 IRP 被取消时，将创建关联的 Irp 的驱动程序必须取消它们。 因为关联的 Irp 不与请求相关联的线程，主 IRP*取消*例程负责取消任何关联 Irp 的主 IRP 被取消时。

数*取消*例程任何驱动程序具有依赖于驱动程序的设计。 一般情况下，驱动程序应具有*取消*例程对在其 I/O 处理的 IRP 可能会持有处于挂起状态的无限期的时间间隔中每个阶段。 此类挂起的 Irp 被称为*保持为可取消状态，* 。

请考虑以下设计原则：

-   分层驱动程序的链中的最高级别的驱动程序必须至少一个*取消*队列 Irp 或否则处于可取消状态持有 Irp 的例程。 它可以有多个*取消*例程，如有必要。

-   较低级别驱动程序在其中 Irp 可以保存在可取消状态相对较长的时间间隔也应具有一个或多个*取消*例程。

-   如果驱动程序管理其自己的 Irp 的内部队列，它应该有一个单独*取消*其队列的每个例程。

一些交互式设备，例如键盘、 鼠标、 声音、 并行类的最高级别的驱动程序和串行驱动程序，必须具有*取消*例程。 一些较低级驱动程序，如持有 Irp 的并行端口驱动程序为排队等待获取一些更高级别的类驱动程序的数量相对较长的时间间隔，还应具有*取消*例程。

大容量存储设备驱动程序，以及中间驱动程序之上，是不可能具有*取消*例程。 若要处理的文件 I/O 请求取消的文件系统驱动程序的责任，虽然 Irp 输入到较低级别的大容量存储驱动程序通常处理完成得太快若要取消。

 

 




