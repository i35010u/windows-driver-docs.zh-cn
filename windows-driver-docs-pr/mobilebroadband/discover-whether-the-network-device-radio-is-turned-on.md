---
title: 发现网络设备无线电是否已打开
description: 发现网络设备无线电是否已打开
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7c292b882175ae3e266ca6ae6839e4ff39b4aa5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788547"
---
# <a name="discover-whether-the-network-device-radio-is-turned-on"></a>发现网络设备无线电是否已打开


如果用户直接从磁贴启动移动宽带应用，移动宽带设备可能会关闭。 如果设备进入节能模式或最终用户打开了飞行模式 (禁用了) 的网络设备，则通常会发生这种情况。 如果是这种情况，则获取相关网络设备的 [**MobileBroadbandDeviceInformation**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandDeviceInformation)对象的 [**CurrentRadioState**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandDeviceInformation#Windows_Networking_NetworkOperators_MobileBroadbandDeviceInformation_CurrentRadioState)属性将返回 [**MobileBroadbandRadioState**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandRadioState)。**Off**。  (或者，如果打开了无线电， **CurrentRadioState** 属性将返回 **MobileBroadbandRadioState**。**On**) 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的常见任务](./create-a-mobilebroadbandaccount-object.md)

 

