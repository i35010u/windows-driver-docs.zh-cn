---
title: 防护带裁剪
description: 防护带裁剪
ms.assetid: bd4ebd97-c948-4219-95a5-f7c6ca45f792
keywords:
- Direct3D WDK Windows 2000 显示、 防止外剪辑
- 保护带剪辑 WDK Direct3D
- 剪辑 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5099f27c057810350bda7afdc5f341a12fe67f14
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323750"
---
# <a name="guard-band-clipping"></a>防护带裁剪


## <span id="ddk_guard_band_clipping_gg"></span><span id="DDK_GUARD_BAND_CLIPPING_GG"></span>


该驱动程序发出信号，它支持防护外剪辑时字段 GUID\_D3DExtendedCaps GUID [ **DdGetDriverInfo**](https://msdn.microsoft.com/library/windows/hardware/ff549404)。 保护带是一个矩形，可能大于视区 （和甚至呈现器目标），到哪些顶点可以剪切自动驱动程序。 Microsoft Direct3D 剪辑代码剪辑添加到此矩形上而不是视区。 通过允许驱动程序来指定可能很大的防护外矩形，减少了生成由于剪辑的新顶点的需求。 一个示例是，只要屏幕 x 和 y 坐标落在范围内通过最多允许 2047年-2048 可以正确呈现的硬件设备。

防护外剪辑也是有益的抗锯齿功能的硬件，因为筛选器区域可以扩展呈现图面范围之外。 这将减少筛选错误可能会造成如果就此而言地理剪辑基元。

若要执行正确的剪辑，驱动程序传递的视区信息。 这将指定的应用程序所需的几何图形来剪辑到的实际视区。 驱动程序编写人员不希望实现防护外剪辑可以忽略此信息。 建议的驱动程序不使用此数据以实现通过剪刀剪辑或屏蔽操作，因为这些很可能要慢于让执行剪辑的 Direct3D。

 

 





