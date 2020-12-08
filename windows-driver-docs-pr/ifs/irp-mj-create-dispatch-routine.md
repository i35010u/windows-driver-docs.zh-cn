---
title: IRP_MJ_CREATE 调度例程
description: IRP_MJ_CREATE 调度例程
keywords:
- IRP_MJ_CREATE
- 安全 WDK 文件系统，添加安全检查
- 安全检查 WDK 文件系统，IRP_MJ_CREATE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b5fadc4805e32800a5cbe29c0acb4bfff3d43a3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830533"
---
# <a name="irp_mj_create-dispatch-routine"></a>IRP \_ MJ \_ 创建调度例程


Windows 安全检查的主要部分发生在 [**IRP \_ MJ \_ 创建**](./irp-mj-create.md) 调度例程中。 这是因为 Windows 安全模型的大部分与访问验证相关。 访问验证结果作为此操作的结果而创建的句柄的一部分存储。 后续操作按照此时计算的权限进行验证。

如果文件或目录打开后对该文件的访问权限发生了更改，则 IRP MJ CREATE 操作期间提供的原始访问权限将 \_ \_ 继续有效。 这些访问权限与句柄相关联，因此只要该句柄仍然存在，则在该句柄下授予的访问控制后续操作。

本节包括下列主题：

[检查 IRP \_ MJ CREATE 的遍历特权 \_](checking-for-traverse-privilege-on-irp-mj-create.md)

[检查 IRP \_ MJ CREATE 上的其他特殊 \_ 情况](checking-for-other-special-cases--on-irp-mj-create.md)

[在 IRP \_ MJ CREATE 上添加审核 \_](adding-auditing-on-irp-mj-create.md)

[对 IRP \_ MJ CREATE 上的访问控制列表的管理 \_](management-of-access-control-lists-on-irp-mj-create.md)

[将安全性分配给 IRP \_ MJ CREATE 上的新文件 \_](assigning-security-to-a-new-file-on-irp-mj-create.md)

[处理 IRP \_ MJ CREATE 的 \_ 配额](handling-quotas-on-irp-mj-create.md)

 

