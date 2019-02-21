---
title: 定义回调对象
description: 定义回调对象
ms.assetid: 9717795b-dd62-4f17-b931-5ca2b1237e60
keywords:
- 回调对象 WDK 内核
- 注册回调通知
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: abfeb44e7c5e222f7e2f34877dcc8392d0b071d8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555690"
---
# <a name="defining-a-callback-object"></a>定义回调对象





驱动程序可以创建其他驱动程序可以通过其请求创建驱动程序所定义条件的通知的回调对象。 下图显示所涉及步骤中定义的回调对象。

![说明定义回调对象的关系图](images/3crt-cbk.png)

然后再创建该对象，该驱动程序调用[ **InitializeObjectAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff547804)以设置其属性。 回调对象必须具有一个名称，不能与匹配的系统定义的回调; 名称它可以具有任何其他属性其创建者认为适当情况下，通常 OBJ\_用例\_INSENSITIVE。 接下来，驱动程序将调用[ **ExCreateCallback**](https://msdn.microsoft.com/library/windows/hardware/ff544560)，将指针传递到已初始化的属性和在其中以接收回调对象的句柄的某个位置。 它还将两个布尔值，该值指示是否不存在此类命名的对象，但是否对象应允许多个注册的回调例程，系统是否应创建回调对象。

该驱动程序定义的条件，它将为其调用注册的回调例程。 条件采用两个参数的形式，每个都指向一个参数定义由创建回调的驱动程序。 你应记录这些条件，以及回调对象和它请求的客户端驱动程序的通知的 IRQL 的名称。

当回调条件发生时，驱动程序调用[ **ExNotifyCallback**](https://msdn.microsoft.com/library/windows/hardware/ff545489)，将其句柄传递给回调对象和两个参数。 然后，系统调用的所有回调例程注册的回调对象，在其中注册它们，顺序将两个参数和一个指针传递给例程注册时提供的上下文。 该驱动程序必须调用**ExNotifyCallback**在 IRQL &lt;= 调度\_级别; 系统相同的 IRQL 驱动程序所做此调用在调用回调例程。

创建回调的驱动程序已与回调对象完成所有操作后，应调用[ **ObDereferenceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff557724)递减引用计数，并确保该对象是已删除。

 

 




