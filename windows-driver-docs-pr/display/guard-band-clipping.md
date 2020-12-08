---
title: 防护带裁剪
description: 防护带裁剪
keywords:
- Direct3D WDK Windows 2000 显示，防护频带剪辑
- 保护带剪辑 WDK Direct3D
- 剪辑 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a35adbeefaf36818c324e94fb1703a77591e7a1d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798311"
---
# <a name="guard-band-clipping"></a>防护带裁剪


## <span id="ddk_guard_band_clipping_gg"></span><span id="DDK_GUARD_BAND_CLIPPING_GG"></span>


驱动程序发出信号，指示其在 \_ [**DdGetDriverInfo**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)中的 guid D3DExtendedCaps 防护带区是一个矩形，它可能大于视区 (甚至是呈现器目标) ，可由驱动程序自动剪切顶点。 Microsoft Direct3D 剪裁代码剪辑到此矩形而不是视口。 通过允许驱动程序指定可能较大的防护带矩形，就减少了生成新顶点的需求。 例如，只要屏幕 x 和 y 坐标范围为-2048 到2047，就可以正确呈现硬件设备。

对于抗锯齿式硬件，防护带剪辑也很有用，因为筛选器区域可以在呈现面范围外扩展。 这会减少在将基元裁剪到此区时可能引入的筛选错误。

若要执行正确的剪辑，驱动程序会传递视区信息。 这将指定应用程序需要剪裁到的几何图形的实际视区。 不想实现防护带剪辑的驱动程序编写器可以忽略此信息。 建议驱动程序不要使用此数据来实现通过剪刀或屏蔽操作进行的剪辑，因为这些操作可能比允许 Direct3D 执行剪辑的速度要慢。

 

