---
title: 将额外的 Create 参数与 IRP_MJ_CREATE 操作一起使用
description: 将额外的 Create 参数与 IRP_MJ_CREATE 操作一起使用
ms.assetid: e32aeec6-1a0a-4d21-8358-89d9fc0a15eb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9db0913111c33f163e8e07004df19a49ce7102f7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840938"
---
# <a name="using-extra-create-parameters-with-an-irp_mj_create-operation"></a>将额外的 Create 参数与 IRP\_MJ 一起使用\_创建操作


操作系统的组件使用额外的 create parameters （ECPs）将附加信息与[**IRP\_MJ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)文件上的 create 操作相关联。 在以下情况下，驱动程序还可以使用 ECPs 来处理或关联 IRP\_MJ\_创建操作的其他信息：

-   当内核模式驱动程序调用[**FltCreateFileEx2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefileex2)或[**IoCreateFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefileex)例程来创建或打开该文件时

-   文件系统筛选器驱动程序处理[**IRP\_MJ 时\_创建**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)文件的操作

以下各节介绍了如何定义、附加和使用 ECPs。 以下各节还介绍了操作系统定义的 ECPs。

[将 ECPs 附加到 IRP\_MJ\_创建内核模式驱动程序生成的操作](attaching-ecps-to-irp-mj-create-operations-that-a-kernel-mode-driver-o.md)

[使用 ECPs 在文件系统筛选器驱动程序中处理 IRP\_MJ\_创建操作](using-ecps-to-process-irp-mj-create-operations-in-a-file-system-filter.md)

[用户定义的 ECPs](user-defined-ecps.md)

[系统定义的 ECPs](system-defined-ecps.md)

 

 




