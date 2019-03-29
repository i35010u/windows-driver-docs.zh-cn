---
title: 序列要求
description: 序列要求
ms.assetid: ee716286-f455-463d-906d-6f1b9fb8f227
keywords:
- 视频解码 WDK DirectX va，因此序列要求
- 解码视频 WDK DirectX va，因此序列要求
- 解码 WDK DirectX va，因此序列要求的图片
- 序列化要求 WDK DirectX VA
- 压缩的缓冲区 WDK DirectX VA
- 缓冲 WDK DirectX VA
- 连续要求 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc36cb08f887ad46e599aa32267e5cea72bc035b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562284"
---
# <a name="sequence-requirements"></a>序列要求


## <span id="ddk_sequence_requirements_gg"></span><span id="DDK_SEQUENCE_REQUIREMENTS_GG"></span>


若要避免争用条件和不正确的解码器和加速器在解码过程中的操作，必须遵守加速器和解码器序列要求。

### <a name="span-idacceleratorspanspan-idacceleratorspanspan-idacceleratorspanaccelerator"></a><span id="Accelerator"></span><span id="accelerator"></span><span id="ACCELERATOR"></span>Accelerator

查询时，硬件加速器报告的未压缩的图面显示是否挂起或正在运行，并已完成请求的操作。 但是，它负责的主机软件解码器 (不 accelerator) 来确保争用条件不会在解码过程中导致意外行为。

### <a name="span-iddecoderspanspan-iddecoderspanspan-iddecoderspandecoder"></a><span id="Decoder"></span><span id="decoder"></span><span id="DECODER"></span>Decoder

解码器必须遵守两个规则进行正确解码，并显示未压缩的图面：

1.  不会覆盖任何图片，除非它已经被已提交为显示在显示屏上显示，并且还从显示中删除。

2.  不会覆盖所需的尚未创建其他图片创建的引用的任何图片。

遵循这些规则可确保正确操作在解码过程中的顺序操作，避免在显示屏上的撕裂项目。 指导规则是：*不要覆盖所需的引用或显示，并避免争用条件。*

若要避免争用条件，软件解码器必须查询 accelerator 的状态。 解码器还必须使用足够数量的未压缩的图面以确保所有必要的操作的可用空间。 这会导致需要至少四个解码组成 I，B，视频流的未压缩的图片表面和 P 图片。 使用四个以上的图面是通常建议，且需对于某些操作，如前端 alpha 值混合处理。 （使用额外的图面可以显著减少需要等待操作要解析的依赖项。）

提供的示例显示解码的传统我、 B 和 P 结构化视频帧 （不使用 deblocking 筛选器）[使用四个未压缩表面解码](using-four-uncompressed-surfaces-for-decoding.md)和[使用五个或多个未压缩的解码的图面](using-five-or-more-uncompressed-surfaces-for-decoding.md)。

**请注意**  压缩缓冲区，以及与未压缩的图面，则通常最好间循环切换已分配和可用缓冲区而不是要保留重复使用同一缓冲区或同一子集分配的缓冲区。 这可以降低所造成的不必要的依赖项上等待的添加延迟的可能性。 由驱动程序的多个缓冲区的分配应视为指示循环的双精度或三重缓冲这些缓冲区为的正确方法进行操作并避免项目，如临时图片会冻结。 这适用于 alpha 混合数据特别加载。

 

 

 





