---
title: 事件信息
description: 事件信息
ms.assetid: e6621b5d-f1af-4021-8832-43f79835a6c1
keywords:
- 目标事件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 247ce0fcbf7430fc22ff069e7733ed41a9baefe5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542728"
---
# <a name="event-information"></a>事件信息


可访问调试会话时，没有*最后一个事件*。 这是导致会话变得可以访问的事件。 *事件目标*是生成的最后一个事件的目标。 当会话变为可访问时，当前的目标设置为事件目标。 返回的最后一个事件的详细信息[ **GetLastEventInformation**](https://msdn.microsoft.com/library/windows/hardware/ff546982)。 返回的最后一个事件并在指令指针在事件发生时的内存中的指令指针[**请求**](https://msdn.microsoft.com/library/windows/hardware/ff554564) operations [**调试\_请求\_获取\_CAPTURED\_事件\_代码\_偏移量**](https://msdn.microsoft.com/library/windows/hardware/ff541561)并[**调试\_请求\_读取\_CAPTURED\_事件\_代码\_流**](https://msdn.microsoft.com/library/windows/hardware/ff541572)。

如果目标是崩溃转储文件，*最后一个事件*是之前创建转储文件所做的最后一个事件。 转储文件中存储此事件，并在引擎它事件回调时生成转储文件获取作为调试目标。

如果目标是内核模式目标且*bug 检查*发生的错误检查代码和相关的参数可在使用[ **ReadBugCheckData**](https://msdn.microsoft.com/library/windows/hardware/ff553517)。

如果目标是用户模式下小型转储，转储文件生成器可以存储的其他事件。 通常情况下，这是导致生成器以保存转储文件的事件。 返回此事件的详细信息[ **GetStoredEventInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff548431)并[**请求**](https://msdn.microsoft.com/library/windows/hardware/ff554564)操作[ **调试\_请求\_目标\_异常\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff541606)， [**调试\_请求\_目标\_异常\_线程**](https://msdn.microsoft.com/library/windows/hardware/ff541623)，并[**调试\_请求\_目标\_异常\_记录**](https://msdn.microsoft.com/library/windows/hardware/ff541616).

转储文件可能包含事件的静态列表。 每个事件表示时间的特定点目标的快照。 返回此列表中的事件数[ **GetNumberEvents**](https://msdn.microsoft.com/library/windows/hardware/ff547906)。 对于列表中的每个事件的说明，请使用[ **GetEventIndexDescription**](https://msdn.microsoft.com/library/windows/hardware/ff546630)。 若要将事件设置为当前事件的此列表中，使用方法[ **SetNextEventIndex**](https://msdn.microsoft.com/library/windows/hardware/ff556737); 在调用[ **WaitForEvent**](https://msdn.microsoft.com/library/windows/hardware/ff561229)、事件将成为当前事件。 若要确定当前事件的事件列表中，使用[ **GetCurrentEventIndex**](https://msdn.microsoft.com/library/windows/hardware/ff545755)。

 

 





