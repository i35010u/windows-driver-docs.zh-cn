---
title: 额外的 Create 参数
description: 额外的 Create 参数
ms.assetid: e32aeec6-1a0a-4d21-8358-89d9fc0a15eb
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 33b75ad1f1b487b9ed03047dad491f47f6aabe05
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910452"
---
# <a name="extra-create-parameters"></a>额外的 Create 参数

额外的 create parameters （ECPs）是可包含文件创建附加信息的结构。 创建操作可以有任意数量的 ECPs，它们使用 ECP_LIST 进行附加。 操作系统组件使用 ECPs 将附加信息与文件上的[**IRP_MJ_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)操作相关联。

在以下情况下，驱动程序还可以使用 ECPs 来处理或关联文件上的 IRP_MJ_CREATE 操作的其他信息：

- 当内核模式驱动程序调用[**FltCreateFileEx2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefileex2)或[**IoCreateFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefileex)例程来创建或打开该文件时

- 文件系统筛选器驱动程序处理文件的[**IRP_MJ_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)操作时

以下各节介绍了如何定义、附加和使用 ECPs，并介绍了操作系统定义的 ECPs。

[将 ECPs 附加到内核模式驱动程序发起 IRP_MJ_CREATE 操作](attaching-ecps-to-irp-mj-create-operations-that-a-kernel-mode-driver-o.md)

[使用 ECPs 在文件系统微筛选器驱动程序中处理 IRP_MJ_CREATE 操作](using-ecps-to-process-irp-mj-create-operations-in-a-file-system-minifilter.md)

[用户定义的 ECPs](user-defined-ecps.md)

[系统定义的 ECPs](system-defined-ecps.md)
