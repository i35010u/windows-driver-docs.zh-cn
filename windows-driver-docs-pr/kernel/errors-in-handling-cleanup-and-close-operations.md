---
title: 处理清理和关闭操作时出错
description: 处理清理和关闭操作时出错
ms.assetid: 9d449974-99b1-4d38-9bbb-54938d67c23a
keywords:
- 可靠性 WDK 内核错误
- DispatchClose
- DispatchCleanup
- 清理错误 WDK 内核
- 关闭错误 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf9a4344aa5dd9a25948adb638dc145f4809417c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564100"
---
# <a name="errors-in-handling-cleanup-and-close-operations"></a>处理清理和关闭操作时出错





某些驱动程序无法区分中所需的任务[ *DispatchCleanup* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)并[ *DispatchClose* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。 I/O 管理器调用的驱动程序*DispatchCleanup*例程时关闭最后一个句柄的文件对象。 *DispatchClose*文件对象中释放的最后一个引用时调用例程。 驱动程序不应尝试释放资源中的其*DispatchCleanup*连接到的文件对象或其他可能使用的例程*调度*Xxx 例程。

在调用调度例程时，I/O 管理器保存到正常的 I/O 调用的文件对象的引用。 因此，驱动程序可以接收后的文件对象的 I/O 请求其*DispatchCleanup*之前调用例程其*DispatchClose*调用例程。 例如，用户模式下调用方可能会在从另一个线程进行 I/O 管理器请求时关闭文件句柄。 如果该驱动程序已删除或释放之前 I/O 管理器调用必要的资源及其*DispatchClose*例程、 无效的指针的引用以及其他问题可能会发生。

 

 




