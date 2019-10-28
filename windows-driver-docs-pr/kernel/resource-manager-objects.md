---
title: 资源管理器对象
description: 资源管理器对象
ms.assetid: b44f2035-ee9f-453b-b12d-89ca36a8b280
keywords:
- 资源管理器 WDK KTM，对象
- 资源管理器 WDK KTM
- 资源管理器 WDK KTM，例程
- 内核事务管理器 WDK，资源管理器
- KTM WDK，资源管理器
- resource manager 对象 WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a94ba8f32324703715e2c4393c6ec332b0e7f50
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836420"
---
# <a name="resource-manager-objects"></a>资源管理器对象


*资源管理器对象*表示资源管理器。 每个资源管理器都必须调用[**ZwCreateResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateresourcemanager)来向 KTM 注册自身。

KTM 提供一组可供内核模式资源管理器调用的[资源管理器对象例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。 KTM 还提供用户模式应用程序可以调用的一组类似的用户模式例程。 有关用户模式例程的详细信息，请参阅 Microsoft Windows SDK。

资源管理器调用**ZwCreateResourceManager**时，KTM 会创建资源管理器对象。

[TPS 组件](understanding-tps-components.md)可以调用[**ZwOpenResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopenresourcemanager)来打开资源管理器对象的其他句柄。 但大多数 TPS 设计不需要额外的开放句柄。

资源管理器通过调用[**ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)关闭其对资源管理器对象的句柄。 如果最后一个句柄已关闭，并且如果 resource manager 仍具有对尚未提交的事务的登记，则 KTM 将发送 TRANSACTION\_将\_回滚通知发送给关联的事务的所有资源管理器包含这些登记。

当最后一个句柄关闭并且 KTM 释放了对该对象的所有引用后，操作系统将删除该对象。

 

 




