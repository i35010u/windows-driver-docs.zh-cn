---
title: 确定哪个 Windows 设备正在连接到网络
description: 确定正在使用哪个 Windows 设备连接到网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fbb7c51e90f4c244128639eb9a4573e8271cfa5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782381"
---
# <a name="determine-which-windows-device-is-being-used-to-connect-to-the-network"></a>确定正在使用哪个 Windows 设备连接到网络

若要确定正在使用哪个 Windows 设备连接到网络，请检查网络适配器的 Windows 设备 ID，该 ID 由帐户的当前网络设备对象的 [**DeviceId**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandDeviceInformation#Windows_Networking_NetworkOperators_MobileBroadbandDeviceInformation_DeviceId) 属性公开。

例如：

``` syntax
account.currentDeviceInformation.deviceId
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的常见任务](./create-a-mobilebroadbandaccount-object.md)

 

