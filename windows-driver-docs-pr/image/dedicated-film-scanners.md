---
title: 专用底片扫描仪
description: 专用底片扫描仪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 895867221708229ee2b45aa07e79d3b388c888e1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837249"
---
# <a name="dedicated-film-scanners"></a>专用底片扫描仪





*专用* 胶片扫描器是只执行胶片扫描的扫描程序。 此设备仅具有要从中进行扫描并具有与带有胶片扫描功能的平板扫描仪相同的要求。 也就是说，胶片扫描器项必须存在，并且必须包含扫描区域的物理尺寸。 此区域可以是胶片进纸器扫描仪或模板区域的单个扫描帧。

下图显示了具有多帧扫描的专用胶卷扫描器的 WIA 项目树，并显示了该物理设备和文档。

![说明具有多帧扫描的专用胶卷扫描器的项目树的关系图](images/art-scanner-film.png)

在上图中，左侧的树表示扫描器项树。 绘制到右侧元素的曲线表示此项树表示的物理设备和文档。

下图说明了使用单个帧扫描的专用胶卷扫描程序的 WIA 项树，并显示了该物理设备和文档。

![用单帧扫描说明专用胶片扫描器的项目树的关系图](images/art-scanner-film2.png)

在上图中，左侧的树表示扫描器项树。 绘制到右侧元素的曲线表示此项树表示的物理设备和文档。

必须注意的是，胶卷项必须能够返回胶片扫描表面的表示形式。 对于不了解胶卷扫描的 Microsoft Windows XP 或 Windows Me 编写的应用程序，还应能使用专用的胶片扫描程序进行扫描。

 

 




