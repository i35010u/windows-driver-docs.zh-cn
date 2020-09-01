---
title: 枚举可用的移动宽带帐户
description: 枚举可用的移动宽带帐户
ms.assetid: 6dcf4789-09e8-43d2-9617-a026cbe0dfbb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47b55c85868ac2757fb8323bf768309a459ee258
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216622"
---
# <a name="enumerate-available-mobile-broadband-accounts"></a>枚举可用的移动宽带帐户


可以使用两种方法来枚举网络帐户：轮询或基于事件。

-   **轮询** 移动宽带应用可以使用静态 [**MobileBroadbandAccount. AvailableNetworkAccountIds**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount#Windows_Networking_NetworkOperators_MobileBroadbandAccount_AvailableNetworkAccountIds) 方法轮询可用的网络帐户。 如果应用程序只需要帐户的快照，并且在运行时不需要响应正在添加或删除的帐户，则这是理想之选。

-   **基于事件** 你可以使用 [**MobileBroadbandAccountWatcher**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher) 类来枚举并监视移动宽带帐户的更改。 当应用程序必须响应所做的更改时，基于事件的方法非常理想， (即，在删除当前选择的帐户) 时返回到帐户选择页。 使用此类的过程如下所示：

    1.  实例化 [**MobileBroadbandAccountWatcher**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher) 对象。

    2.  将事件处理程序添加到 [**AccountAdded**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_AccountAdded)、 [**AccountRemoved**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_AccountRemoved)和 [**EnumerationCompleted**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_EnumerationCompleted) 事件。

    3.  调用在观察程序上启动 ( # A1。

    为每个现有的网络帐户调用 [**AccountAdded**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_AccountAdded) 事件处理程序。 枚举所有现有的网络帐户时，将引发 [**EnumerationCompleted**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_EnumerationCompleted) 事件。

    当)  (删除移动宽带硬件或 SIM 时，其他 [**AccountAdded**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_AccountAdded) 和 [**AccountRemoved**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_AccountRemoved) 事件会引发。

**重要提示**   当 Windows 挂起应用程序并在恢复应用程序时重新启动时，帐户观察程序对象会自动停止。 这样做是为了保留电池寿命，因为恢复已挂起的应用程序来处理事件，然后将其重新置于挂起状态，这会导致大量的磁盘活动。 当观察程序停止时，将发生停止事件 (这是在应用程序获取其挂起事件) 之前或之后发生的。 当应用程序恢复时，在该应用程序挂起之前运行的所有观察程序会自动重新启动，从而触发一系列 [**AccountAdded**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_AccountAdded) 事件，这些事件后跟 [**EnumerationCompleted**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_EnumerationCompleted) 事件 (与) [**启动**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_Start) 方法相同的方式。 这使应用程序能够最大程度地获取在挂起期间发生的任何重要内容。

[**MobileBroadbandAccountWatcher**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher) 对象相互独立。 这意味着，不能依赖于报告同一组事件的所有观察程序–作为一个组，它们将报告所有事件。 但是，任何给定的观察程序可能都不会报告任何给定的事件，因为该事件已被其他观察程序使用。 除非有充分的理由，否则每个应用只应使用一个帐户观察程序对象。

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的常见任务](./create-a-mobilebroadbandaccount-object.md)

 

