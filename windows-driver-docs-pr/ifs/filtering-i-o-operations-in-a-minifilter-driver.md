---
title: 筛选微筛选器驱动程序中的 I/O 操作
description: 筛选微筛选器驱动程序中的 I/O 操作
keywords:
- preoperation 回调例程 WDK 文件系统微筛选器，指导原则
- postoperation 回调例程 WDK 文件系统微筛选器，指导原则
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 077cf52b41fd7eafdd66c65256263c0751d6b785
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837265"
---
# <a name="filtering-io-operations-in-a-minifilter-driver"></a>筛选微筛选器驱动程序中的 I/O 操作


## <span id="ddk_filtering_io_operations_in_a_minifilter_driver_if"></span><span id="DDK_FILTERING_IO_OPERATIONS_IN_A_MINIFILTER_DRIVER_IF"></span>


下面的列表介绍了几个用于在文件系统微筛选器驱动程序中筛选特定类型的 i/o 操作的准则：

-   IRP MJ CREATE 的 [**preoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback) \_ \_ 无法查询或设置文件、流或流句柄的上下文，因为在预先创建的时间，如果尚未确定要创建的任何) ，则文件或流 (。

-   IRP MJ CLOSE 的 [**postoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback) \_ \_ 不能设置或查询文件、流或流句柄的上下文，因为与这些项关联的系统内部结构将在调用关闭后例程之前被释放。

-   微筛选器驱动程序不得失败 IRP \_ mj \_ 清除或 irp \_ mj \_ 关闭操作。 这些操作可以挂起、返回到筛选器管理器或已完成，状态为 " \_ 成功"。 但是，preoperation 回调例程永远不能使这些操作失败。

-   微筛选器驱动程序无法注册 IRP MJ 关闭的 postoperation 回调例程 \_ \_ 。

 

