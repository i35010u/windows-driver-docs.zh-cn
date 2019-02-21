---
title: 使用额外使用 IRP_MJ_CREATE 操作创建参数
description: 使用额外使用 IRP_MJ_CREATE 操作创建参数
ms.assetid: e32aeec6-1a0a-4d21-8358-89d9fc0a15eb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d41a8d53a8146611820408666cbf34634042a8db
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534858"
---
# <a name="using-extra-create-parameters-with-an-irpmjcreate-operation"></a>使用额外创建的参数与 IRP\_MJ\_创建操作


操作系统使用额外的组件创建具有参数 (ECPs) 若要将其他信息相关联[ **IRP\_MJ\_创建**](https://msdn.microsoft.com/library/windows/hardware/ff548630)文件中的操作。 驱动程序还可以使用 ECPs 来处理或将其他信息与 IRP 相关联\_MJ\_上在以下情况下的文件的创建操作：

-   当内核模式驱动程序调用[ **FltCreateFileEx2** ](https://msdn.microsoft.com/library/windows/hardware/ff541939)或[ **IoCreateFileEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548283)例程，以创建或打开文件

-   当文件系统筛选器驱动程序处理[ **IRP\_MJ\_创建**](https://msdn.microsoft.com/library/windows/hardware/ff548630)文件操作

以下部分介绍如何定义、 附加和使用 ECPs。 以下部分还介绍了操作系统定义 ECPs。

[将 ECPs 附加到 IRP\_MJ\_内核模式驱动程序产生的创建操作](attaching-ecps-to-irp-mj-create-operations-that-a-kernel-mode-driver-o.md)

[使用 ECPs 处理 IRP\_MJ\_中的文件系统筛选器驱动程序的创建操作](using-ecps-to-process-irp-mj-create-operations-in-a-file-system-filter.md)

[用户定义 ECPs](user-defined-ecps.md)

[系统定义 ECPs](system-defined-ecps.md)

 

 




