---
title: DirectDraw 驱动程序
description: DirectDraw 驱动程序
keywords:
- 绘制 WDK DirectDraw，DirectDraw 驱动程序
- DirectDraw WDK Windows 2000 显示，DirectDraw 驱动程序
- DirectDraw driver WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51e363928f0e632bcc696551c510ec89a31b266d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801803"
---
# <a name="the-directdraw-driver"></a>DirectDraw 驱动程序


## <span id="ddk_the_directdraw_driver_gg"></span><span id="DDK_THE_DIRECTDRAW_DRIVER_GG"></span>


DirectDraw 通过 DirectDraw 驱动程序提供设备独立性。 DirectDraw 驱动程序是通常由显示硬件制造商提供的特定于设备的接口。 DirectDraw 向应用程序公开方法，并使用显示驱动程序的 DirectDraw 部分直接与硬件一起工作。 应用程序永远不会直接调用显示驱动程序。

在 Windows 2000 和更高版本中，DirectDraw 驱动程序始终作为32位代码实现。 DirectDraw 驱动程序可以是显示驱动程序的一部分，也可以是通过驱动程序编写器定义的专用接口与显示驱动程序通信的单独 DLL 的一部分。 DirectDraw 文档假设在 Windows 2000 和更高版本下，DirectDraw 驱动程序是显示驱动程序的一部分。

DirectDraw 驱动程序只包含设备相关的代码，不执行任何仿真。 如果某个函数不是由硬件执行的，则 DirectDraw 驱动程序不会将其报告为硬件功能。 此外，DirectDraw 驱动程序不会验证参数，因为 DirectDraw 运行时在调用驱动程序之前执行此功能。

 

 





