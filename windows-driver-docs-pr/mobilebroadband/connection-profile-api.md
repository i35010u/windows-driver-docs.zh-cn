---
title: 连接配置文件 API
description: 连接配置文件 API
ms.assetid: 671b0df6-4f4b-4867-86dd-5eb832d86b4b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1fbc87c916215f58860c323c74e1f3bf8a26287
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360832"
---
# <a name="connection-profile-api"></a>连接配置文件 API


连接配置文件 API，它是一部分的[ **Windows.Networking.Connectivity.NetworkInformation**](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.NetworkInformation)，提供已建立的网络连接的连接、 使用情况和数据计划信息. 可以通过使用来检索与给定的移动帐户相关联的连接配置文件[ **MobileBroadbandAccount** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount) API。 连接配置文件 API 允许你的移动宽带应用以查询移动宽带接口，其中包括上的网络连接的多个属性：

-   [**GetNetworkConnectivityLevel** ](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.ConnectionProfile#Windows_Networking_Connectivity_ConnectionProfile_GetNetworkConnectivityLevel)指示是否已连接网络和网络如果提供 internet 连接。

-   [**GetSignalBars** ](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.ConnectionProfile#Windows_Networking_Connectivity_ConnectionProfile_GetSignalBars)指示当前的信号条显示通过 Windows 用户界面的连接数。

-   [**GetNetworkUsageAsync** ](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.ConnectionProfile#Windows_Networking_Connectivity_ConnectionProfile_GetNetworkUsageAsync_Windows_Foundation_DateTime_Windows_Foundation_DateTime_Windows_Networking_Connectivity_DataUsageGranularity_Windows_Networking_Connectivity_NetworkUsageStates_)提供发送的字节数、 接收，字节数和连接配置文件的连接时间。

此 API 还包括每当操作员的接口上的连接发生更改时通知应用程序的状态更改事件。 有关详细信息[ **NetworkStatusChanged** ](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.NetworkInformation#Windows_Networking_Connectivity_NetworkInformation_NetworkStatusChanged)事件，请参阅[ **NetworkStatusChangedEventHandler 委托**](https://docs.microsoft.com/uwp/api/windows.networking.connectivity.networkstatuschangedeventhandler)。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 Api 的列表](list-of-mobile-broadband-windows-runtime-apis.md)

[网络信息示例](https://go.microsoft.com/fwlink/p/?linkid=227013)

[**NetworkStatusChangedEventHandler delegate**](https://docs.microsoft.com/uwp/api/windows.networking.connectivity.networkstatuschangedeventhandler)

 

 






