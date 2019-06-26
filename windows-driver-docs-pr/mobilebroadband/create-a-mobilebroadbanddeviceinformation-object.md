---
title: 创建 MobileBroadbandDeviceInformation 对象
description: 创建 MobileBroadbandDeviceInformation 对象
ms.assetid: d7f89045-acb5-4b7c-9154-c05e4169490d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b36664a086035e3532717e98696538b8df7a03c1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385534"
---
# <a name="create-a-mobilebroadbanddeviceinformation-object"></a>创建 MobileBroadbandDeviceInformation 对象


一个[ **MobileBroadbandDeviceInformation** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandDeviceInformation)对象包含一组可用于获取有关移动宽带与相关联的网络设备的移动宽带特定于数据的属性帐户 （例如，固件版本）。 你可以获取这些对象从[ **MobileBroadbandAccount** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount)仅对象。 请注意，单个**MobileBroadbandAccount**对象可以是关联与多个**MobileBroadbandDeviceInformation**对象，但一次只有一个。 （这将是单一的 SIM 卡，保存 m n O 使用来区分用户帐户的信息，使用在两个不同的移动宽带设备中。）

您获得[ **MobileBroadbandDeviceInformation** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandDeviceInformation)对象通过获取[ **CurrentDeviceInformation** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount#Windows_Networking_NetworkOperators_MobileBroadbandAccount_CurrentDeviceInformation) 属性[ **MobileBroadbandAccount** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount)对象。 如果没有网络的设备时显示的**CurrentDeviceInformation**读取属性 （例如，因为它已拔掉电源或关闭状态），读取此属性将返回 NULL。 因为这可能会随时更改 （例如，用户可以拔出设备），我们建议获取属性的副本、 测试的是否为 NULL，并使用该副本。 下面的代码示例说明了如何执行此操作：

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

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 Api 的常见任务](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






