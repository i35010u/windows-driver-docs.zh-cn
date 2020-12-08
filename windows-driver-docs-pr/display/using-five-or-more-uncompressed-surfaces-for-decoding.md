---
title: 使用五个或更多个未压缩的图面进行解码
description: 使用五个或更多个未压缩的图面进行解码
keywords:
- 视频解码 WDK DirectX VA，顺序要求
- 解码视频 WDK DirectX VA，顺序要求
- 图片解码 WDK DirectX VA，顺序要求
- 序列要求 WDK DirectX VA
- 连续要求 WDK DirectX VA
- 用于解码 WDK DirectX VA 的多个未压缩的图面
- 用于解码 WDK DirectX VA 的未压缩曲面示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10cbb75181255ae2ea1cb84842df2c70f7fe3cb5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818549"
---
# <a name="using-five-or-more-uncompressed-surfaces-for-decoding"></a>使用五个或更多个未压缩的图面进行解码


## <span id="ddk_using_five_or_more_uncompressed_surfaces_for_decoding_gg"></span><span id="DDK_USING_FIVE_OR_MORE_UNCOMPRESSED_SURFACES_FOR_DECODING_GG"></span>


超过四个未压缩的图面可用于解码，这允许从缓冲区的显示开始到缓冲区的新写入操作之间的时间延迟，将最小显示时间段增加到两个或更多。 此方法可以在解码过程中提供更多的抖动来实现抖动。 此方法还可以对解码的图片启用输出处理，以在显示过程中执行三域的取消隔行扫描操作。 这是因为不仅可以显示当前可用的图片，还可以在实际的显示过程中提供上下文并允许出现单字段延迟。

尽管要有效地使用带有 B 图片的 DirectX VA 需要四个缓冲区，但建议使用5个或更多的缓冲区，尤其是在不需要保持延迟最小的情况下。 因此，在分配未压缩的图面时，需要将最小和最大的未压缩的图面分配计数设置为至少四个和五个的 DirectX VA 解码器。 使用一个或多个额外未压缩的图面可以实现可靠且无需操作。

 

 





