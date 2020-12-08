---
title: 用作应用程序图形语言的 GDI
description: 用作应用程序图形语言的 GDI
keywords:
- GDI WDK Windows 2000 显示，应用程序的图形语言
- 图形驱动程序 WDK Windows 2000 显示、应用程序的图形语言
- 绘制 WDK GDI，适用于应用程序的图形语言
- 适用于应用程序的图形语言 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60625a376139b1bdeba32945c87063cdb3b2571b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839927"
---
# <a name="gdi-as-a-graphics-language-for-applications"></a>用作应用程序图形语言的 GDI


## <span id="ddk_gdi_as_a_graphics_language_for_applications_gg"></span><span id="DDK_GDI_AS_A_GRAPHICS_LANGUAGE_FOR_APPLICATIONS_GG"></span>


Win32 GDI 和图形引擎完全独立于设备。 因此，应用程序无需直接访问硬件。 根据应用程序图形请求，GDI 将与设备相关图形驱动程序结合使用，以便为图形设备数组提供高质量的图形输出。 打印和显示设备同时使用相同的 GDI 代码路径。

 

 





