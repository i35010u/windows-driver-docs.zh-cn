---
title: IRP_MJ_CREATE 上访问控制列表的管理
description: IRP_MJ_CREATE 上访问控制列表的管理
ms.assetid: 07b35931-8e20-4789-b2ef-14c6195b817f
keywords:
- IRP_MJ_CREATE
- 访问控制列表 WDK 文件系统
- 安全检查 WDK 的文件系统，IRP_MJ_CREATE
- ACL WDK 的文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42bca29a7bf3d44c9f148dc747e1410e91591782
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554264"
---
# <a name="management-of-access-control-lists-on-irpmjcreate"></a>访问控制管理列出了在 IRP\_MJ\_创建


## <span id="ddk_management_of_access_control_lists_on_irp_mj_create_if"></span><span id="DDK_MANAGEMENT_OF_ACCESS_CONTROL_LISTS_ON_IRP_MJ_CREATE_IF"></span>


有许多其他与安全相关问题，可以在文件系统中加以解决。 例如，在磁盘上的访问控制列表的管理是一个主要的安全问题。 考虑到安全信息可能是相同的数千个文件，它是通常适用于文件系统，从而实现安全描述符的共享模型。 因此，使用相同的安全描述符的所有文件都共享的安全描述符的单个磁盘上 （和可能是内存） 副本。 NTFS 文件系统使用此模型。

其他选项会为文件系统缓存结果。 虽然严格来说不与安全相关，是一定要认识到安全操作，可以将大量成本添加到普通的操作，如打开的文件。 因此，从上一操作的安全结果缓存可以允许文件系统，以依赖于以前的决策。 例如，可能同时授予新的调用中请求访问以前授予的同一个用户在同一文件的子集。 当然，添加任何此类机制的风险是添加 bug，允许不正确的访问的可能性。 请务必确保任何安全性实现进行全面测试，以确保它按预期方式工作。

 

 




