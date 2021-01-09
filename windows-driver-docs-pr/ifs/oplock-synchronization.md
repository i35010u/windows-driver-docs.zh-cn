---
title: Oplock 同步
description: 介绍筛选器和文件系统如何处理 oplock 同步
ms.date: 01/08/2021
ms.localizationpriority: medium
ms.openlocfilehash: b9509c7024416756bb544af39164eeb0b067d15c
ms.sourcegitcommit: c435386d93f2de662a8e959e9d5b39d61e543ba1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2021
ms.locfileid: "98056184"
---
# <a name="oplock-synchronization"></a>Oplock 同步

 (oplock) 请求 [独占机会锁](oplock-overview.md) 的筛选器和文件系统必须将调用同步到系统提供的 oplock 包。 特别是，对 oplock FSCTRL 例程的调用 (建立 oplock) 时，必须与对 oplock 检查例程的调用同步。 这两组例程的列表包括：

* Oplock FSCTRL 例程：

  * Minifilters： [**FltOplockFsctrl**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)、 [**FltOplockFsctrlEx**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrlex)
  * 旧筛选器和文件系统： [**FsRtlOplockFsctrl**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)、 [**FsRtlOplockFsctrlEx**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrlex)、 [**FsRtlUpperOplockFsctrl**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlupperoplockfsctrl)

* Oplock 检查中断例程：

  * Minifilters： [**FltCheckOplock**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcheckoplock)、  [**FltCheckOplockEx**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcheckoplockex)
  * 旧筛选器和文件系统： [**FsRtlCheckOplock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlcheckoplock)、 [**FsRtlCheckOplockEx**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlcheckoplockex)、 [**FsRtlCheckOplockEx2**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlcheckoplockex2)、 [**FsRtlOplockBreakH**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockbreakh)

处理 oplock 请求时，筛选器和文件系统必须确保以下各项：

* 可能中断 oplock 的 i/o 无法与处理请求并行进行。
* Oplock 请求不能同时出现 oplock 中断确认。

IRP 调用请求为同一文件控制块创建独占 oplock (FCB) 为：

* 在 Create. Options 中设置了 FILE_OPEN_REQUIRING_OPLOCK 位的[IRP_MJ_CREATE](irp-mj-create.md)
* 与 oplock 控件[IRP_MJ_FILE_SYSTEM_CONTROL](irp-mj-file-system-control.md)

下面是 oplock 同步的一些示例：

* 处理 oplock 请求时，文件系统将以独占方式获取一些资源，调用 [**FsRtlOplockFsctrlEx**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrlex)并释放资源。

* 处理 oplock 中断确认时，文件系统会获取共享的同一资源，调用 [**FsRtlOplockFsctrlEx**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrlex)并释放资源。

* 执行 i/o 时，文件系统会获取共享的同一资源，调用 [**FsRtlCheckOplockEx2**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlcheckoplockex2)，执行 i/o，然后释放资源。

  文件系统的文件系统应确保它们在 [**FsRtlCheckUpperOplock**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlcheckupperoplock) 和 [**FsRtlUpperOplockFsctrl**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlupperoplockfsctrl) 的调用之间以类似方式进行同步。
