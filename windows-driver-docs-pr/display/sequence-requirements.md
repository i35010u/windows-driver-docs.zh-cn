---
title: 序列要求
description: 序列要求
keywords:
- 视频解码 WDK DirectX VA，顺序要求
- 解码视频 WDK DirectX VA，顺序要求
- 图片解码 WDK DirectX VA，顺序要求
- 序列要求 WDK DirectX VA
- 压缩的缓冲区 WDK DirectX VA
- 缓冲 WDK DirectX VA
- 连续要求 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78e0464859e2d59ba23bf7637e9146e9e6b3538b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816819"
---
# <a name="sequence-requirements"></a>序列要求


## <span id="ddk_sequence_requirements_gg"></span><span id="DDK_SEQUENCE_REQUIREMENTS_GG"></span>


必须观察加速器和解码器的顺序要求，以避免在解码过程中出现争用情况和解码器和加速器的不正确操作。

### <a name="span-idacceleratorspanspan-idacceleratorspanspan-idacceleratorspanaccelerator"></a><span id="Accelerator"></span><span id="accelerator"></span><span id="ACCELERATOR"></span>键

查询时，硬件加速器会报告未压缩的图面是处于挂起还是正在进行的，以及是否已完成请求的操作。 但是，主机软件解码器的责任 (不是加速) ，以确保争用情况在解码过程中不会导致意外的行为。

### <a name="span-iddecoderspanspan-iddecoderspanspan-iddecoderspandecoder"></a><span id="Decoder"></span><span id="decoder"></span><span id="DECODER"></span>解码器

解码器必须遵循两个规则才能正确地解码和显示未压缩的图面：

1.  不要覆盖已提交以供显示的任何图片，除非它已显示在显示器上并从显示中删除。

2.  不要覆盖任何需要的图片，作为创建尚未创建的其他图片的参考。

遵循这些规则可确保对解码过程中的顺序操作进行适当的操作，并避免显示中出现撕裂的项目。 指导原则是： *不要写入引用或显示所需的内容，避免争用条件。*

若要避免争用条件，软件解码器必须查询加速器的状态。 解码器还必须使用足够数量的未压缩图片图面，以确保空间可用于所有必要的操作。 这将导致需要至少四个未压缩的图片面来解码包含 I、B 和 P 图片的视频流。 通常建议使用四个以上的图面，对于某些操作（例如前端 alpha 混合）来说，这是必需的。 使用额外的图面 (可以显著减少等待解决操作依赖关系所需的时间。 ) 

[使用四个未压缩的图面进行解码](using-four-uncompressed-surfaces-for-decoding.md)并[使用5个或更多个未压缩的图面进行](using-five-or-more-uncompressed-surfaces-for-decoding.md)解码，可以在不使用 deblocking 筛选) 器的情况下，显示常规 I、B 和 P 结构化视频 (帧解码的示例。

**注意**   对于压缩的缓冲区以及未压缩的图面，通常更好的做法是循环访问已分配的和可用的缓冲区，而不是重复使用同一缓冲区或已分配缓冲区的相同子集。 这可以减少由于等待不必要的依赖关系而导致添加延迟的可能性。 通过驱动程序分配多个缓冲区时，应将其作为一种指示来循环使用这两个缓冲区进行双或三次缓冲，以正确操作和避免项目（如暂时图片冻结）。 这适用于特别适用于 alpha blend 数据加载。

 

 

 





