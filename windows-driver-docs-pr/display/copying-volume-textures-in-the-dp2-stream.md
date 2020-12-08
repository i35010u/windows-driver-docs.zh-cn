---
title: 在 DP2 流中复制体积纹理
description: 在 DP2 流中复制体积纹理
keywords:
- 纹理 WDK DirectX 8。0
- DirectX 8.0 发行说明 WDK Windows 2000 显示，音量纹理
- 卷纹理 WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a067c6b8f05b98ae329da061518c125ce6f05653
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839115"
---
# <a name="copying-volume-textures-in-the-dp2-stream"></a>在 DP2 流中复制体积纹理


## <span id="ddk_copying_volume_textures_in_the_dp2_stream_gg"></span><span id="DDK_COPYING_VOLUME_TEXTURES_IN_THE_DP2_STREAM_GG"></span>


添加了新的 DP2 令牌 D3DDP2OP \_ VOLUMEBLT，以支持卷纹理的最佳复制和更新。 此令牌非常类似于现有的 D3DDP2OP \_ TEXBLT，它可复制和更新纹理，但) 复制而不是简单的矩形就已扩展为支持 subvolume (框。

 

 





