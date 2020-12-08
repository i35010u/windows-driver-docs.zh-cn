---
title: 禁止在 Preoperation 回调例程中使用快速 i/o 操作
description: 禁止在 Preoperation 回调例程中使用快速 i/o 操作
keywords:
- preoperation 回调例程 WDK 文件系统微筛选器，不允许快速 i/o
- 不允许快速 i/o 操作 WDK 文件系统微筛选器
- 快速 i/o 不允许的 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd564732465258ddb0724401a16b4a4c38969566
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823221"
---
# <a name="disallow-a-fast-io-operation-in-a-preoperation-callback-routine"></a>禁止在 Preoperation 回调例程中使用快速 i/o 操作


## <span id="ddk_disallowing_a_fast_io_operation_in_a_preoperation_callback_routine"></span><span id="DDK_DISALLOWING_A_FAST_IO_OPERATION_IN_A_PREOPERATION_CALLBACK_ROUTINE"></span>


在某些情况下，微筛选器驱动程序可能会选择禁止快速 i/o 操作，而不是完成此操作。 禁止快速 i/o 操作可防止此操作使用快速 i/o 路径。

与完成 i/o 操作一样，不允许快速 i/o 操作对其暂停处理，并将其返回到筛选器管理器。 但是，不允许快速 i/o 操作与完成的操作不同。 如果微筛选器驱动程序不允许由 i/o 管理器颁发的快速 i/o 操作，则 i/o 管理器可能会重新发出与基于 IRP 的等效操作相同的操作。

当微筛选器驱动程序的 [**preoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback) 不允许快速 i/o 操作时，筛选器管理器将执行以下操作：

-   不会将操作发送到当前微筛选器驱动程序下的微筛选器驱动程序、旧筛选器或文件系统。

-   在微筛选器驱动程序实例堆栈中的当前微微筛选器驱动程序之前调用微筛选器驱动程序的 [**postoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback) 。

-   不会为操作（如果有）调用当前微筛选器驱动程序的 postoperation 回调例程。

微筛选器驱动程序不允许快速 i/o 操作，方法是 \_ \_ \_ 从操作的 preoperation 回调例程返回 FLT PREOP 禁止 FASTIO。

由于筛选器管理器自动将此字段设置为 STATUS **IoStatus.Status** \_ FLT \_ 禁止 \_ 快速 \_ IO，preoperation 回调例程不应设置此字段。

FLT \_ PREOP \_ 禁止 \_ FASTIO 只能为快速 i/o 操作返回。 若要确定某一操作是否为快速 i/o 操作，请参阅 [**FLT \_ is \_ FASTIO \_ operation**](/windows-hardware/drivers/ddi/index)。

微筛选器驱动程序无法返回 FLT \_ PREOP 不 \_ 允许 \_ FASTIO 用于 IRP \_ mj \_ 关闭、IRP \_ mj \_ 卷 \_ 装载或 IRP \_ mj \_ 卷 \_ 卸载操作。

 

