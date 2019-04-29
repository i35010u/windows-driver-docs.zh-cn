---
title: 在并行设备上设置属性
description: 在并行设备上设置属性
ms.assetid: 10df9a1b-99ec-46b1-b515-10fb20fe2aed
keywords:
- 并行设备 WDK，属性
- 属性 WDK 并行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b0d430a405c113f99b0ad4c307e88464ef490da
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370941"
---
# <a name="setting-attributes-on-a-parallel-device"></a>在并行设备上设置属性





客户端使用以下设备控制请求设置并行的设备的指示的操作：

-   [**IOCTL\_PAR\_设置\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff544103)初始化并行设备。

-   [**IOCTL\_串行\_设置\_超时**](https://msdn.microsoft.com/library/windows/hardware/ff544126)设置并行的设备的超时。

-   [**IOCTL\_PAR\_设置\_读取\_地址**](https://msdn.microsoft.com/library/windows/hardware/ff544107)设置 ECP 或 EPP 读取并行设备地址 （通道）。

-   [**IOCTL\_PAR\_设置\_编写\_地址**](https://msdn.microsoft.com/library/windows/hardware/ff544115)设置 ECP 或 EPP 写地址 （通道） 并行设备。

 

 




