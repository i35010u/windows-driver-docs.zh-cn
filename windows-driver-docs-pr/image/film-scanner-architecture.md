---
title: 底片扫描仪体系结构
description: 底片扫描仪体系结构
ms.assetid: fe3a2c23-a520-4701-8178-02f50ac08767
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f475358de358cdac39d7c8d854eebe67e6e48613
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323452"
---
# <a name="film-scanner-architecture"></a>底片扫描仪体系结构





支持幻灯片或透明度扫描单位的扫描程序设备应在其 WIA 项树实现电影胶片扫描程序项。 此 WIA 项表示的可编程数据源。 生成的映像或从此项请求从位于正在扫描时数据传输的表面的扫描程序的电影胶片图像。 电影扫描程序项应位于直接关闭 WIA 根项，并应包含一个或多个子项 （称为帧）。 *帧*是电影胶片项表示单独选择区域和电影正在扫描的表面上的所选内容区域的位置。 WIA 驱动程序确定是否这些选择可以添加、 删除、 调整大小，或甚至重新定位通过设置的有效值的范围内设置。

以下主题介绍两种类型的电影胶片扫描程序：

[支持电影扫描平板扫描仪](flatbed-scanners-that-support-film-scanning.md)

[专用的电影扫描仪](dedicated-film-scanners.md)

 

 




