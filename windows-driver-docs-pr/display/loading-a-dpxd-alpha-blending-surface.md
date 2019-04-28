---
title: 加载 DPXD Alpha 混合图面
description: 加载 DPXD Alpha 混合图面
ms.assetid: 6b5f62e9-3211-42c2-8168-505983c7814e
keywords:
- stride WDK DirectX VA
- alpha 混合数据加载 WDK DirectX VA
- 混合型的图片 WDK DirectX VA，alpha 混合数据加载
- DPXD alpha 值混合处理面 WDK DirectX VA
- 已解码的 PXD alpha 值混合处理面 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec64f0474d7248694225aa08466d6ca8ab5d0f44
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347578"
---
# <a name="loading-a-dpxd-alpha-blending-surface"></a>加载 DPXD Alpha 混合图面


## <span id="ddk_loading_a_dpxd_alpha_blending_surface_gg"></span><span id="DDK_LOADING_A_DPXD_ALPHA_BLENDING_SURFACE_GG"></span>


已解码的 PXD (DPXD) alpha 值混合处理图面定义为一个范围的字节数组。 帧数据的每个字节包含四个 2 位示例。 每个 2 位示例使用由突出显示和 DCCMD （显示控制命令） 数据四色表中的索引。 DPXD、 突出显示，和 DCCMD 组合的结果等效于 IA44 面，用于与 16 项 YUV 调色板值混合处理。 如果 DPXD 数据的第一个字节的最高有效位的字节，第一个 2 位示例的索引数组原样处理 DPXD alpha 值混合处理图面，则下一个示例是在接下来的 2 位，第三个示例是在接下来的 2 位第四个示例是以最低有效位为单位，第五个示例是中的最高有效位的下一个字节，依此类推。

可能从 DVD 有关的 PXD 信息创建 DPXD alpha 值混合处理图面。 （PXD 数据运行长度编码格式的 DVD 中记录）。从 DVD 上 PXD DPXD 创建所需的主机解码器执行运行长度解码的 DVD 上的原始 PXD 数据。

在图面跨距必须解释为 stride 以字节为单位，而不在 2 位样本。 但是，宽度和高度必须是以 2 位示例为单位。

**请注意**   PXD DVD 上为结构字段的交错格式。 为 DirectX VA 定义 DPXD alpha 值混合处理面不是。 因此，主机负责如果从 DVD PXD 数据形成 DPXD 交错的两个字段中的数据。

 

DVD 子画面定义和数据字段的解释的详细说明，请参阅*DVD 规范为只读磁盘：第 3 部分-视频规范 （版本 1.11，1999 年 5）*。

 

 





