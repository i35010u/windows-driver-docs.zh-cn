---
title: 处理帐户到达和删除事件的最佳做法
description: 处理帐户到达和删除事件的最佳做法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c64d13ebea9b058d632d41c030c9bcb78eabe23e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782495"
---
# <a name="best-practices-for-handling-account-arrival-and-removal-events"></a>处理帐户到达和删除事件的最佳做法


移动宽带应用的生存期内可以添加或删除移动宽带帐户。 这可能是由于添加或删除硬件、PIN 解锁或 SIM 交换引起的。 在许多情况下，帐户的到达或删除是暂时性的。 正确处理这些事件对应用程序的可用性有重要影响。 以下最佳实践适用于处理帐户到达和删除事件：

-   删除正在使用的活动帐户时，请勿立即引发错误对话框。

-   不要假设用户已删除硬件。 在计算机睡眠/恢复期间，硬件可能暂时不可用，具体取决于驱动程序或总线的行为。

-   不要首先释放已启动的任何帐户观察程序对象，而无需先调用它们的 [**Stop**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_Stop) 方法。 帐户观察程序（如所有 Windows 运行时 (WinRT) 对象）都是引用计数的。 调用 " [**开始**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_Start) " 会递增其引用计数 (**停止** 递减) 。 如果你发布已启动的帐户观察程序，它将保留触发事件，但你无法对刚刚发布的句柄调用 **停止** 。

-   请记住，当 Windows 挂起应用程序时，帐户观察程序对象会自动停止，并在应用程序恢复时重新启动。 这与你的应用程序调用 [**停止**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_Stop) 和 [**启动**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_Start)相同，并导致相同的事件。 使用这些事件可以使应用程序保持最新状态，使其在挂起期间出现的任何内容都保持最新。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[使用移动宽带 Windows 运行时 API 的最佳做法](best-practices-for-handling-account-arrival-and-removal-events.md)

 

