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
- 资源管理器对象 WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7a99a4897b5eb225b524af70fe8057c464ae107
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373409"
---
# <a name="resource-manager-objects"></a>资源管理器对象


*资源管理器对象*表示资源管理器。 每个资源管理器必须调用[ **ZwCreateResourceManager** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreateresourcemanager)进入 KTM 注册自身。

KTM 提供了一套[资源管理器对象例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)内核模式资源管理器可以调用。 KTM 还提供了一组类似的用户模式下用户模式应用程序可以调用的例程。 有关用户模式下例程的详细信息，请参阅 Microsoft Windows SDK。

KTM 创建资源管理器对象，当资源管理器调用**ZwCreateResourceManager**。

[TP 组件](understanding-tps-components.md)可以调用[ **ZwOpenResourceManager** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntopenresourcemanager)打开附加到资源管理器对象的句柄。 但是，大多数 TP 设计不需要其他打开的句柄。

资源管理器关闭其对象的句柄资源管理器通过调用[ **ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)。 如果最后一个句柄已关闭，并且如果资源管理器仍有尚未提交的事务的登记，KTM 发送事务\_通知\_回滚通知到的交易记录的所有资源管理器与这些登记相关联。

在最后一个句柄已关闭并且 KTM 已释放其对该对象的所有引用之后，操作系统将删除对象。

 

 




