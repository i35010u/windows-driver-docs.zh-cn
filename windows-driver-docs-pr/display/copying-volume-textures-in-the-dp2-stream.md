---
title: DP2 Stream 中的复制卷纹理
description: DP2 Stream 中的复制卷纹理
ms.assetid: c7f982d8-d35b-4462-a0cf-49dfb82860f8
keywords:
- 纹理 WDK DirectX 8.0
- DirectX 8.0 发行说明 WDK Windows 2000 显示，体积纹理
- 体积纹理 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b225f03106e802d10706dbeb3ab7e813c4d2d2b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520344"
---
# <a name="copying-volume-textures-in-the-dp2-stream"></a>DP2 Stream 中的复制卷纹理


## <span id="ddk_copying_volume_textures_in_the_dp2_stream_gg"></span><span id="DDK_COPYING_VOLUME_TEXTURES_IN_THE_DP2_STREAM_GG"></span>


新的 DP2 令牌 D3DDP2OP\_添加了 VOLUMEBLT，以获得最佳的复制和更新的体积纹理。 此令牌是非常类似于现有 D3DDP2OP\_TEXBLT 复制和更新的纹理，但已扩展为支持子宗卷 （框） 复制而不简单的矩形。

 

 





