---
title: 用作应用程序图形语言的 GDI
description: 用作应用程序图形语言的 GDI
ms.assetid: fc824284-0400-47b0-ac4e-ff21e1e0ded9
keywords:
- GDI WDK Windows 2000 显示、 图形的应用程序的语言
- 显示图形驱动程序 WDK Windows 2000，图形的应用程序的语言
- 绘制 WDK GDI，图形的应用程序的语言
- 图形的应用程序 WDK GDI 的语言
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93e0738724ae028f131c93606806b357a771e640
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351188"
---
# <a name="gdi-as-a-graphics-language-for-applications"></a>用作应用程序图形语言的 GDI


## <span id="ddk_gdi_as_a_graphics_language_for_applications_gg"></span><span id="DDK_GDI_AS_A_GRAPHICS_LANGUAGE_FOR_APPLICATIONS_GG"></span>


Win32 GDI 和图形引擎完全独立于设备。 因此，应用程序不需要直接访问硬件。 根据应用程序图形请求，GDI 结合依赖于设备的图形驱动程序提供高质量的图形输出数组的图形设备工作。 打印和显示设备使用相同的 GDI 代码路径。

 

 





