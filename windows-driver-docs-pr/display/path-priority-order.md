---
title: 路径优先顺序
description: 路径优先顺序
ms.assetid: 93f8f932-fc7b-4420-8b3e-27194937bed5
keywords:
- 连接显示 WDK Windows 7 显示、 CCD 概念、 路径优先顺序
- 连接显示 WDK Windows Server 2008 R2 显示、 CCD 概念、 路径优先顺序
- 配置显示 WDK Windows 7 显示、 CCD 概念、 路径优先顺序
- 配置显示 WDK Windows Server 2008 R2 显示、 CCD 概念、 路径优先顺序
- CCD 概念 WDK Windows 7 显示、 路径优先顺序
- CCD 概念 WDK Windows Server 2008 R2 显示、 路径优先顺序
- 路径优先级排序 WDK Windows 7 显示
- 路径的优先级顺序 WDK Windows Server 2008 R2 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98dcd5a41c8a2f98d02eb6077554d2920402d1b1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352352"
---
# <a name="path-priority-order"></a>路径优先顺序


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533) CCD 函数确定路径中的活动路径数组的指定*pathArray*参数进行排序此类该**SetDisplayConfig**可以提供更高的优先级较低数字数组路径元素的数目。 以下各项影响的顺序：

-   如果[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533)找不到现有的显示配置**SetDisplayConfig**过程中的搜索顺序的最佳模式逻辑中使用此路径的优先级。 因此， **SetDisplayConfig**更有可能满足在自身分辨率较低的优先级路径以外的更高优先级路径。

-   克隆路径中的最高优先级路径是在其计划投掷的路径。 因此，较低优先级路径时可能会出现次要撕裂现象。

-   DirectX 图形内核子系统使用 （连同 GDI 主视图） 的路径优先级来派生子系统将传递给路径重要性该值**ImportanceOrdinal**的成员[ **D3DKMDT\_VIDPN\_存在\_路径**](https://msdn.microsoft.com/library/windows/hardware/ff546647)显示微型端口驱动程序的调用中的结构。 路径重要性值会影响驱动程序的决策，例如，到哪个路径驱动程序应优先考虑中的资源分配。 例如，较低序号路径可能有更好地访问到覆盖层或更高版本的质量控制器。

[ **QueryDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569215) CCD 函数始终返回按优先顺序的路径。 如果 QDC\_所有\_中设置路径标志*标志*参数**QueryDisplayConfig**， **QueryDisplayConfig**返回的所有以下路径中的所有活跃的路径组合的非活动状态的路径组合数组*pPathInfoArray*参数指定。

 

 





