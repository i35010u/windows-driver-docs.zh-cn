---
title: 使用 TmXxx 例程
description: 使用 TmXxx 例程
ms.assetid: 8bc763e9-e67c-4810-9901-e5dc1a1cfd0c
keywords:
- 内核事务管理器 WDK，TmXxx 例程
- KTM WDK，TmXxx 例程
- TmXxx 例程，WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbac18629f721e7121cbc4231df8199eeb34f37c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838326"
---
# <a name="using-tmxxx-routines"></a>使用 TmXxx 例程


大多数[KTM 例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)使用 **Zw*Xxx * * * 的命名格式。 这些例程基于处理程序。 也就是说，其输入或输出参数中至少有一个是 KTM 对象的句柄。

KTM 还提供了较少数量的例程，这些例程使用的命名格式为 **Tm*Xxx * * *。 这些例程是基于指针的。 其中至少有一个输入或输出参数是指向 KTM 对象的指针。

某些**Tm * xxx*** 例程重复**Zw * xxx*** 例程。 其他**Tm * xxx*** 例程没有**Zw * xxx*** 等效项。

在大多数情况下，应使用**Zw * Xxx*** 例程。 但在下列情况下应使用**Tm * Xxx*** 例程：

- 资源管理器使用[**ResourceManagerNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ptm_rm_notification)回调例程，该例程提供指向登记对象而不是句柄的指针。

  可以将登记对象指针传递到登记对象的**Tm * Xxx*** 例程。

- 事务处理系统（TPS）组件会对 KTM 执行许多快速调用，这可能会导致系统性能太慢。

  在这种情况下，组件可以调用[**ObReferenceObjectByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)将每个 KTM 对象句柄转换为指针，保存指针，然后将指针传递给**Tm * Xxx*** 例程。 通过此转换，无需在每次调用**Zw * Xxx*** 例程时，在内部将每个句柄转换为指针。

  每次调用**ObReferenceObectByHandle**时，都应包括一个访问掩码，其中包含相应的 KTM 定义的标志。 在 KTM 的创建和打开例程的参考页上介绍了这些标志。

  当你的组件完成使用 KTM 对象时，它必须通过调用[**ObDereferenceObjectDeferDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobjectdeferdelete)或[**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)来取消对该对象的引用。

  -   如果你的组件或驱动程序堆栈中的任何其他组件包含系统提供的任何锁（如自旋锁、互斥体对象或快速 mutex），则必须使用**ObDereferenceObjectDeferDelete** 。

  -   如果确定驱动程序堆栈上的任何组件都不包含系统提供的锁，则可以使用**ObDereferenceObject** 。

  如果组件在持有锁的同时调用**ObDereferenceObject** ，则会发生死锁，因为 KTM 也可能持有对象命名空间的锁。 此外，你的组件可以调用[**TmGetTransactionId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-tmgettransactionid)来更有效地获取事务的标识符，而不是调用[**ZwQueryInformationTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationtransaction)。

- 您必须具有**Zw * Xxx*** 例程不提供的功能。

  具体而言，资源管理器可以调用以下例程：

  -   [**TmEnableCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-tmenablecallbacks)通过回调例程启用通知的异步传递。
  -   [**TmReferenceEnlistmentKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-tmreferenceenlistmentkey)和[**TmDereferenceEnlistmentKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-tmdereferenceenlistmentkey)用于递增或递减登记对象的键引用计数。
  -   [**TmRequestOutcomeEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-tmrequestoutcomeenlistment)请求登记的即时提交或回滚通知。
  -   [**TmIsTransactionActive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-tmistransactionactive)确定事务是否处于活动状态。

 

 




