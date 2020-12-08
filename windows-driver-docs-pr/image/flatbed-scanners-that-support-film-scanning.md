---
title: 支持底片扫描的平板扫描仪
description: 支持底片扫描的平板扫描仪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3953a5fb83764a095737e79100ade4efe308f65
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808245"
---
# <a name="flatbed-scanners-that-support-film-scanning"></a>支持底片扫描的平板扫描仪





下图显示了平板扫描仪的可能的 WIA 项目树，该树支持使用平板影印作为胶片扫描图面进行胶片扫描。 该图还显示了物理设备和文档。

![说明带仅限影印扫描的平板胶卷扫描仪的项目树的关系图](images/art-flatbed-film.png)

在上图中，左侧的树表示扫描器项树。 绘制到右侧元素的曲线表示此项树表示的物理设备和文档。

胶片扫描器项始终代表整个胶片扫描图面。 范围设置的有效值应限制为整个扫描面，以便预览扫描始终显示代表整个胶片扫描区域的单个图像。 此单个图像适用于向用户显示放置在扫描图面上的幻灯片或电影的表示形式的应用程序。 各个帧项的 "范围" 设置被限制为胶片扫描表面的物理尺寸。 胶片项上的床大小属性： "每 [**\_ \_ 水平 \_ 床 \_ 大小**](./wia-dps-horizontal-bed-size.md) " 和 " [**WIA dps" " \_ \_ 垂直 \_ 床 \_ 大小**](./wia-dps-vertical-bed-size.md) " 应表示胶片扫描区域的物理尺寸。 请注意，胶片扫描表面的 "范围" 设置开始 (0，0) ，即使它位于平板扫描影印中间。 这种编号是因为胶片扫描表面有其自己的原点，而与平板扫描原点无关。

**注意**   影片扫描会话中允许重叠的帧选择区域。

 

 

