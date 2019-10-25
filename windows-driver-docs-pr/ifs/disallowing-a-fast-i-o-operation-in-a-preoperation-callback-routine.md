---
title: 禁止在 Preoperation 回调例程中使用快速 i/o 操作
description: 禁止在 Preoperation 回调例程中使用快速 i/o 操作
ms.assetid: 20797d8c-ffcf-46df-b870-839d5c02d2d4
keywords:
- preoperation 回调例程 WDK 文件系统微筛选器，不允许快速 i/o
- 不允许快速 i/o 操作 WDK 文件系统微筛选器
- 快速 i/o 不允许的 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 038301b102db1a7b6111f25340169a8800e152a9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841435"
---
# <a name="disallow-a-fast-io-operation-in-a-preoperation-callback-routine"></a>禁止在 Preoperation 回调例程中使用快速 i/o 操作


## <span id="ddk_disallowing_a_fast_io_operation_in_a_preoperation_callback_routine"></span><span id="DDK_DISALLOWING_A_FAST_IO_OPERATION_IN_A_PREOPERATION_CALLBACK_ROUTINE"></span>


在某些情况下，微筛选器驱动程序可能会选择禁止快速 i/o 操作，而不是完成此操作。 禁止快速 i/o 操作可防止此操作使用快速 i/o 路径。

与完成 i/o 操作一样，不允许快速 i/o 操作对其暂停处理，并将其返回到筛选器管理器。 但是，不允许快速 i/o 操作与完成的操作不同。 如果微筛选器驱动程序不允许由 i/o 管理器颁发的快速 i/o 操作，则 i/o 管理器可能会重新发出与基于 IRP 的等效操作相同的操作。

当微筛选器驱动程序的[**preoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)不允许快速 i/o 操作时，筛选器管理器将执行以下操作：

-   不会将操作发送到当前微筛选器驱动程序下的微筛选器驱动程序、旧筛选器或文件系统。

-   在微筛选器驱动程序实例堆栈中的当前微微筛选器驱动程序之前调用微筛选器驱动程序的[**postoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)。

-   不会为操作（如果有）调用当前微筛选器驱动程序的 postoperation 回调例程。

微筛选器驱动程序不允许快速 i/o 操作，方法是：返回 FLT\_PREOP\_禁止从操作的 preoperation 回调例程\_FASTIO。

由于筛选器管理器自动将此字段设置为状态\_FLT\_不允许\_快速\_IO，因此 preoperation 回调例程不应设置此**字段。**

FLT\_PREOP\_不允许为快速 i/o 操作返回\_FASTIO。 若要确定某一操作是否为快速 i/o 操作，请参阅[**FLT\_is\_FASTIO\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

微筛选器驱动程序无法返回 FLT\_PREOP\_禁止对\_IRP 的\_FASTIO，\_关闭，IRP\_MJ\_卷\_装载，或 IRP\_

 

 




