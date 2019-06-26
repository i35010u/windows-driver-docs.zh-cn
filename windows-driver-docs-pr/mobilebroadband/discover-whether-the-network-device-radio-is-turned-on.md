---
title: 发现网络设备无线电是否已打开
description: 发现网络设备无线电是否已打开
ms.assetid: deded77d-8810-498c-a5ae-44885189c061
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d09e6703e7002aa8cdd4e473f28c014e8458bf23
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381480"
---
# <a name="discover-whether-the-network-device-radio-is-turned-on"></a>发现网络设备无线电是否已打开


如果用户启动的移动宽带应用直接从其磁贴时，移动宽带设备可能已关闭。 如果在设备进入节能模式或最终用户开启飞行模式 （这将禁用的网络设备），通常会发生这种情况。 如果是这样，则获取[ **CurrentRadioState** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandDeviceInformation#Windows_Networking_NetworkOperators_MobileBroadbandDeviceInformation_CurrentRadioState)属性[ **MobileBroadbandDeviceInformation** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandDeviceInformation)对象网络设备有问题将返回[ **MobileBroadbandRadioState**](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandRadioState)。**关闭**。 (或者，如果打开单选**CurrentRadioState**属性将返回**MobileBroadbandRadioState**。**在**。)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 Api 的常见任务](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






