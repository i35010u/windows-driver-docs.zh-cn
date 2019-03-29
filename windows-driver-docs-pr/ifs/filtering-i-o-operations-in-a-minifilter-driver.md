---
title: 筛选微筛选器驱动程序中的 I/O 操作
description: 筛选微筛选器驱动程序中的 I/O 操作
ms.assetid: e35944c1-fcc6-44e0-838c-da8d24f95d51
keywords:
- preoperation 回调例程 WDK 文件系统微筛选器，准则
- postoperation 回调例程 WDK 文件系统微筛选器，准则
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60d3dc0f9729f1421a8dc83f06eb6c98589fad92
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564756"
---
# <a name="filtering-io-operations-in-a-minifilter-driver"></a>筛选微筛选器驱动程序中的 I/O 操作


## <span id="ddk_filtering_io_operations_in_a_minifilter_driver_if"></span><span id="DDK_FILTERING_IO_OPERATIONS_IN_A_MINIFILTER_DRIVER_IF"></span>


以下列表介绍了几条准则，用于筛选特定类型的文件系统微筛选器驱动程序中的 I/O 操作：

-   [ **Preoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551109)的 IRP\_MJ\_创建不能查询或设置文件、 流或流句柄的上下文，因为，在预创建时，该文件或这是流 （如果有） 将创建尚未确定。

-   [ **Postoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551107)的 IRP\_MJ\_关闭不能设置或查询上下文的文件、 流或流句柄，因为系统内部结构这些项相关联的也将释放调用后关闭例程之前。

-   微筛选器驱动程序必须永远不会失败 IRP\_MJ\_清除或 IRP\_MJ\_关闭操作。 这些操作可以被挂起，返回到筛选器管理器，或已完成，但状态\_成功。 但是，preoperation 回调例程必须永远不会失败，这些操作。

-   微筛选器驱动程序无法注册 IRP postoperation 回调例程\_MJ\_关闭。

 

 




