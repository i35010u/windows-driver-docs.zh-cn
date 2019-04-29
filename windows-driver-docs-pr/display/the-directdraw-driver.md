---
title: DirectDraw 驱动程序
description: DirectDraw 驱动程序
ms.assetid: 6f3343d6-9544-4389-a753-f4520f21a65c
keywords:
- 绘制 WDK DirectDraw，DirectDraw 驱动程序
- DirectDraw WDK Windows 2000 显示，DirectDraw 驱动程序
- DirectDraw 驱动程序 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35e33481ee4302317d53d11aac5d83cd390e64a1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389891"
---
# <a name="the-directdraw-driver"></a>DirectDraw 驱动程序


## <span id="ddk_the_directdraw_driver_gg"></span><span id="DDK_THE_DIRECTDRAW_DRIVER_GG"></span>


DirectDraw 提供通过 DirectDraw 驱动程序的设备独立性。 DirectDraw 驱动程序是通常由显示硬件制造商提供的特定于设备的接口。 DirectDraw 公开给应用程序的方法，并使用显示器驱动程序的 DirectDraw 部分来直接与硬件工作。 应用程序永远不会直接调用显示器驱动程序。

在 Windows 2000 及更高版本，DirectDraw 驱动程序始终作为 32 位代码来实现。 DirectDraw 驱动程序可以是显示驱动程序或单独的 DLL 定义由驱动程序编写器的专用接口通过显示驱动程序与之通信的一部分。 DirectDraw 文档假定在 Windows 2000 及更高版本，DirectDraw 驱动程序是显示驱动程序的一部分。

DirectDraw 驱动程序包含仅依赖于设备的代码，并不执行任何模拟。 如果函数未执行的硬件，DirectDraw 驱动程序不报告它为硬件功能。 此外，DirectDraw 驱动程序不会验证参数，因为 DirectDraw 运行时执行此调用驱动程序之前。

 

 





