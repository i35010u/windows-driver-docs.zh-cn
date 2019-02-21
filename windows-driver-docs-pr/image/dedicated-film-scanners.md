---
title: 专用的电影扫描仪
description: 专用的电影扫描仪
ms.assetid: 1f8b73eb-a81a-4db3-b5be-b0a01a12696a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a83fc8ff94eb9b5b3962b249d82ab9d17cb8f0c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522781"
---
# <a name="dedicated-film-scanners"></a>专用的电影扫描仪





一个*专用*电影扫描程序是执行唯一的电影胶片扫描，扫描程序。 此设备具有仅扫描图面，从要扫描的电影，并且具有扫描功能的电影胶片平板扫描仪与相同的要求。 也就是说，电影胶片扫描程序项必须存在并且必须包含扫描区域的物理尺寸。 此区域可以是电影胶片的送纸器的扫描仪或模板区域的单个扫描范围。

下图说明了专用的电影胶片扫描仪多帧进行扫描的 WIA 项树并显示物理设备和文档。

![说明具有多帧扫描专用的电影扫描仪项树的关系图](images/art-scanner-film.png)

在上图中，在左侧的树表示扫描程序项树。 在右侧绘制元素到曲线符号表示的物理设备和由此项树表示的文档。

下图说明了单个帧进行扫描的专用的电影扫描仪的 WIA 项树并显示物理设备和文档。

![说明具有单帧扫描专用的电影扫描仪项树的关系图](images/art-scanner-film2.png)

在上图中，在左侧的树表示扫描程序项树。 在右侧绘制元素到曲线符号表示的物理设备和由此项树表示的文档。

请务必注意，电影胶片项必须是能够返回正在扫描的表面电影胶片的表示形式。 应用程序编写的 Microsoft Windows XP 或 Windows Me 的电影胶片扫描不知道应仍将能够通过使用专用的电影胶片扫描程序扫描。

 

 




