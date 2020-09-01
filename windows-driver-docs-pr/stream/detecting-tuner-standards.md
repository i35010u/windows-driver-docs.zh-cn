---
title: 检测调谐器标准
description: 检测调谐器标准
ms.assetid: 02923d8f-d8a2-427d-8957-2ffb0273b84a
keywords:
- 格式化 WDK 视频捕获
- 电视信号格式 WDK 视频捕获
- KSPROPERTY_TUNER_STANDARD_MODE
- 检测调谐器标准 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfdd8671acc1be57eeec190505163739b3f83481
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184167"
---
# <a name="detecting-tuner-standards"></a>检测调谐器标准


**本部分仅适用于从 Microsoft Windows Vista 开始的操作系统。**

电视应用程序可能难以从电子收视指南 (EPG) 信息或频道表检索电视信号的实际格式。 视频捕获微型驱动程序应支持 [**KSPROPERTY \_ 调谐器 \_ 标准 \_ 模式**](./ksproperty-tuner-standard-mode.md) 属性，使电视应用程序能够更准确地检测电视信号的格式。 KSPROPERTY \_ 调谐器 \_ 标准 \_ 模式向应用程序指示微型驱动程序是否可以识别电视信号本身的调谐器标准。 如果微型驱动程序支持标准检测，则 KSPROPERTY \_ 调谐器 \_ 标准 \_ 模式属性可以将优化设备设置为自动检测信号中的调谐器标准。 设置自动检测模式后，调谐设备本身可以处理对 [**KSPROPERTY \_ 调谐器 \_ 标准**](./ksproperty-tuner-standard.md) 属性的任何请求。

支持 KSPROPERTY \_ 调谐器标准模式属性的视频捕获 \_ 微型驱动程序 \_ 必须能够自动检测优化设备支持的所有模拟标准。 但数字标准目前是可选的。

对于模拟信号， \_ 最难检测到 (PAL B/PAL \_ NICAM/BTSC) 的音频标准。 但是，如果微型驱动程序中嵌入了适当的逻辑，则微型驱动程序也可以自动检测这些音频标准。

 

