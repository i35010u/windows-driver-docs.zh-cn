---
title: IRP_MJ_CREATE 调度例程
description: IRP_MJ_CREATE 调度例程
ms.assetid: 1ff7915a-0949-43fe-9cf4-c0ad9abf6592
keywords:
- IRP_MJ_CREATE
- 安全 WDK 文件系统，添加安全检查
- 安全检查 WDK 的文件系统，IRP_MJ_CREATE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 274bd9078fc8cc514ba1231c72b5d1e32401148f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380028"
---
# <a name="irpmjcreate-dispatch-routine"></a>IRP\_MJ\_创建调度例程


Windows 安全检查的主要部分发生在内[ **IRP\_MJ\_创建**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)调度例程。 这是因为 Windows 安全模型中的大容量相关访问验证。 访问验证结果将存储为完成此操作后创建的句柄的一部分。 后续操作将验证此时计算的权限。

如果的访问权限的文件更改上打开的文件或目录后，原始的访问权限在 IRP 过程中提供\_MJ\_创建操作仍然有效。 这些访问权限与句柄关联，以便授予访问权限，只要该句柄仍然存在，它控制后续操作。

本部分包括以下主题：

[检查遍历特权 IRP\_MJ\_创建](checking-for-traverse-privilege-on-irp-mj-create.md)

[检查其他特殊情况下在 IRP\_MJ\_创建](checking-for-other-special-cases--on-irp-mj-create.md)

[添加审核 IRP\_MJ\_创建](adding-auditing-on-irp-mj-create.md)

[访问控制管理列出了在 IRP\_MJ\_创建](management-of-access-control-lists-on-irp-mj-create.md)

[将安全分配给新文件在 IRP\_MJ\_创建](assigning-security-to-a-new-file-on-irp-mj-create.md)

[处理 IRP 的配额\_MJ\_创建](handling-quotas-on-irp-mj-create.md)

 

 




