---
title: 了解网络连接何时更改
description: 了解网络连接何时更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: edf1fe928c481308067dd36d0ce296a3b0561738
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786775"
---
# <a name="know-when-network-connectivity-changes"></a>了解网络连接何时更改


若要了解何时更改了网络连接，请使用 [**MobileBroadbandAccountWatcher**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher)的 [**AccountUpdated**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_AccountUpdated)事件：

1.  实例化 [**MobileBroadbandAccountWatcher**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher) 对象。

2.  添加 [**AccountUpdated**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_AccountUpdated) 事件处理程序。

3.  在观察程序上调用 [**Start**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_Start) 。

4.  查询 [**AccountUpdated**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_AccountUpdated)事件处理程序中 [**MobileBroadbandAccountUpdatedEventArgs**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountUpdatedEventArgs)对象的 [**HasNetworkChanged**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountUpdatedEventArgs#Windows_Networking_NetworkOperators_MobileBroadbandAccountUpdatedEventArgs_HasNetworkChanged)属性。

5.  如果网络已更改，请查询当前网络对象的 [**CurrentNetwork**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount#Windows_Networking_NetworkOperators_MobileBroadbandAccount_CurrentNetwork) 属性。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的常见任务](./create-a-mobilebroadbandaccount-object.md)

 

