---
title: 检索 MobileBroadbandAccount 的 ConnectionProfile 对象
description: 检索 MobileBroadbandAccount 的 ConnectionProfile 对象
ms.assetid: 7e612aa5-1627-4ada-971a-a1d04eafeb81
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa7ae18126e29fa4a4339ab4be10699e20934497
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212209"
---
# <a name="retrieve-connectionprofile-objects-for-a-mobilebroadbandaccount"></a>检索 MobileBroadbandAccount 的 ConnectionProfile 对象


[**ConnectionProfile**](/uwp/api/Windows.Networking.Connectivity.ConnectionProfile)对象包含一组属性和方法，你可以使用这些属性和方法获取已建立的网络连接的连接、使用情况和数据计划信息。 可以使用 [**MobileBroadbandAccount**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount) 对象来检索与移动帐户关联的连接配置文件。 下面的代码示例演示如何执行此操作：

**注意**   所有[**ConnectionProfile**](/uwp/api/Windows.Networking.Connectivity.ConnectionProfile)对象的列表均可从 system.net.networkinformation 检索。 [**GetConnectionProfiles**](/uwp/api/Windows.Networking.Connectivity.NetworkInformation#Windows_Networking_Connectivity_NetworkInformation_GetConnectionProfiles)。

 

``` syntax
var myConnectionProfileList = myNetworkAccountObject.getConnectionProfiles();

if (myConnectionProfileList.length !== 0)
{
  for (var i = 0; i < myConnectionProfileList.length; i++)
  {
    //Display connection profile properties
    var connectivityLevel = myConnectionProfileList[i].getNetworkConnectivityLevel();
    }
  }
else 
{
  // No connection profiles are associated with this mobile broadband account.
}
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的常见任务](./create-a-mobilebroadbandaccount-object.md)

 

