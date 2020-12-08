---
title: 有关实现 DispatchCreate、DispatchClose 和 DispatchCreateClose 例程的规则
description: 有关实现 DispatchCreate、DispatchClose 和 DispatchCreateClose 例程的规则
keywords:
- 调度例程 WDK 内核，DispatchCreate 例程
- 调度例程 WDK 内核，DispatchClose 例程
- 调度例程 WDK 内核，DispatchCreateClose 例程
- DispatchCreateClose 例程
- DispatchClose 例程
- DispatchCreate 例程
- IRP_MJ_CREATE i/o 函数代码
- IRP_MJ_CLOSE i/o 函数代码
- 创建调度例程 WDK 内核
- 关闭调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07ff69d254c92bf11c1424ba69115345078d0a72
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839053"
---
# <a name="rules-for-implementing-dispatchcreate-dispatchclose-and-dispatchcreateclose-routines"></a>有关实现 DispatchCreate、DispatchClose 和 DispatchCreateClose 例程的规则





实现 *DispatchCreate*、 *DispatchClose* 和 *DispatchCreateClose* 例程时，请注意以下几点：

-   例程至少必须执行以下操作：
    1.  使用适当的 NTSTATUS （通常为成功状态）设置输入 IRP 的 i/o 状态块的 " **状态** " 字段 \_ 。
    2.  将输入 IRP 的 i/o 状态块的 **信息** 字段设置为零。
    3.  使用 IRP 调用 **IoCompleteRequest** ，并将 *PRIORITYBOOST* 替换为 IO \_ 无 \_ 增量。
    4.  返回在 IRP 的 i/o 状态块的 " **状态** " 字段中设置的 NTSTATUS。
-   在最高级或中间的驱动程序中，例程可能需要执行其他工作来处理创建或关闭请求，具体取决于其设备或基础设备的性质，以及驱动程序的设计。

-   若要创建用于打开表示逻辑或物理设备的文件对象的 create 请求，最高级别的驱动程序应检查 i/o 堆栈位置中的 **FileObject** ，并在 \_ **文件名** 的 Unicode 字符串长度为零时完成 IRP，状态为 "成功"。 否则，它应完成 IRP，其状态为 \_ 无效 \_ 参数。

-   仅当下一级驱动程序调用 **IoAttachDeviceToDeviceStack**、 **plxntb** 或 **IoAttachDevice** 时，才调用最低级别驱动程序的例程。 分层驱动程序链中的最低级别驱动程序通常只执行创建或关闭请求所需的最低处理。

 

 




