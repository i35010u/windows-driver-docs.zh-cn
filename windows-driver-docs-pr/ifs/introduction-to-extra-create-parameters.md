---
title: 额外 Create 参数简介
description: 额外 Create 参数简介
ms.assetid: e32aeec6-1a0a-4d21-8358-89d9fc0a15eb
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 06e6d4f7265eb3e688af1f1e6ddea105720d169c
ms.sourcegitcommit: 2a1c24db881ed843498001493c3ce202c9aa03f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/16/2019
ms.locfileid: "74135161"
---
# <a name="introduction-to-extra-create-parameters"></a>额外 Create 参数简介

额外的 create parameters （ECPs）是可包含文件创建附加信息的结构。 创建操作可以有任意数量的 ECPs，它们使用 ECP_LIST 进行附加。 操作系统组件使用 ECPs 将附加信息与文件上的[**IRP_MJ_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)操作相关联。

在以下情况下，驱动程序还可以使用 ECPs 来处理或关联文件上的 IRP_MJ_CREATE 操作的其他信息：

- 当内核模式驱动程序调用[**FltCreateFileEx2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefileex2)或[**IoCreateFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefileex)例程来创建或打开该文件时

- 文件系统筛选器驱动程序处理文件的[**IRP_MJ_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)操作时

以下各节介绍了如何定义、附加和使用 ECPs。 以下各节还介绍了操作系统定义的 ECPs。

[将 ECPs 附加到内核模式驱动程序发起 IRP_MJ_CREATE 操作](attaching-ecps-to-irp-mj-create-operations-that-a-kernel-mode-driver-o.md)

[使用 ECPs 在文件系统微筛选器中处理 IRP_MJ_CREATE 操作](using-ecps-to-process-irp-mj-create-operations-in-a-file-system-minifilter.md)

[用户定义的 ECPs](user-defined-ecps.md)

[系统定义的 ECPs](system-defined-ecps.md)
