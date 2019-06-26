---
title: 将额外的 Create 参数与 IRP_MJ_CREATE 操作配合使用
description: 将额外的 Create 参数与 IRP_MJ_CREATE 操作配合使用
ms.assetid: e32aeec6-1a0a-4d21-8358-89d9fc0a15eb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f529755102f85ed4e142d2d1a76de2347e4dcab3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380270"
---
# <a name="using-extra-create-parameters-with-an-irpmjcreate-operation"></a>使用额外创建的参数与 IRP\_MJ\_创建操作


操作系统使用额外的组件创建具有参数 (ECPs) 若要将其他信息相关联[ **IRP\_MJ\_创建**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)文件中的操作。 驱动程序还可以使用 ECPs 来处理或将其他信息与 IRP 相关联\_MJ\_上在以下情况下的文件的创建操作：

-   当内核模式驱动程序调用[ **FltCreateFileEx2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefileex2)或[ **IoCreateFileEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefileex)例程，以创建或打开文件

-   当文件系统筛选器驱动程序处理[ **IRP\_MJ\_创建**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)文件操作

以下部分介绍如何定义、 附加和使用 ECPs。 以下部分还介绍了操作系统定义 ECPs。

[将 ECPs 附加到 IRP\_MJ\_内核模式驱动程序产生的创建操作](attaching-ecps-to-irp-mj-create-operations-that-a-kernel-mode-driver-o.md)

[使用 ECPs 处理 IRP\_MJ\_中的文件系统筛选器驱动程序的创建操作](using-ecps-to-process-irp-mj-create-operations-in-a-file-system-filter.md)

[用户定义 ECPs](user-defined-ecps.md)

[系统定义 ECPs](system-defined-ecps.md)

 

 




