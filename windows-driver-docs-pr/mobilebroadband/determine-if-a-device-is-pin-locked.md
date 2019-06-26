---
title: 确定设备是否已进行 PIN 锁定
description: 确定设备是否已进行 PIN 锁定
ms.assetid: 7889c049-e8a2-4d69-9e5b-4b4756dcf1b4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0d156ab5e78fddff13b61dfb0dbce8b5d7126e3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381513"
---
# <a name="determine-if-a-device-is-pin-locked"></a>确定设备是否已进行 PIN 锁定


已锁定的设备 （例如，ICCID 或 IMEI） 上的订阅信息可能不可用，因为所有锁定的设备枚举可用的网络帐户。 若要了解客户是否表示已锁定的设备，请查询[ **NetworkDeviceStatus** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandDeviceInformation#Windows_Networking_NetworkOperators_MobileBroadbandDeviceInformation_NetworkDeviceStatus)属性[ **CurrentDeviceInformation** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount#Windows_Networking_NetworkOperators_MobileBroadbandAccount_CurrentDeviceInformation)帐户的属性。 [**NetworkDeviceStatus**](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.NetworkDeviceStatus)。**DeviceLocked**指示一个 PIN 锁定，而**NetworkDeviceStatus**。**DeviceBlocked**指示 PUK 块。

例如：

``` syntax
var account = Windows.Networking.NetworkOperators.MobileBroadbandAccount.createFromNetworkAccountId(accountId);
if (account.currentDeviceInformation.networkDeviceStatus == Windows.Networking.NetworkOperators.NetworkDeviceStatus.DeviceLocked)
{
  // the pin is locked
}
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 Api 的常见任务](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






