---
title: 连接配置文件 API
description: 连接配置文件 API
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8595fc21cc314d91f6683acf6a0955e39fcbf7b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782476"
---
# <a name="connection-profile-api"></a>连接配置文件 API


连接配置文件 API 是 [**system.net.networkinformation**](/uwp/api/Windows.Networking.Connectivity.NetworkInformation)的一部分，可为建立的网络连接提供连接、使用情况和数据计划信息。 可以使用 [**MobileBroadbandAccount**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount) API 来检索与给定移动帐户关联的连接配置文件。 通过连接配置文件 API，移动宽带应用可以在移动宽带接口上查询网络连接的多个属性，包括以下各项：

-   [**GetNetworkConnectivityLevel**](/uwp/api/Windows.Networking.Connectivity.ConnectionProfile#Windows_Networking_Connectivity_ConnectionProfile_GetNetworkConnectivityLevel) 指示网络是否已连接，以及网络是否提供 internet 连接。

-   [**GetSignalBars**](/uwp/api/Windows.Networking.Connectivity.ConnectionProfile#Windows_Networking_Connectivity_ConnectionProfile_GetSignalBars) 指示用于连接的 Windows UI 当前显示的信号栏数。

-   [**GetNetworkUsageAsync**](/uwp/api/Windows.Networking.Connectivity.ConnectionProfile#Windows_Networking_Connectivity_ConnectionProfile_GetNetworkUsageAsync_Windows_Foundation_DateTime_Windows_Foundation_DateTime_Windows_Networking_Connectivity_DataUsageGranularity_Windows_Networking_Connectivity_NetworkUsageStates_) 为连接配置文件提供发送的字节数、接收的字节数和连接时间。

此 API 还包括一个状态更改事件，该事件在操作员接口上的连接发生更改时通知应用程序。 有关 [**NetworkStatusChanged**](/uwp/api/Windows.Networking.Connectivity.NetworkInformation#Windows_Networking_Connectivity_NetworkInformation_NetworkStatusChanged) 事件的详细信息，请参阅 [**NetworkStatusChangedEventHandler 委托**](/uwp/api/windows.networking.connectivity.networkstatuschangedeventhandler)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的列表](list-of-mobile-broadband-windows-runtime-apis.md)

[网络信息示例](/samples/browse/)

[**NetworkStatusChangedEventHandler 委托**](/uwp/api/windows.networking.connectivity.networkstatuschangedeventhandler)

