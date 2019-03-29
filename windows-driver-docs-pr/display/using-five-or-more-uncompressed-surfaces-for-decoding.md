---
title: 使用五个或更多个未压缩的图面进行解码
description: 使用五个或更多个未压缩的图面进行解码
ms.assetid: 7cd09d7a-6700-4079-97bd-0b0151705b82
keywords:
- 视频解码 WDK DirectX va，因此序列要求
- 解码视频 WDK DirectX va，因此序列要求
- 解码 WDK DirectX va，因此序列要求的图片
- 序列化要求 WDK DirectX VA
- 连续要求 WDK DirectX VA
- 用于解码 WDK DirectX VA 的多个未压缩的图面
- 用于解码 WDK DirectX VA 的未压缩的图面示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad73a257be86b7802d5d8bc2ffa3ffe513ba695e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562078"
---
# <a name="using-five-or-more-uncompressed-surfaces-for-decoding"></a>使用五个或更多个未压缩的图面进行解码


## <span id="ddk_using_five_or_more_uncompressed_surfaces_for_decoding_gg"></span><span id="DDK_USING_FIVE_OR_MORE_UNCOMPRESSED_SURFACES_FOR_DECODING_GG"></span>


四个未压缩的图面可用于解码，允许显示缓冲区的开始日期和向该缓冲区的新写入操作之间的滞后时间从一个显示时间至少增加到两个或多个。 此方法可以提供多个在解码过程的计时抖动的限额。 此方法还可以启用对已解码的输出处理图片执行三个字段取消隔行扫描操作作为显示进程的一部分。 这是因为不只是当前图片的显示，但上一张图片也可用，可用和可以提供上下文，并且允许在实际显示进程中的一个字段延迟。

尽管需要有效地利用 DirectX VA B 图片的四个缓冲区最小值，则被鼓励使用五个或多个缓冲区，尤其是在不需要延迟保持在最低限度的方案。 我、 B 和 P 结构化视频解码的 DirectX VA 解码器因此应在设置其最小值和最大请求未压缩图面上分配计数到至少四个和第五个，分别分配未压缩的图面时。 使用一个或多个额外的未压缩的图面可以实现可靠的、 免拆解操作。

 

 





