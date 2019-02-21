---
title: 显示器驱动程序中的透明度
description: 显示器驱动程序中的透明度
ms.assetid: 566706fb-66bd-44f5-b98c-23ed60e27970
keywords:
- 显示驱动程序 WDK Windows 2000，透明度
- 透明度 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3dd2cae2303356336569a9d96815e92e74b6b447
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524148"
---
# <a name="transparency-in-display-drivers"></a>显示器驱动程序中的透明度


## <span id="ddk_transparency_in_display_drivers_gg"></span><span id="DDK_TRANSPARENCY_IN_DISPLAY_DRIVERS_GG"></span>


如果显示硬件支持透明度，显示器驱动程序应实现[ **DrvTransparentBlt**](https://msdn.microsoft.com/library/windows/hardware/ff557283)。

若要减少从视频内存读取的成本，驱动程序应在视频内存中的源和目标的图面时实现此函数。 驱动程序，应让 GDI 处理到视频存储器透明位块传输从系统内存，并让 GDI 处理外延式的位块传输。

 

 





