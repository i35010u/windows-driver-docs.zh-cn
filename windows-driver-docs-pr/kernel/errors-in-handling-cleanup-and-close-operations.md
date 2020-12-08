---
title: 处理清理和关闭操作时出错
description: 处理清理和关闭操作时出错
keywords:
- 可靠性 WDK 内核，错误
- DispatchClose
- DispatchCleanup
- 清理错误 WDK 内核
- 关闭错误 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35f174a70e7ab2a27e94bc707a91d75817d12bd5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785129"
---
# <a name="errors-in-handling-cleanup-and-close-operations"></a>处理清理和关闭操作时出错





某些驱动程序无法区分 [*DispatchCleanup*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 和 [*DispatchClose*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程中所需的任务。 当关闭文件对象的最后一个句柄时，i/o 管理器将调用驱动程序的 *DispatchCleanup* 例程。 当从文件对象中释放最后一个引用时，将调用 *DispatchClose* 例程。 驱动程序不应尝试在附加到文件对象的 *DispatchCleanup* 例程中释放资源，也不应使用其他 *调度* Xxx 例程来释放资源。

调用调度例程时，i/o 管理器将保留对常规 i/o 调用的文件对象的引用。 因此，在调用 *DispatchCleanup* 例程之后、调用 *DispatchClose* 例程之前，驱动程序可以接收文件对象的 i/o 请求。 例如，用户模式调用方可能会在 i/o 管理器请求正在来自其他线程的过程中关闭文件句柄。 如果在 i/o 管理器调用其 *DispatchClose* 例程之前，驱动程序已删除或释放了必需的资源，则指针引用无效，并且可能会出现其他问题。

 

