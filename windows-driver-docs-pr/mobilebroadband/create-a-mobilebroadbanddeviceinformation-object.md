---
title: 创建 MobileBroadbandDeviceInformation 对象
description: 创建 MobileBroadbandDeviceInformation 对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7783e4cad01f8cf1fca674c94e929461cfaa01f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782449"
---
# <a name="create-a-mobilebroadbanddeviceinformation-object"></a>创建 MobileBroadbandDeviceInformation 对象


[**MobileBroadbandDeviceInformation**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandDeviceInformation)对象包含一组属性，这些属性可用于获取有关与移动宽带帐户关联的网络设备的移动宽带特定数据 (例如) 固件版本。 只能从 [**MobileBroadbandAccount**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount) 对象获取这些对象。 请注意，单个 **MobileBroadbandAccount** 对象可以与多个 **MobileBroadbandDeviceInformation** 对象相关联，但每次只能有一个。  (如果单个 SIM 卡保存 o 用于区分用户帐户的信息，则会发生这种情况。 ) 

通过获取 [**MobileBroadbandAccount**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount)对象的 [**CurrentDeviceInformation**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount#Windows_Networking_NetworkOperators_MobileBroadbandAccount_CurrentDeviceInformation)属性，可以获得 [**MobileBroadbandDeviceInformation**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandDeviceInformation)对象。 如果在读取 **CurrentDeviceInformation** 属性时没有网络设备， (例如，因为它已被拔出或关闭) ，所以读取此属性将返回 NULL。 因为这可能会随时更改 (例如，用户可以在) 上拔出设备，因此，我们建议你获取属性的副本，测试该属性是否为 NULL，并使用副本。 下面的代码示例演示如何执行此操作：

``` syntax
var myDeviceInfo = myNetworkAccountObject.currentDeviceInformation

if (myDeviceInfo == null)
{
  // no device present, inform user
}
else 
{
  // use myDeviceInfo to get the data you need
}
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的常见任务](./create-a-mobilebroadbandaccount-object.md)

 

