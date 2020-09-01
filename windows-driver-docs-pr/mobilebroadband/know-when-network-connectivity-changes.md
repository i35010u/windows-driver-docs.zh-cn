---
title: 了解网络连接何时更改
description: 了解网络连接何时更改
ms.assetid: 2937ba62-16ad-4a81-92e8-62a8bb40d608
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 210d4aaddbbc34c193b27d9bdfe492dea82ccc97
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209835"
---
# <a name="know-when-network-connectivity-changes"></a>了解网络连接何时更改


若要了解何时更改了网络连接，请使用[**MobileBroadbandAccountWatcher**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher)的[**AccountUpdated**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_AccountUpdated)事件：

1.  实例化 [**MobileBroadbandAccountWatcher**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher) 对象。

2.  添加 [**AccountUpdated**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_AccountUpdated) 事件处理程序。

3.  在观察程序上调用 [**Start**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_Start) 。

4.  查询[**AccountUpdated**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_AccountUpdated)事件处理程序中[**MobileBroadbandAccountUpdatedEventArgs**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountUpdatedEventArgs)对象的[**HasNetworkChanged**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountUpdatedEventArgs#Windows_Networking_NetworkOperators_MobileBroadbandAccountUpdatedEventArgs_HasNetworkChanged)属性。

5.  如果网络已更改，请查询当前网络对象的 [**CurrentNetwork**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount#Windows_Networking_NetworkOperators_MobileBroadbandAccount_CurrentNetwork) 属性。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的常见任务](./create-a-mobilebroadbandaccount-object.md)

 

