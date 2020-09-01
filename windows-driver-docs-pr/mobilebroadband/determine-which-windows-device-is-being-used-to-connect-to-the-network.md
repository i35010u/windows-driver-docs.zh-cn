---
title: 确定哪个 Windows 设备正在连接到网络
description: 确定正在使用哪个 Windows 设备连接到网络
ms.assetid: ea9a07cd-ad6e-4c49-aae0-fc9eee9b17c8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 621c92423c8a8112d4d8c9a261a5b48a6eb1b8a4
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215290"
---
# <a name="determine-which-windows-device-is-being-used-to-connect-to-the-network"></a>确定正在使用哪个 Windows 设备连接到网络

若要确定正在使用哪个 Windows 设备连接到网络，请检查网络适配器的 Windows 设备 ID，该 ID 由帐户的当前网络设备对象的 [**DeviceId**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandDeviceInformation#Windows_Networking_NetworkOperators_MobileBroadbandDeviceInformation_DeviceId) 属性公开。

例如：

``` syntax
account.currentDeviceInformation.deviceId
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的常见任务](./create-a-mobilebroadbandaccount-object.md)

 

