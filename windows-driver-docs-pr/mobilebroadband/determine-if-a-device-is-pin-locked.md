---
title: 确定设备是否已进行 PIN 锁定
description: 确定设备是否已进行 PIN 锁定
ms.assetid: 7889c049-e8a2-4d69-9e5b-4b4756dcf1b4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72d70b573158a33babbb2668c0df8bdeea386e77
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215294"
---
# <a name="determine-if-a-device-is-pin-locked"></a>确定设备是否已进行 PIN 锁定


由于锁定的设备上的订阅信息 (例如，ICCID 或 IMEI) 可能不可用，因此所有锁定的设备都列举了可用的网络帐户。 若要了解帐户是否表示锁定的设备，请查询帐户的[**CurrentDeviceInformation**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount#Windows_Networking_NetworkOperators_MobileBroadbandAccount_CurrentDeviceInformation)属性的[**NetworkDeviceStatus**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandDeviceInformation#Windows_Networking_NetworkOperators_MobileBroadbandDeviceInformation_NetworkDeviceStatus)属性。 [**NetworkDeviceStatus**](/uwp/api/Windows.Networking.NetworkOperators.NetworkDeviceStatus)。**DeviceLocked** 指示 PIN 锁，而 **NetworkDeviceStatus**。**DeviceBlocked** 表示 PUK 块。

例如：

``` syntax
var account = Windows.Networking.NetworkOperators.MobileBroadbandAccount.createFromNetworkAccountId(accountId);
if (account.currentDeviceInformation.networkDeviceStatus == Windows.Networking.NetworkOperators.NetworkDeviceStatus.DeviceLocked)
{
  // the pin is locked
}
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的常见任务](./create-a-mobilebroadbandaccount-object.md)

 

