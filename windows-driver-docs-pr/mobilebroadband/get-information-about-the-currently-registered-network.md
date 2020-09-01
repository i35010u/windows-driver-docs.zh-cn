---
title: 获取当前已注册网络的信息
description: 获取当前已注册网络的信息
ms.assetid: 94321933-fc93-4203-8de1-e715d66fd1e3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0f1ccc9c78dab551124193b7387ebd3900448c5
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217313"
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

 

