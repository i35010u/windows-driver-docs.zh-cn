---
title: 管理 IRP_MJ_CREATE 上的访问控制列表
description: 管理 IRP_MJ_CREATE 上的访问控制列表
keywords:
- IRP_MJ_CREATE
- 访问控制列表 WDK 文件系统
- 安全检查 WDK 文件系统，IRP_MJ_CREATE
- ACL WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a745800bde849d7ce5068174c2f7192ac94126e8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828758"
---
# <a name="management-of-access-control-lists-on-irp_mj_create"></a>对 IRP \_ MJ CREATE 上的访问控制列表的管理 \_


## <span id="ddk_management_of_access_control_lists_on_irp_mj_create_if"></span><span id="DDK_MANAGEMENT_OF_ACCESS_CONTROL_LISTS_ON_IRP_MJ_CREATE_IF"></span>


文件系统中还有许多其他与安全相关的问题。 例如，管理磁盘上的访问控制列表是一个主要的安全问题。 如果安全信息可能与数千个文件相同，则文件系统为安全描述符实现共享模型通常是很有用的。 因此，使用同一安全描述符的所有文件共享单个磁盘上 (，可能会在内存中) 安全描述符的副本。 NTFS 文件系统使用此模型。

其他选项将用于文件系统缓存结果。 尽管并非严格地与安全性相关，但必须认识到安全操作可能会给普通操作（如打开文件）带来巨大的代价。 因此，缓存来自以前操作的安全结果可以允许文件系统依赖于以前的决定。 例如，请求之前授予同一文件中的同一用户的访问子集的新调用可能会被立即授予。 当然，添加任何此类机制的风险就是添加 bug 的可能性，这将导致不正当的访问。 务必确保对安全实现进行全面测试，以确保其按预期方式工作。

 

 




