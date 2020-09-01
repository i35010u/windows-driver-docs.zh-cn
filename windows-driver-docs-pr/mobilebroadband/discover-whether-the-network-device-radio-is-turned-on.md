---
title: 发现网络设备无线电是否已打开
description: 发现网络设备无线电是否已打开
ms.assetid: deded77d-8810-498c-a5ae-44885189c061
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72352b3cc6e369878b5d844df9f7ae0312959b98
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216624"
---
# <a name="discover-whether-the-network-device-radio-is-turned-on"></a>发现网络设备无线电是否已打开


如果用户直接从磁贴启动移动宽带应用，移动宽带设备可能会关闭。 如果设备进入节能模式或最终用户打开了飞行模式 (禁用了) 的网络设备，则通常会发生这种情况。 如果是这种情况，则获取相关网络设备的[**MobileBroadbandDeviceInformation**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandDeviceInformation)对象的[**CurrentRadioState**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandDeviceInformation#Windows_Networking_NetworkOperators_MobileBroadbandDeviceInformation_CurrentRadioState)属性将返回[**MobileBroadbandRadioState**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandRadioState)。**Off**。  (或者，如果打开了无线电， **CurrentRadioState**属性将返回**MobileBroadbandRadioState**。**On**) 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的常见任务](./create-a-mobilebroadbandaccount-object.md)

 

