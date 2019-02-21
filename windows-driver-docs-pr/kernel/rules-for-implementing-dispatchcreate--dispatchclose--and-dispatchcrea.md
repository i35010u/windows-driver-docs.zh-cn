---
title: 规则实现 DispatchCreate、 DispatchClose 和 DispatchCreateClose 例程
description: 规则实现 DispatchCreate、 DispatchClose 和 DispatchCreateClose 例程
ms.assetid: 4ce37675-92a6-41c2-b386-6570c989e56c
keywords:
- 调度例程 WDK 内核，DispatchCreate 例程
- 调度例程 WDK 内核，DispatchClose 例程
- 调度例程 WDK 内核，DispatchCreateClose 例程
- DispatchCreateClose 例程
- DispatchClose 例程
- DispatchCreate 例程
- IRP_MJ_CREATE I/O 函数代码
- IRP_MJ_CLOSE I/O 函数代码
- 创建调度例程 WDK 内核
- 关闭调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5c955c734e5c0a1166f59367f44eaa952004712
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520668"
---
# <a name="rules-for-implementing-dispatchcreate-dispatchclose-and-dispatchcreateclose-routines"></a>规则实现 DispatchCreate、 DispatchClose 和 DispatchCreateClose 例程





在实现时记住以下几点*DispatchCreate*， *DispatchClose*，并*DispatchCreateClose*例程：

-   最小值，该例程必须执行以下步骤：
    1.  设置**状态**字段输入的 IRP I/O 状态块包含相应的 NTSTATUS，通常状态\_成功。
    2.  设置**信息**输入的 IRP I/O 状态块为零的字段。
    3.  调用**IoCompleteRequest** IRP 与和一个*PriorityBoost*的 IO\_否\_增量。
    4.  返回在中设置该 NTSTATUS**状态**IRP 的 I/O 状态块的字段。
-   在最高级别的或中间驱动程序，该例程可能需要执行其他工作来处理创建或关闭请求，具体取决于其设备的或的基础设备，并对设计的驱动程序的性质。

-   若要打开的文件对象，表示逻辑或物理设备的创建请求，最高级别的驱动程序应检查**FileObject.FileName** i/o 堆栈位置，并完成状态 IRP\_成功如果处的 Unicode 字符串**文件名**长度为零。 否则，它应完成状态 IRP\_无效\_参数。

-   仅在下一更高级别驱动程序调用时调用的最低级别的驱动程序的例程**IoAttachDeviceToDeviceStack**， **IoGetDeviceObjectPointer**，或**IoAttachDevice**. 分层驱动程序的链中的最低级别驱动程序频繁地执行所需的创建或关闭请求处理的最小值。

 

 




