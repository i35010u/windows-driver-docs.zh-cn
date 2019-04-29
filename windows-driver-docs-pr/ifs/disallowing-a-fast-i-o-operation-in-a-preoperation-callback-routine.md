---
title: 不允许 Preoperation 回调例程中的快速 I/O 操作
description: 不允许 Preoperation 回调例程中的快速 I/O 操作
ms.assetid: 20797d8c-ffcf-46df-b870-839d5c02d2d4
keywords:
- preoperation 回调例程 WDK 文件系统微筛选器，不允许快速 I/O
- 不允许快速 I/O 操作 WDK 文件系统微筛选器
- 快速的 i/o 操作不允许使用 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5746d9e9e187441a5798a4ceab9fdb65615f51f3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359543"
---
# <a name="disallow-a-fast-io-operation-in-a-preoperation-callback-routine"></a>不允许 Preoperation 回调例程中的快速 I/O 操作


## <span id="ddk_disallowing_a_fast_io_operation_in_a_preoperation_callback_routine"></span><span id="DDK_DISALLOWING_A_FAST_IO_OPERATION_IN_A_PREOPERATION_CALLBACK_ROUTINE"></span>


在某些情况下，可以选择微筛选器驱动程序不允许一个快速的 I/O 操作，而无需完成它。 不允许快速 I/O 操作会阻止快速 I/O 路径用来执行操作。

与类似完成某个 I/O 操作，不允许快速 I/O 操作意味着若要暂停上它的处理，并将其返回到筛选器管理器。 但是，不允许快速 I/O 操作是不同于完成它。 如果微筛选器驱动程序不允许的快速 I/O 操作中，已颁发的 I/O 管理器，I/O 管理器可能会重新发出相同的操作的等效基于 IRP 的操作。

当微筛选器驱动程序[ **preoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551109)不允许快速 I/O 操作，筛选器管理器执行以下操作：

-   下面当前微筛选器驱动程序的微筛选器驱动程序、 旧筛选器，或文件系统，则不发送该操作。

-   调用[ **postoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551107)上面微筛选器驱动程序实例堆栈中的当前微筛选器驱动程序的微筛选器驱动程序。

-   如果存在，不会为该操作，调用当前微筛选器驱动程序的 postoperation 回调例程。

微筛选器驱动程序不允许快速 I/O 操作，通过返回 FLT\_PREOP\_禁止\_FASTIO 操作 preoperation 回调例程。

Preoperation 回调例程不应设置的回调数据结构**IoStatus.Status**字段，因为筛选器管理器会自动将此字段设置为状态\_FLT\_禁止\_快速\_IO。

FLT\_PREOP\_禁止\_FASTIO 才会返回用于快速 I/O 操作。 若要确定操作是否是一个快速的 I/O 操作，请参阅[ **FLT\_IS\_FASTIO\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff544645)。

微筛选器驱动程序不能返回 FLT\_PREOP\_禁止\_IRP 的 FASTIO\_MJ\_关闭、 IRP\_MJ\_卷\_装载点或 IRP\_MJ\_卷\_卸除操作。

 

 




