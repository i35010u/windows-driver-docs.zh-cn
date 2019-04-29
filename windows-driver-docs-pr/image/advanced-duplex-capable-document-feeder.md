---
title: 支持高级双工的文档送纸器
description: 支持高级双工的文档送纸器
ms.assetid: 05b91864-7573-4d99-8a03-701d6cdd650b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04351c8218656b32e8f059c368aa63978890b6e4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367099"
---
# <a name="advanced-duplex-capable-document-feeder"></a>支持高级双工的文档送纸器





高级双工扫描允许应用程序单独配置前端并将页设置。

下图说明了支持高级双工和文档送纸器扫描平板扫描仪的 WIA 项树。

![说明支持高级双工和文档送纸器扫描平板扫描仪项树的关系图](images/wia-feeder-tree3.png)

请注意项树中的单独的子项目由表示正面和背面正在扫描的页。 此区别包括分隔不同类别中的[ **WIA\_IPA\_项\_类别**](https://msdn.microsoft.com/library/windows/hardware/ff551581)属性：WIA\_类别\_前端和 WIA\_类别\_返回。 前端和后端项目分别; 设置在执行高级双工的扫描，扫描程序，它们可能设置为不同的值。 但是，即使上的扫描程序是支持的高级双工扫描，不能有只有前端或后项;如果前端或后的项，另一个项目也必须存在。

该驱动程序指示有独立的前端和后端项目的设置 （即，高级的双工扫描是执行） 通过设置高级\_送纸器中的重复标志[ **WIA\_DPS\_文档\_处理\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff551379)属性。

### <a name="scanning"></a>扫描

应用程序导航到要执行文档送纸器扫描的送纸器项。 送纸器项上的 WIA 属性应是通用的前端和后端页面的受支持的属性值的子集。 应用程序可以选择使用两种类型的数据传输 （标准图像采集或文件夹获取） 的影响，将使用哪些文档送纸器设置。

### <a name="standard-image-acquisition"></a>标准图像采集

在标准的采集或非文件夹获取，WIA 送纸器项目属性设置用于前端和后端页面 （与简单的双工和非双工扫描仪型号相同）。

### <a name="folder-image-acquisition"></a>文件夹图像采集

在文件夹获取 WIA 送纸器项的映像设置将被忽略，并改为使用的前端和后端项目的设置。 高级应用程序将文档送纸器传输的单个可配置设置。 上送纸器扫描仪，图像数据始终获取送纸器选择项目，即使子项目 （前端和后端项目）。

 

 




