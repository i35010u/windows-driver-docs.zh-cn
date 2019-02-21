---
title: 支持电影扫描平板扫描仪
description: 支持电影扫描平板扫描仪
ms.assetid: ee77c2c6-41a2-43dd-90e4-baf902b46f69
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41c6873b33303cca9182bf7a90764b8f010189ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554544"
---
# <a name="flatbed-scanners-that-support-film-scanning"></a>支持电影扫描平板扫描仪





下图说明了支持扫描使用平板辊作为扫描面电影胶片平板扫描仪可能 WIA 项树。 该图还说明了物理设备和文档。

![说明具有仅限辊扫描平板电影扫描仪项树的关系图](images/art-flatbed-film.png)

在上图中，在左侧的树表示扫描程序项树。 在右侧绘制元素到曲线符号表示的物理设备和由此项树表示的文档。

电影扫描程序项始终表示整个电影正在扫描的表面。 有效值的范围内设置应限制为整个扫描图面，以便预览扫描始终显示表示整个电影扫描区域的单一映像。 此单一映像可用于应用程序向用户显示的表示形式的幻灯片或电影的扫描的图面上放置。 单个帧项的范围内设置仅限于物理尺寸为正在扫描的表面电影。 电影项上的平台大小属性[ **WIA\_DPS\_水平\_平台\_大小**](https://msdn.microsoft.com/library/windows/hardware/ff551399)并[ **WIA\_DPS\_垂直\_平台\_大小**](https://msdn.microsoft.com/library/windows/hardware/ff551445)应表示电影扫描区域的物理尺寸。 请注意，电影正在扫描的表面的范围内设置开始 (0，0)，即使它位于中间扫描辊平板。 此编号是平板的因为正在扫描的表面电影有其自己的源，独立于扫描原点。

**请注意**  电影扫描会话中允许使用重叠帧选择区域。

 

 

 




