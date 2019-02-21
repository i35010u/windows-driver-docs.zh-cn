---
title: 平板扫描仪体系结构
description: 平板扫描仪体系结构
ms.assetid: 04f7df17-d289-44a1-8c2d-7d0fa618cc97
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 002946aa4e4678c1c190969697298dc7ce8053ba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523978"
---
# <a name="flatbed-scanner-architecture"></a>平板扫描仪体系结构





如果扫描程序设备支持平板辊扫描，则它应作为第一个子项目，直接从其 WIA 项树; 中的根项目实现平板扫描仪项此外， [ **WIA\_IPA\_项\_类别**](https://msdn.microsoft.com/library/windows/hardware/ff551581)属性必须设置为 WIA\_类别\_平板。 此平板项表示的可编程数据源，并生成了此项从请求数据传输时当前放置在扫描程序的平板辊的文档中的图像。

支持仅扫描平板辊扫描仪具有下图显示了 WIA 项树。

![说明具有仅限辊扫描平板扫描仪的关系图](images/art-flatbed1.png)

请注意 WIA 平板项所在直接来自根项。

支持平板辊扫描和文档送纸器扫描的扫描仪具有下图显示了 WIA 项树。

![说明与自动文档送纸器平板扫描仪的关系图](images/art-flatbed2.png)

WIA 项树中的第一个非根项必须为 WIA 平板项，如果实现了其他扫描的数据源。 这种部署使得更轻松地支持 Microsoft Windows XP 和 Windows Me 的应用程序。 有关使用这些操作系统的兼容性的详细信息，请参阅[WIA 平板扫描仪兼容性的 Windows Me 和 Windows XP](wia-flatbed-scanner-compatibility-for-windows-xp-and-windows-me.md)。

 

 




