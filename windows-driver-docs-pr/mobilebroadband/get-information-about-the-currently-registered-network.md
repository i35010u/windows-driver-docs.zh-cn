---
title: 获取当前已注册网络的信息
description: 获取当前已注册网络的信息
ms.assetid: 94321933-fc93-4203-8de1-e715d66fd1e3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92b5c3ce071303c696e8c82705eb10efe7eea4ac
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381471"
---
# <a name="get-information-about-the-currently-registered-network"></a>获取当前已注册网络的信息


可以获取的数据类、 服务提供程序 ID 和移动宽带设备当前已注册到的网络的名称。 若要执行此操作，请使用[ **RegisteredDataClass**](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandNetwork#Windows_Networking_NetworkOperators_MobileBroadbandNetwork_RegisteredDataClass)， [ **RegisteredProviderId**](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandNetwork#Windows_Networking_NetworkOperators_MobileBroadbandNetwork_RegisteredProviderId)，并[ **RegisteredProviderName** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandNetwork#Windows_Networking_NetworkOperators_MobileBroadbandNetwork_RegisteredProviderName)帐户当前的网络对象的属性。

例如：

``` syntax
var myNetwork = myNetworkAccountObject.currentNetwork
if (myNetwork != null && myNetwork.registeredDataClass == DataClasses.LteAdvanced)
{
  // user is connected to an LTE network
}
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 Api 的常见任务](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






