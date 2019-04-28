---
title: 使用 DirectDraw 驱动程序的前几个步骤
description: 使用 DirectDraw 驱动程序的前几个步骤
ms.assetid: 0bb00060-7887-447f-a3c9-394ae5ac84db
keywords:
- 绘制 WDK DirectDraw，DirectDraw 驱动程序
- DirectDraw WDK Windows 2000 显示，DirectDraw 驱动程序
- DirectDraw 驱动程序 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cedcc900ae4de2ff7ff05059d6053ade2e6c1b55
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327915"
---
# <a name="first-steps-for-directdraw-drivers"></a>使用 DirectDraw 驱动程序的前几个步骤


## <span id="ddk_first_steps_for_directdraw_drivers_gg"></span><span id="DDK_FIRST_STEPS_FOR_DIRECTDRAW_DRIVERS_GG"></span>


若要开始实现 DirectDraw 功能的好方法是修改现有驱动程序。 如果没有驱动程序可用，启动 DirectDraw 部分的 Windows Driver Kit (WDK) 中的示例代码和获取驱动程序初始化，锁，以及 flip 工作。 从该基本功能，可以这样将提高显示性能添加更强大的功能。

DirectDraw 要求的最低驱动程序功能是能够锁定、 解锁和翻转图面。 假设在硬件支持相关的操作，驱动程序支持还应添加为 blts （包括透明 blts，对于在游戏中的速度非常重要），拉伸，并覆盖，对视频播放而言非常关键。

 

 





