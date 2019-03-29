---
title: 使用工作项
description: 使用工作项
ms.assetid: 4617A33F-9026-45FF-9CC2-7215423E6D35
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50401156ec31dbf5cbb9c8e4d7182b78af3783bd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564030"
---
# <a name="using-work-items"></a>使用工作项


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

工作项是一个驱动程序中执行的任务[ *OnWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/hh463909)事件回调函数。 这些函数以异步方式运行。

UMDF 驱动程序通常使用工作项，如果[ *OnInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/hh463902)必须执行其他处理，而不会中断服务请求 (ISR) 的执行，因为可能会中断行由多个设备共享。

通常情况下，驱动程序的[ *OnInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/hh463902)回调函数创建一个工作项对象，并将其添加到系统的工作项队列。 随后，线程池线程取消排队对象和调用的工作项[ *OnWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/hh463909)回调函数。

## <a name="setting-up-a-work-item"></a>设置工作项


若要设置的工作项，您的驱动程序必须：

1.  创建工作项。

    驱动程序调用[ **IWDFDevice3::CreateWorkItem** ](https://msdn.microsoft.com/library/windows/hardware/hh451213)若要创建工作项对象，并标识[ *OnWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/hh463909)回调将处理工作项的函数。

2.  存储有关工作项的信息。

    通常情况下，驱动程序使用的工作项对象的上下文内存来存储有关任务的信息的[ *OnWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/hh463909)应执行的回调函数。 当*OnWorkItem*调用回调函数，它可以通过访问此上下文内存中检索信息。 有关如何分配和访问上下文的内存的信息，请参阅[**IWDFObject::AssignContext**](https://msdn.microsoft.com/library/windows/hardware/ff560208)。

3.  将工作项添加到系统的工作项队列。

    驱动程序调用[ **IWDFWorkItem::Enqueue**](https://msdn.microsoft.com/library/windows/hardware/hh463883)，这将驱动程序的工作项添加到工作项队列。

当您的驱动程序调用[ **IWDFDevice3::CreateWorkItem**](https://msdn.microsoft.com/library/windows/hardware/hh451213)，它可能会根据需要提供的父对象 （例如设备对象或队列对象）。 当系统中删除该对象时，它还会删除与对象关联的任何现有工作项。

## <a name="using-the-workitem-callback-function"></a>使用工作项回调函数


工作项已添加到工作项队列后，它保留在队列中直到系统工作线程变为可用。 系统工作线程从队列中移除工作项，然后调用驱动程序的 OnWorkItem 回调函数，将工作项对象作为输入传递。

通常情况下，OnWorkItem 回调函数将执行以下步骤：

1.  通过访问工作项对象的上下文内存来获取有关工作项的驱动程序所提供的信息。
2.  执行指定的任务。 如果有必要，请回调函数可以调用[ **IWDFWorkItem::GetParentObject** ](https://msdn.microsoft.com/library/windows/hardware/hh463891)来确定工作项的父对象。
3.  如果该驱动程序将重新排队工作项，指示工作项的句柄现已可供重复使用。

几个的驱动程序可能需要调用[ **IWDFWorkItem::Flush** ](https://msdn.microsoft.com/library/windows/hardware/hh463886)若要刷新工作项队列中的各自的工作项。 如果驱动程序调用**刷新**方法，该方法不返回直到一个工作线程已从工作项队列中删除指定的工作项并调用在驱动程序[ *OnWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/hh463909)回调函数，并*OnWorkItem*回调函数随后已在处理工作项之后返回。

 

 





