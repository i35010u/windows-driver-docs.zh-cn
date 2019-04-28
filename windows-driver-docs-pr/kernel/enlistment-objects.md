---
title: 登记对象
description: 登记对象
ms.assetid: 80e61475-4bb7-4eaa-b9f1-ff95eac9bc77
keywords:
- 登记 WDK KTM
- 登记 WDK KTM，对象
- 资源管理器 WDK KTM，创建登记
- 内核事务管理器 WDK 登记
- KTM WDK 登记
- 登记对象 WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a3bf610ad7d092481c462d9c453532543cb5231
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334052"
---
# <a name="enlistment-objects"></a>登记对象


*登记对象*表示资源管理器[*登记*](transaction-processing-terms.md#ktm-term-enlistment)为事务。 资源管理器资源管理器可以接收有关事务的事件通知之前，必须调用[ **ZwCreateEnlistment** ](https://msdn.microsoft.com/library/windows/hardware/ff566422)创建对事务的登记。

KTM 提供了一套[登记对象例程](https://msdn.microsoft.com/library/windows/hardware/ff544270)内核模式资源管理器可以调用。 KTM 还提供了一组类似的用户模式下用户模式应用程序可以调用的例程。 有关用户模式下例程的详细信息，请参阅 Microsoft Windows SDK。

KTM 创建登记对象资源管理器调用时**ZwCreateEnlistment**资源管理器已收到 （通常是从事务的客户端） 的事务中登记。

[TP 组件](understanding-tps-components.md)可以调用[ **ZwOpenEnlistment** ](https://msdn.microsoft.com/library/windows/hardware/ff567008)打开其他句柄的登记对象。 但是，大多数 TP 设计不需要其他打开的句柄。

资源管理器通过调用关闭其对象的句柄登记[ **ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)。 如果之前已提交的关联的事务对象，最后一个句柄已关闭，KTM 发送事务\_通知\_回滚通知到具有该事务的登记的所有资源管理器。

在最后一个句柄已关闭并且 KTM 已释放其对该对象的所有引用之后，操作系统将删除对象。

 

 




