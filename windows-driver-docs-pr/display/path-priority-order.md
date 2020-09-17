---
title: 路径优先顺序
description: 路径优先顺序
ms.assetid: 93f8f932-fc7b-4420-8b3e-27194937bed5
keywords:
- 连接显示 WDK Windows 7 显示、CCD 概念、路径优先级顺序
- 连接显示 WDK Windows Server 2008 R2 显示、CCD 概念、路径优先级顺序
- 配置显示 WDK Windows 7 显示、CCD 概念、路径优先级顺序
- 配置显示 WDK Windows Server 2008 R2 显示、CCD 概念、路径优先级顺序
- CCD 概念 WDK Windows 7 显示，路径优先级顺序
- CCD 概念 WDK Windows Server 2008 R2 显示，路径优先级顺序
- 路径优先级顺序 WDK Windows 7 显示
- 路径优先级顺序 WDK Windows Server 2008 R2 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f446fc7f57fa78162fad1354fe1d0e9bc7879258
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716256"
---
# <a name="path-priority-order"></a>路径优先顺序


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

[**SetDisplayConfig**](/windows/win32/api/winuser/nf-winuser-setdisplayconfig) CCD 函数确定*pathArray*参数指定的路径数组中的活动路径按顺序排列，以便**SetDisplayConfig**给出更高优先级的数组路径元素。 以下各项会影响顺序：

-   如果 [**SetDisplayConfig**](/windows/win32/api/winuser/nf-winuser-setdisplayconfig) 找不到现有的显示配置，则 **SetDisplayConfig** 将在搜索顺序中使用最佳模式逻辑期间使用路径优先级。 因此， **SetDisplayConfig** 更有可能满足本地解析的更高优先级路径以外的优先级路径。

-   在克隆的路径中，最高优先级路径是在其上安排翻转的路径。 因此，较低优先级的路径可能会有轻微的撕裂。

-   DirectX 图形内核子系统使用路径优先级 (以及 GDI 主视图) 派生在调用显示小型端口驱动程序的过程中，子系统传递到[**D3DKMDT \_ VIDPN \_ 显示 \_ 路径**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path)结构的**ImportanceOrdinal**成员的路径重要性值。 路径重要性值会影响驱动程序决策（例如），驱动程序应在资源分配中为哪个路径指定优先级。 例如，更低顺序的路径可以更好地访问叠加或更高质量的控制器。

[**QueryDisplayConfig**](/windows/win32/api/winuser/nf-winuser-querydisplayconfig) CCD 函数始终按优先级顺序返回路径。 如果在 \_ QueryDisplayConfig 的 \_ *Flags*参数中设置了 QDC all PATHS 标志**QueryDisplayConfig**，则**QueryDisplayConfig**将在*pPathInfoArray*参数指定的路径数组中的所有活动路径组合后返回所有非活动路径组合。

 

