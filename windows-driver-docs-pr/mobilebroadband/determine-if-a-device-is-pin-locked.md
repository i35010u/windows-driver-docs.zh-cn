---
title: 确定设备是否已进行 PIN 锁定
description: 确定设备是否已进行 PIN 锁定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd9bb28bc671946491efb405c94faa6060642ef7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782377"
---
# <a name="determine-if-a-device-is-pin-locked"></a>确定设备是否已进行 PIN 锁定


由于锁定的设备上的订阅信息 (例如，ICCID 或 IMEI) 可能不可用，因此所有锁定的设备都列举了可用的网络帐户。 若要了解帐户是否表示锁定的设备，请查询帐户的 [**CurrentDeviceInformation**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount#Windows_Networking_NetworkOperators_MobileBroadbandAccount_CurrentDeviceInformation)属性的 [**NetworkDeviceStatus**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandDeviceInformation#Windows_Networking_NetworkOperators_MobileBroadbandDeviceInformation_NetworkDeviceStatus)属性。 [**NetworkDeviceStatus**](/uwp/api/Windows.Networking.NetworkOperators.NetworkDeviceStatus)。**DeviceLocked** 指示 PIN 锁，而 **NetworkDeviceStatus**。**DeviceBlocked** 表示 PUK 块。

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

 

