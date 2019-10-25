---
title: 登记对象
description: 登记对象
ms.assetid: 80e61475-4bb7-4eaa-b9f1-ff95eac9bc77
keywords:
- 登记 WDK KTM
- 登记 WDK KTM，对象
- 资源管理器 WDK KTM，创建登记
- 内核事务管理器 WDK，登记
- KTM WDK，登记
- 登记对象 WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d33be4b8366fb9adc7f90b73ce443278c53b01d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836746"
---
# <a name="enlistment-objects"></a>登记对象


*征用对象*表示资源管理器在事务中的[*登记*](transaction-processing-terms.md#ktm-term-enlistment)。 在资源管理器可以接收有关事务事件的通知之前，资源管理器必须调用[**ZwCreateEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateenlistment)来创建对事务的登记。

KTM 提供一组可供内核模式资源管理器调用的[登记对象例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。 KTM 还提供用户模式应用程序可以调用的一组类似的用户模式例程。 有关用户模式例程的详细信息，请参阅 Microsoft Windows SDK。

当资源管理器调用**ZwCreateEnlistment** ，以在资源管理器已接收的事务中登记（通常来自事务性客户端）时，KTM 会创建一个登记对象。

[TPS 组件](understanding-tps-components.md)可以调用[**ZwOpenEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopenenlistment)来打开登记对象的其他句柄。 但大多数 TPS 设计不需要额外的开放句柄。

资源管理器通过调用[**ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)将其句柄关闭到登记对象。 如果在提交关联的事务对象之前，最后一个句柄已关闭，则 KTM 将发送 TRANSACTION\_将\_回滚通知发送到具有事务登记的所有资源管理器。

当最后一个句柄关闭并且 KTM 释放了对该对象的所有引用后，操作系统将删除该对象。

 

 




