---
title: 底片扫描仪体系结构
description: 底片扫描仪体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9fb94fd7964f3010ac77ec7174d744dfc6bbcba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839254"
---
# <a name="film-scanner-architecture"></a>底片扫描仪体系结构





支持幻灯片或透明度扫描单元的扫描仪设备应在其 WIA 项树中实现胶片扫描器项。 此 WIA 项表示可编程数据源。 当从此项请求数据传输时，它将从电影中生成一个图像或图像，并将其放置在扫描仪的电影扫描图面上。 胶片扫描器项应直接位于 WIA 根项的位置，并且应包含一个或多个子项 (称为 "帧") 。 *帧* 是表示各个选择区域以及影片扫描表面上选择区域位置的电影项。 WIA 驱动程序通过设置范围设置的有效值来确定是否可以添加、删除、调整大小或甚至重定位这些选择。

以下主题描述了两种类型的胶片扫描器：

[支持胶片扫描的平板扫描仪](flatbed-scanners-that-support-film-scanning.md)

[专用底片扫描仪](dedicated-film-scanners.md)

 

 




