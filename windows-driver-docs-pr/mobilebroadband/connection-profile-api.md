---
title: 连接配置文件 API
description: 连接配置文件 API
ms.assetid: 671b0df6-4f4b-4867-86dd-5eb832d86b4b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9072ea925177f66ff01f12bb72ec7aaac7708c0b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214097"
---
# <a name="connection-profile-api"></a>连接配置文件 API


连接配置文件 API 是 [**system.net.networkinformation**](/uwp/api/Windows.Networking.Connectivity.NetworkInformation)的一部分，可为建立的网络连接提供连接、使用情况和数据计划信息。 可以使用 [**MobileBroadbandAccount**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount) API 来检索与给定移动帐户关联的连接配置文件。 通过连接配置文件 API，移动宽带应用可以在移动宽带接口上查询网络连接的多个属性，包括以下各项：

-   [**GetNetworkConnectivityLevel**](/uwp/api/Windows.Networking.Connectivity.ConnectionProfile#Windows_Networking_Connectivity_ConnectionProfile_GetNetworkConnectivityLevel) 指示网络是否已连接，以及网络是否提供 internet 连接。

-   [**GetSignalBars**](/uwp/api/Windows.Networking.Connectivity.ConnectionProfile#Windows_Networking_Connectivity_ConnectionProfile_GetSignalBars) 指示用于连接的 Windows UI 当前显示的信号栏数。

-   [**GetNetworkUsageAsync**](/uwp/api/Windows.Networking.Connectivity.ConnectionProfile#Windows_Networking_Connectivity_ConnectionProfile_GetNetworkUsageAsync_Windows_Foundation_DateTime_Windows_Foundation_DateTime_Windows_Networking_Connectivity_DataUsageGranularity_Windows_Networking_Connectivity_NetworkUsageStates_) 为连接配置文件提供发送的字节数、接收的字节数和连接时间。

此 API 还包括一个状态更改事件，该事件在操作员接口上的连接发生更改时通知应用程序。 有关 [**NetworkStatusChanged**](/uwp/api/Windows.Networking.Connectivity.NetworkInformation#Windows_Networking_Connectivity_NetworkInformation_NetworkStatusChanged) 事件的详细信息，请参阅 [**NetworkStatusChangedEventHandler 委托**](/uwp/api/windows.networking.connectivity.networkstatuschangedeventhandler)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的列表](list-of-mobile-broadband-windows-runtime-apis.md)

[网络信息示例](https://go.microsoft.com/fwlink/p/?linkid=227013)

[**NetworkStatusChangedEventHandler 委托**](/uwp/api/windows.networking.connectivity.networkstatuschangedeventhandler)

 

