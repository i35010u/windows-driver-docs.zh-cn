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
ms.openlocfilehash: bf8afd82379cee97f8ffe496211f1271f8a49d6d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829860"
---
# <a name="path-priority-order"></a>路径优先顺序


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

[**SetDisplayConfig**](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig) CCD 函数确定*pathArray*参数指定的路径数组中的活动路径按顺序排列，以便**SetDisplayConfig**给出更高优先级的数组路径元素。 以下各项会影响顺序：

-   如果[**SetDisplayConfig**](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig)找不到现有的显示配置，则**SetDisplayConfig**将在搜索顺序中使用最佳模式逻辑期间使用路径优先级。 因此， **SetDisplayConfig**更有可能满足本地解析的更高优先级路径以外的优先级路径。

-   在克隆的路径中，最高优先级路径是在其上安排翻转的路径。 因此，较低优先级的路径可能会有轻微的撕裂。

-   DirectX 图形内核子系统使用路径优先级（以及 GDI 主视图）来派生子系统传递到 [**D3DKMDT\_VIDPN\_的 ImportanceOrdinal 成员的路径重要性值\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path)对显示微型端口驱动程序的调用中的路径结构。 路径重要性值会影响驱动程序决策（例如），驱动程序应在资源分配中为哪个路径指定优先级。 例如，更低顺序的路径可以更好地访问叠加或更高质量的控制器。

[**QueryDisplayConfig**](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig) CCD 函数始终按优先级顺序返回路径。 如果在**QueryDisplayConfig**的*Flags*参数中设置了 QDC\_所有\_路径标志，则**QueryDisplayConfig**将返回路径数组中所有活动路径组合后面的所有非活动路径组合，*pPathInfoArray*参数指定。

 

 





