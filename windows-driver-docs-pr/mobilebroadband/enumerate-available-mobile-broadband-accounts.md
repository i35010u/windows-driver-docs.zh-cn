---
title: 枚举可用的移动宽带帐户
description: 枚举可用的移动宽带帐户
ms.assetid: 6dcf4789-09e8-43d2-9617-a026cbe0dfbb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7821be8edbb6231e7dd1301daa95ffcc9fc2301
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554355"
---
# <a name="enumerate-available-mobile-broadband-accounts"></a>枚举可用的移动宽带帐户


有两种方法可用于枚举网络帐户： 轮询或基于事件的。

-   **轮询**移动宽带应用程序可以使用静态轮询可用的网络帐户[ **MobileBroadbandAccount.AvailableNetworkAccountIds** ](https://msdn.microsoft.com/library/windows/apps/hh770608)方法。 这是理想的如果应用程序只需根据帐户的快照，并且不需要在运行时响应帐户正在添加或删除。

-   **基于事件的**可以使用[ **MobileBroadbandAccountWatcher** ](https://msdn.microsoft.com/library/windows/apps/hh770597)类枚举和然后监视对移动宽带帐户更改。 基于事件的方法非常适用于应用程序必须对更改做出响应 （即，返回到帐户选择页删除当前所选的帐户后）。 若要使用此类的过程如下所示：

    1.  实例化[ **MobileBroadbandAccountWatcher** ](https://msdn.microsoft.com/library/windows/apps/hh770597)对象。

    2.  添加到事件处理程序[ **AccountAdded**](https://msdn.microsoft.com/library/windows/apps/hh770599)， [ **AccountRemoved**](https://msdn.microsoft.com/library/windows/apps/hh770600)，并[ **EnumerationCompleted** ](https://msdn.microsoft.com/library/windows/apps/hh770602)事件。

    3.  观察程序上调用 start （）。

    [ **AccountAdded** ](https://msdn.microsoft.com/library/windows/apps/hh770599)为每个现有的网络帐户调用事件处理程序。 枚举的所有现有的网络帐户时[ **EnumerationCompleted** ](https://msdn.microsoft.com/library/windows/apps/hh770602)引发事件。

    其他[ **AccountAdded** ](https://msdn.microsoft.com/library/windows/apps/hh770599)并[ **AccountRemoved** ](https://msdn.microsoft.com/library/windows/apps/hh770600)帐户时所引发的事件可用性发生变化 （即，当移动宽带硬件或者 sim 卡被移除）。

**重要**  帐户观察程序对象自动时应用挂起的 Windows，停止并重新启动时恢复应用程序。 这样做是为了保持电池寿命，因为正在恢复已挂起的应用程序处理事件，然后将其放回处于挂起状态可能会导致大量的磁盘活动。 已停止事件发生时停止观察程序 （发生这种情况可以立即之前或应用程序将获取其正在挂起事件后）。 当应用程序继续时，重新启动之前应用已挂起，会自动为正在运行的所有观察程序，从而触发一系列[ **AccountAdded** ](https://msdn.microsoft.com/library/windows/apps/hh770599)事件后跟[**EnumerationCompleted** ](https://msdn.microsoft.com/library/windows/apps/hh770602)事件 (相同的方式如同[**启动**](https://msdn.microsoft.com/library/windows/apps/hh770604)已调用方法一样)。 这使应用以获取最新状态与有重大已暂停的时间段内发生的。

[**MobileBroadbandAccountWatcher** ](https://msdn.microsoft.com/library/windows/apps/hh770597)对象是相互独立。 这意味着不能依赖于报告的事件-一组作为一组相同的所有观察程序，它们将报告所有事件。 但是，任何给定的观察程序可能不报告任何给定的事件，因为该事件由另一个观察程序。 除非有充分的理由，否则应使用每个应用只有一个帐户观察程序对象。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[移动宽带 Windows 运行时 Api 的常见任务](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






