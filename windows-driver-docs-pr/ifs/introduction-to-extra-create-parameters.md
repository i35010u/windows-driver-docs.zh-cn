---
title: 额外 Create 参数简介
description: 额外 Create 参数简介
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 89fb25a912e88612bc79a5fd9f371ede0f8aa4a8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834563"
---
# <a name="introduction-to-extra-create-parameters"></a>额外 Create 参数简介

ECPs)  (额外的 create 参数是可以包含文件创建附加信息的结构。 创建操作可以有任意数量的 ECPs，它们使用 ECP_LIST 进行附加。 操作系统组件使用 ECPs 将附加信息与文件上的 [**IRP_MJ_CREATE**](./irp-mj-create.md) 操作相关联。

在以下情况下，驱动程序还可以使用 ECPs 来处理或关联文件上的 IRP_MJ_CREATE 操作的其他信息：

- 当内核模式驱动程序调用 [**FltCreateFileEx2**](/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefileex2) 或 [**IoCreateFileEx**](/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefileex) 例程来创建或打开该文件时

- 文件系统筛选器驱动程序处理文件的 [**IRP_MJ_CREATE**](./irp-mj-create.md) 操作时

以下各节介绍了如何定义、附加和使用 ECPs。 以下各节还介绍了操作系统定义的 ECPs。

[将 ECP 附加到产生内核模式驱动程序的 IRP_MJ_CREATE 操作](attaching-ecps-to-irp-mj-create-operations-that-a-kernel-mode-driver-o.md)

[在文件系统微驱动程序中使用 ECP 处理 IRP_MJ_CREATE 操作](using-ecps-to-process-irp-mj-create-operations-in-a-file-system-minifilter.md)

[用户定义的 ECPs](user-defined-ecps.md)

[系统定义的 ECPs](system-defined-ecps.md)
