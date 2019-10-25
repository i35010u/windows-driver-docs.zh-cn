---
title: 筛选微筛选器驱动程序中的 I/O 操作
description: 筛选微筛选器驱动程序中的 I/O 操作
ms.assetid: e35944c1-fcc6-44e0-838c-da8d24f95d51
keywords:
- preoperation 回调例程 WDK 文件系统微筛选器，指导原则
- postoperation 回调例程 WDK 文件系统微筛选器，指导原则
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ad47dcef5e8dd67c4e4aad26e6bf99bfc2d87ae
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841396"
---
# <a name="filtering-io-operations-in-a-minifilter-driver"></a>筛选微筛选器驱动程序中的 I/O 操作


## <span id="ddk_filtering_io_operations_in_a_minifilter_driver_if"></span><span id="DDK_FILTERING_IO_OPERATIONS_IN_A_MINIFILTER_DRIVER_IF"></span>


下面的列表介绍了几个用于在文件系统微筛选器驱动程序中筛选特定类型的 i/o 操作的准则：

-   IRP\_MJ\_CREATE 的[**preoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)无法查询或设置文件、流或流句柄的上下文，因为在预先创建的时间，尚未确定将要创建的文件或流（如果有）。

-   IRP\_MJ\_CLOSE 的[**postoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)无法设置或查询文件、流或流句柄的上下文，因为与这些项关联的系统内部结构将在关闭后释放调用例程。

-   微筛选器驱动程序绝不能\_MJ\_清除或 IRP\_MJ\_关闭操作。 这些操作可以挂起、返回到筛选器管理器或已完成，状态\_成功。 但是，preoperation 回调例程永远不能使这些操作失败。

-   微筛选器驱动程序无法为 IRP\_MJ\_关闭注册一个 postoperation 回调例程。

 

 




