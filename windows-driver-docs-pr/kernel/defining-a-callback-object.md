---
title: 定义回调对象
description: 定义回调对象
ms.assetid: 9717795b-dd62-4f17-b931-5ca2b1237e60
keywords:
- 回叫对象 WDK 内核
- 注册回调通知
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb0d080fd4b39458ce9a8b37ff47a7e652a66eb2
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188589"
---
# <a name="defining-a-callback-object"></a>定义回调对象





驱动程序可以创建回调对象，其他驱动程序可以通过该对象请求创建驱动程序所定义的条件的通知。 下图显示了定义回调对象所涉及的步骤。

![说明如何定义回调对象的关系图](images/3crt-cbk.png)

在创建对象之前，驱动程序会调用 [**InitializeObjectAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/nf-wudfwdm-initializeobjectattributes) 来设置其属性。 回调对象的名称必须与系统定义的回调的名称不匹配;它可以具有其创建者认为合适的任何其他属性，通常不 \_ 区分 OBJ 大小写 \_ 。 接下来，该驱动程序调用 [**ExCreateCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-excreatecallback)，并将一个指针传递到已初始化的属性，以及将接收到回调对象的句柄的位置。 它还传递两个布尔值，指示系统是否应在不存在此类命名对象时创建回调对象，以及该对象是否应允许多个已注册的回调例程。

驱动程序定义它将调用注册的回调例程的条件。 条件采用两个参数的形式，每个参数都指向由创建回调的驱动程序定义的参数。 对于驱动程序的客户端，应记录这些条件，以及回调对象的名称以及它请求通知的 IRQL。

当发生回调条件时，驱动程序将调用 [**ExNotifyCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exnotifycallback)，并将其句柄传递给回调对象和两个自变量。 然后，系统会按照它们的注册顺序调用为回调对象注册的所有回调例程，同时传递两个自变量和一个指针，指向注册该例程时提供的上下文。 驱动程序必须调用 **ExNotifyCallback** ， &lt; 其值为 irql = 调度 \_ 级别; 系统将在该驱动程序进行此调用的相同 IRQL 处调用回调例程。

使用回调对象完成所有操作后，创建回调的驱动程序应调用 [**ObDereferenceObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject) 来减小其引用计数，并确保已删除该对象。

 

