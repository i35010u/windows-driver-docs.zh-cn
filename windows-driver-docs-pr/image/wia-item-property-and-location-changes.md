---
title: WIA 项属性和位置更改
description: WIA 项属性和位置更改
ms.assetid: 4e8b3d2a-a28c-41d1-9c4b-8d85f28cf904
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34ec6d8a2b6a012f24957661674033f33dc832fb
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190993"
---
# <a name="wia-item-property-and-location-changes"></a>WIA 项属性和位置更改





确保 Windows Vista 和以前操作系统中的应用程序兼容性的最简单方法是在 windows XP 和 Windows Me 位置 *以及* windows Vista 位置中实现 WIA 属性。 通常，为 Windows Vista 编写的 WIA 应用程序只运行在为 windows Vista 添加的 WIA 属性和位置，而为 Windows XP 和 Windows Me 编写的应用程序仅适用于在这些操作系统中定义的 WIA 属性和位置。 如果在这两个位置中实现属性，则为 Windows Vista、Windows XP 和 Windows Me 编写的应用程序将使用相同的属性集实现。

在 Windows Vista 之前的操作系统中，以下 WIA 属性位于支持平板影印扫描的扫描仪驱动程序的根项上。 在 Windows Vista 中，它们位于 "平板" 项上。

-   [**WIA \_DPS \_ 横向 \_ 床 \_ 大小**](./wia-dps-horizontal-bed-size.md) (在 Windows Vista 中称为 [**WIA \_ IPS \_ 最大 \_ 水平 \_ 大小**](./wia-ips-max-horizontal-size.md)) 

-   [**WIA \_DPS \_ 垂直 \_ 床 \_ 大小**](./wia-dps-vertical-bed-size.md) (在 Windows Vista 中称为 [**WIA \_ IPS \_ 最大 \_ \_ 大小**](./wia-ips-max-vertical-size.md)) 

-   [**WIA \_在 Windows Vista 中，DPS \_ 光学 \_ XRES**](./wia-dps-optical-xres.md) (称为 [**WIA \_ IPS \_ \_ XRES**](./wia-ips-optical-xres.md)) 

-   [**WIA \_在 Windows Vista 中，DPS \_ 光学 \_ YRES**](./wia-dps-optical-yres.md) (称为 [**WIA \_ IPS \_ \_ YRES**](./wia-ips-optical-yres.md)) 

-   [**WIA \_在 \_ **](./wia-dps-preview.md) Windows Vista 中，DPS preview (称为 [**WIA \_ ip \_ 预览版**](./wia-ips-preview.md)) 

-   [**WIA \_DPS \_ 显示 \_ 预览 \_ 控件**](./wia-dps-show-preview-control.md) (称为 WIA ip 在 Windows Vista 中 [** \_ \_ 显示 \_ 预览 \_ 控件**](./wia-ips-show-preview-control.md)) 

**注意**   仅支持平板影印扫描或文档送纸器扫描的扫描仪需要重复 WIA 属性。 成对属性具有相同的属性标识符来实现兼容性。 驱动程序可以为 \_ 根项添加 wia DPS \_ *xxx*属性，并 \_ 为其他项目添加 wia ip \_ *xxx* 。

 

 

