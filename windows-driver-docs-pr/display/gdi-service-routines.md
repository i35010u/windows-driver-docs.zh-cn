---
title: GDI 服务例程
description: GDI 服务例程
keywords:
- GDI WDK Windows 2000 显示，服务例程
- 图形驱动程序 WDK Windows 2000 显示，服务例程
- 绘制 WDK GDI，服务例程
- 服务例程 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45565e228ece3e2caf8e9844e8d482a40c46e553
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793943"
---
# <a name="gdi-service-routines"></a>GDI 服务例程


## <span id="ddk_gdi_service_routines_gg"></span><span id="DDK_GDI_SERVICE_ROUTINES_GG"></span>


GDI 将导出多个服务例程，其名称格式为 **Eng**_Xxx_。 驱动程序动态链接到 *win32k.sys* 以直接访问这些例程。 GDI 服务例程包括 surface management、渲染模拟以及路径、调色板、字体和文本服务。 [GDI 支持服务](gdi-support-services.md)中详细讨论了这些服务。

 

 





