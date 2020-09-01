---
title: 平板扫描仪体系结构
description: 平板扫描仪体系结构
ms.assetid: 04f7df17-d289-44a1-8c2d-7d0fa618cc97
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ac30781b6003eb3ab3d431f2fa55210c00173b6
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188110"
---
# <a name="flatbed-scanner-architecture"></a>平板扫描仪体系结构





如果扫描仪设备支持平板影印扫描，则它应将平板扫描仪项作为第一个子项直接实现为其 WIA 项树中的根项;此外， [**wia \_ IPA \_ ITEM \_ CATEGORY**](./wia-ipa-item-category.md) 属性必须设置为 wia 类别 " \_ 平台" \_ 。 此平台项表示一个可编程数据源，并在从该项目请求数据传输时，从该文档生成一个图像。

仅支持平板影印扫描的扫描程序具有下图所示的 WIA 项树。

![说明带仅限影印扫描的平板扫描仪的示意图](images/art-flatbed1.png)

请注意，WIA 平板项直接位于根项的位置。

支持平板影印扫描和文档送纸器扫描的扫描程序具有如下图所示的 WIA 项树。

![阐释带有自动文档送纸器的平板扫描仪的示意图](images/art-flatbed2.png)

如果实现了其他扫描数据源，WIA 项树中的第一个 nonroot 项必须为 WIA 平板项。 这种安排使 Microsoft Windows XP 和 Windows Me 应用程序更易于支持。 有关与这些操作系统兼容性的详细信息，请参阅 [Windows Me 和 WINDOWS XP 的 WIA 平板扫描仪兼容性](wia-flatbed-scanner-compatibility-for-windows-xp-and-windows-me.md)。

 

