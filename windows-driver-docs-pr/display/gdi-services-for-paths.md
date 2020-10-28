---
title: 路径的 GDI 服务
description: 路径的 GDI 服务
ms.assetid: 8fc51b7e-d787-48ed-a865-528547abefc5
keywords:
- GDI WDK Windows 2000 显示，路径
- 图形驱动程序 WDK Windows 2000 显示，路径
- 绘制 WDK GDI，路径
- 路径 WDK GDI
- 填充路径 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1a4e224333226ef9da4ce6622033b5e6d01630f
ms.sourcegitcommit: a32079f3cc5d564d3b12576f832ed442a6b1a918
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92793488"
---
# <a name="gdi-services-for-paths"></a>路径的 GDI 服务

为了帮助矢量设备填充复杂区域，其驱动程序可以调用下表中列出的用于创建、修改和枚举路径的引擎函数。 驱动程序可以通过 [**PATHOBJ**](/windows/win32/api/winddi/ns-winddi-pathobj) 结构访问路径。

| GDI 路径服务函数 | 说明 |
| ------------------------- | ----------- |
| [**EngCreatePath**](/windows/win32/api/winddi/nf-winddi-engcreatepath) | 为驱动程序的临时使用分配一个路径。 在从其当前的绘图调用返回到 GDI 之前，驱动程序应删除此路径。 |
| [**EngDeletePath**](/windows/win32/api/winddi/nf-winddi-engdeletepath) | 删除由 **EngCreatePath** 函数分配的路径。 |
| [**PATHOBJ_bCloseFigure**](/windows/win32/api/winddi/nf-winddi-pathobj_bclosefigure) | 关闭路径 (用于填充) ，方法是将行绘制回开始点。 |
| [**PATHOBJ_bEnum**](/windows/win32/api/winddi/nf-winddi-pathobj_benum) | 检索路径中的下一个 [**PATHDATA**](/windows/win32/api/winddi/ns-winddi-pathdata) 记录。 每条记录描述全部或部分子路径。 |
| [**PATHOBJ_bEnumClipLines**](/windows/win32/api/winddi/nf-winddi-pathobj_benumcliplines) | 枚举路径中的剪裁线段。 |
| [**PATHOBJ_bMoveTo**](/windows/win32/api/winddi/nf-winddi-pathobj_bmoveto) | 更改 [**PATHOBJ**](/windows/win32/api/winddi/ns-winddi-pathobj)定义路径中的当前位置。 |
| [**PATHOBJ_bPolyBezierTo**](/windows/win32/api/winddi/nf-winddi-pathobj_bpolybezierto) | 在 PATHOBJ 定义的路径中绘制)  (三次曲线的贝塞尔曲线。 |
| [**PATHOBJ_bPolyLineTo**](/windows/win32/api/winddi/nf-winddi-pathobj_bpolylineto) | 在 PATHOBJ 定义的路径中绘制线条。 |
| [**PATHOBJ_vEnumStart**](/windows/win32/api/winddi/nf-winddi-pathobj_venumstart) | 通知 [**PATHOBJ**](/windows/win32/api/winddi/ns-winddi-pathobj) 驱动程序将开始调用 **PATHOBJ_bEnum** 来枚举指定路径中的曲线。 如果重启枚举，则必须调用此函数。 |
| [**PATHOBJ_vEnumStartClipLines**](/windows/win32/api/winddi/nf-winddi-pathobj_venumstartcliplines) | 允许驱动程序要求对 [**CLIPOBJ**](/windows/win32/api/winddi/ns-winddi-clipobj) 剪辑区域进行剪切的行比使用单个矩形更复杂。 |
| [**PATHOBJ_vGetBounds**](/windows/win32/api/winddi/nf-winddi-pathobj_vgetbounds) | 返回路径的边框。 |
