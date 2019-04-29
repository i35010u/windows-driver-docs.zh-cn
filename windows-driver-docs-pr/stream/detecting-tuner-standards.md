---
title: 检测调谐器标准
description: 检测调谐器标准
ms.assetid: 02923d8f-d8a2-427d-8957-2ffb0273b84a
keywords:
- 格式 WDK 视频捕获
- 电视信号格式 WDK 视频捕获
- KSPROPERTY_TUNER_STANDARD_MODE
- 检测调谐器标准 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ab522d1ebec00571ce4db6db2c57ae4f30bc65e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374071"
---
# <a name="detecting-tuner-standards"></a>检测调谐器标准


**本部分仅适用于与 Microsoft Windows Vista 一起启动的操作系统。**

电视应用程序可能很难从电子版收视指南 (EPG) 信息或通道表中检索的电视信号的实际格式。 视频捕获微型驱动程序应支持[ **KSPROPERTY\_调谐器\_标准\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff565909)属性，以允许电视应用程序更准确地检测电视信号的格式。 KSPROPERTY\_调谐器\_标准\_模式将指示应用程序到微型驱动程序是否可以标识从本身的电视信号的调谐器标准。 如果微型驱动程序支持标准检测，KSPROPERTY\_调谐器\_标准\_模式属性可以设置优化设备能够自动检测信号的调谐器标准。 后自动检测设置模式，优化设备本身可以处理任何请求[ **KSPROPERTY\_调谐器\_标准**](https://msdn.microsoft.com/library/windows/hardware/ff565907)属性。

视频捕获微型驱动程序支持 KSPROPERTY\_调谐器\_标准\_模式属性必须是能够自动检测优化设备支持的所有模拟标准。 但是，数字标准是当前可选的。

对于模拟信号，音频标准 (PAL\_B / PAL\_G-NICAM / BTSC) 是最难检测到。 但是，如果合适逻辑嵌入在微型驱动程序，微型驱动程序将能够自动检测这些音频标准过。

 

 




