---
title: 发现网络设备无线电是否已打开
description: 发现网络设备无线电是否已打开
ms.assetid: deded77d-8810-498c-a5ae-44885189c061
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 629538fce62acd6f785fb722104458c2a8f00a02
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380261"
---
# <a name="discover-whether-the-network-device-radio-is-turned-on"></a>发现网络设备无线电是否已打开


如果用户启动的移动宽带应用直接从其磁贴时，移动宽带设备可能已关闭。 如果在设备进入节能模式或最终用户开启飞行模式 （这将禁用的网络设备），通常会发生这种情况。 如果是这样，则获取[ **CurrentRadioState** ](https://msdn.microsoft.com/library/windows/apps/hh770613)属性[ **MobileBroadbandDeviceInformation** ](https://msdn.microsoft.com/library/windows/apps/br207361)对象网络设备有问题将返回[ **MobileBroadbandRadioState**](https://msdn.microsoft.com/library/windows/apps/hh758385)。**关闭**。 (或者，如果打开单选**CurrentRadioState**属性将返回**MobileBroadbandRadioState**。**在**。)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 Api 的常见任务](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






