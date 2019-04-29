---
title: 处理帐户到达和删除事件的最佳做法
description: 处理帐户到达和删除事件的最佳做法
ms.assetid: e299a920-a27e-4832-b81d-1562f86f37e2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71fbe660d79a3e47cca3c290e2974ac3a9801d3e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392989"
---
# <a name="best-practices-for-handling-account-arrival-and-removal-events"></a>处理帐户到达和删除事件的最佳做法


可以添加或删除的移动宽带应用程序生命周期内移动宽带帐户。 这可能引起添加或删除硬件、 PIN 解锁或 SIM 交换。 到达或删除的帐户是在许多情况下暂时的。 正确处理这些事件具有重要的意义上的应用程序的可用性。 以下最佳做法适用于处理帐户到达和删除事件：

-   不立即会引发一个错误对话框时删除正在使用的活动帐户。

-   不要假定用户已删除硬件。 睡眠/恢复运行的计算机，具体取决于驱动程序或在总线的行为时，硬件可能暂时不可用。

-   不会释放任何已启动的帐户观察程序对象而无需调用其[**停止**](https://msdn.microsoft.com/library/windows/apps/hh770606)方法第一个。 帐户观察程序，类似于所有 Windows 运行时 (WinRT) 对象，将进行引用计数。 调用[**启动**](https://msdn.microsoft.com/library/windows/apps/hh770604)递增其引用计数 (**停止**递减它)。 如果发布已启动的帐户观察程序，它将保持触发事件，但不能调用**停止**近期发布了对句柄。

-   请记住帐户观察程序对象自动时应用程序获取挂起的 Windows，停止并重新启动该应用程序恢复运行时。 这是相同的结果，就像您的应用程序已调用[**停止**](https://msdn.microsoft.com/library/windows/apps/hh770606)并[**启动**](https://msdn.microsoft.com/library/windows/apps/hh770604)，并生成相同的事件。 使用这些事件将保持最新状态与有重大已暂停的时间段内发生的应用。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[使用移动宽带 Windows 运行时 API 的最佳实践](best-practices-for-using-mobile-broadband-windows-runtime-api.md)

 

 






