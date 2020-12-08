---
title: 加载 DPXD Alpha 混合图面
description: 加载 DPXD Alpha 混合图面
keywords:
- stride WDK DirectX VA
- alpha-blend 数据加载 WDK DirectX VA
- 混合图片 WDK DirectX VA，alpha-blend 数据加载
- DPXD alpha-混合 surface WDK DirectX VA
- 已解码 PXD alpha-混合图面 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0390d9c5e8aa2089aa4b38570cf749b9264afa27
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792291"
---
# <a name="loading-a-dpxd-alpha-blending-surface"></a>加载 DPXD Alpha 混合图面


## <span id="ddk_loading_a_dpxd_alpha_blending_surface_gg"></span><span id="DDK_LOADING_A_DPXD_ALPHA_BLENDING_SURFACE_GG"></span>


已解码的 PXD (DPXD) alpha 混合图面定义为帧的字节数组。 帧数据的每个字节都包含 4 2 位示例。 每个2位示例用作由突出显示和 DCCMD 所确定的四色表格中的索引 (显示) 数据的控件命令。 DPXD、高光和 DCCMD 的组合结果等效于 IA44 图面，并与用于混合的 16-entry YUV 调色板一起使用。 如果将 DPXD alpha 混合图面视为字节数组，第一个2位示例的索引是 DPXD 数据的第一个字节的最高有效位，下一个示例是在接下来的2位中，第三个示例位于下2位，第四个样本处于最小有效位，第五个示例位于下一个字节的最高有效位等。

DPXD alpha-混合图面可从有关 DVD 的 PXD 信息创建。  (PXD 数据以运行长度编码格式记录在 DVD 上。 ) 从 DVD 上的 PXD 创建 DPXD 时，需要主机解码器才能对 DVD 上的原始 PXD 数据执行运行长度解码。

图面的跨距必须解释为字节跨距（而不是2位样本）。 但是，宽度和高度必须是2位示例单位。

**注意**   DVD 上的 PXD 采用字段结构交错格式。 为 DirectX VA 定义的 DPXD alpha 混合图面不是。 因此，如果要从 DVD PXD 数据中形成 DPXD，则该主机负责隔行扫描两个字段中的数据。

 

有关 DVD 子画面定义和数据字段解释的更多说明，请参阅 *Read-Only 磁盘的 DVD 规范：第3部分-视频规范 (版本1.11，5月) 1999*。

 

 





