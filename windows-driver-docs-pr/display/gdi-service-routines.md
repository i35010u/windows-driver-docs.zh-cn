---
title: GDI 服务例程
description: GDI 服务例程
ms.assetid: ca4fbb84-33a8-498f-8549-c8aaf87429fd
keywords:
- GDI WDK Windows 2000 显示中，服务例程
- 图形驱动程序 WDK Windows 2000 显示中，服务例程
- 绘制 WDK GDI，服务例程
- 服务例程 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b34b364e71ce14a20b06de2f7707141c80acd4a4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374636"
---
# <a name="gdi-service-routines"></a>GDI 服务例程


## <span id="ddk_gdi_service_routines_gg"></span><span id="DDK_GDI_SERVICE_ROUTINES_GG"></span>


GDI 导出多个服务例程，其名称具有窗体 **Eng * * * Xxx*。 该驱动程序动态链接到*win32k.sys*直接访问这些例程。 GDI 服务例程包括图面上的管理，呈现模拟和路径，调色板、 字体和文本服务。 中详细地讨论了这些服务[GDI 支持服务](gdi-support-services.md)。

 

 





