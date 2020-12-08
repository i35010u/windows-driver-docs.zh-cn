---
title: 获取当前已注册网络的信息
description: 获取当前已注册网络的信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: badea3030798b599732e3e864c5c5be8249e93b2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782341"
---
# <a name="get-information-about-the-currently-registered-network"></a>获取当前已注册网络的信息


可以获取移动宽带设备当前注册到的数据类、服务提供程序 ID 和网络名称。 为此，请使用该帐户的当前网络对象的 [**RegisteredDataClass**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandNetwork#Windows_Networking_NetworkOperators_MobileBroadbandNetwork_RegisteredDataClass)、 [**RegisteredProviderId**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandNetwork#Windows_Networking_NetworkOperators_MobileBroadbandNetwork_RegisteredProviderId)和 [**RegisteredProviderName**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandNetwork#Windows_Networking_NetworkOperators_MobileBroadbandNetwork_RegisteredProviderName) 属性。

例如：

``` syntax
var myNetwork = myNetworkAccountObject.currentNetwork
if (myNetwork != null && myNetwork.registeredDataClass == DataClasses.LteAdvanced)
{
  // user is connected to an LTE network
}
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的常见任务](./create-a-mobilebroadbandaccount-object.md)

 

