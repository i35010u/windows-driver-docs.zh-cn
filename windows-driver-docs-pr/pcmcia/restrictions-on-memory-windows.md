---
title: Windows 上的内存限制
description: Windows 上的内存限制
ms.assetid: 664320e6-b155-470b-9b86-8b463663961f
keywords:
- PCMCIA WDK 总线，内存窗口
- 内存 Windows WDK PCMCIA 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16b84e26a63ee1d289734355f1640dc9859406eb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382608"
---
# <a name="restrictions-on-memory-windows"></a>Windows 上的内存限制





本部分介绍由 Windows 2000 和更高版本操作系统上的 PCMCIA 卡内存 windows 施加的限制。

当枚举设备所带来的插管理器的请求时，通常指定 PCMCIA 内存卡的资源要求由总线驱动程序。 此外可以在指定特定内存窗口[ **INF DDInstall.LogConfigOverride 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-logconfigoverride-section)设备驱动程序的 INF 文件。 可以为 PCMCIA 内存卡请求最多为两个内存窗口。

 

 





