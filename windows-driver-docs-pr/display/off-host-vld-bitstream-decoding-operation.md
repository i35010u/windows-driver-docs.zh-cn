---
title: 主机外 VLD 位流解码操作
description: 主机外 VLD 位流解码操作
ms.assetid: fd339d5f-2d63-4b2f-a5dc-7ab7a6799a6d
keywords:
- 关闭主机 VLD 位流处理 WDK DirectX VA
- 位流 VLD 处理 WDK DirectX VA
- 反转量化矩阵缓冲 WDK DirectX VA
- 切片控制缓冲 WDK DirectX VA
- 位流缓冲 WDK DirectX VA
- 压缩的图片解码 WDK DirectX va，因此面向宏块的图片解码
- 图片解码 WDK DirectX VA，压缩
- 视频解码 WDK DirectX VA，压缩的图片
- 解码视频 WDK DirectX VA，压缩图片
- 视频解码 WDK DirectX va，因此主机-VLD 位流处理
- 解码视频 WDK DirectX VA，非主机 VLD 位流处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0a5819e50452ce4aff38a99754086ea77982093
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372786"
---
# <a name="off-host-vld-bitstream-decoding-operation"></a>主机外 VLD 位流解码操作


## <span id="ddk_off_host_vld_bitstream_decoding_operation_gg"></span><span id="DDK_OFF_HOST_VLD_BITSTREAM_DECODING_OPERATION_GG"></span>


加速器上执行时的原始位流数据的长度可变的解码，则由主机发送的图片的解码的数据分为以下缓冲区类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">缓冲区类型</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>反转量化矩阵</p></td>
<td align="left"><p>提供有关如何执行逆量化位流数据的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>切片控件</p></td>
<td align="left"><p>提供的启动代码和相应的位流数据缓冲区中的数据位置有关的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>位流</p></td>
<td align="left"><p>包含原始流编码根据特定的视频编码规范的数据。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idinverse-quantizationmatrixbuffersspanspan-idinverse-quantizationmatrixbuffersspanspan-idinverse-quantizationmatrixbuffersspaninverse-quantization-matrix-buffers"></a><span id="Inverse-Quantization_Matrix_Buffers"></span><span id="inverse-quantization_matrix_buffers"></span><span id="INVERSE-QUANTIZATION_MATRIX_BUFFERS"></span>反转量化矩阵缓冲区

反转量化矩阵缓冲区发送以初始化用于关闭主机位流解码逆量化矩阵。 反转量化矩阵缓冲区提供有关如何提供新的逆量化矩阵缓冲区之前解码位流中的所有当前和后续视频的信息。 （因此，反转量化矩阵是永久性的。）不能超过一个逆量化矩阵缓冲区可以从主机到快捷键发送一次。 [ **DXVA\_QmatrixData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_qmatrixdata)结构将用于压缩视频图片解码量化矩阵数据加载。

### <a name="span-idslice-controlbuffersspanspan-idslice-controlbuffersspanspan-idslice-controlbuffersspanslice-control-buffers"></a><span id="Slice-Control_Buffers"></span><span id="slice-control_buffers"></span><span id="SLICE-CONTROL_BUFFERS"></span>切片控制缓冲区

切片控制缓冲区指导非主机 VLD 位流处理的操作。 主机软件解码器确定位流中的切片级别重新同步点的位置。 切片定义为位流数据中包括的重新同步点 multimacroblock 层。 在 H.261 轨道 H.261 组的基块 (GOB) 被视为一个切片。 中 H.263 轨道，一系列一个或多个 H.263 大笔开头 GOB 启动代码，并包含任何其他 GOB 开始代码被视为一个切片。 切片控制缓冲区中包含的数组[ **DXVA\_SliceInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_sliceinfo)切片控制结构，将应用于相应的位流数据缓冲区的内容。

### <a name="span-idbitstreambuffersspanspan-idbitstreambuffersspanspan-idbitstreambuffersspanbitstream-buffers"></a><span id="Bitstream_Buffers"></span><span id="bitstream_buffers"></span><span id="BITSTREAM_BUFFERS"></span>位流缓冲区

如果使用的位流缓冲区，则在缓冲区中只包含视频的位流中的原始字节。 此类型的缓冲区使用的非主机解码，包括低级别的位流分析与可变长度解码。

为了让所接收数据的加速器是可识别和高效的窗体中，将位流缓冲区的内容上施加某些限制。

1.  除了 mpeg-1 和 mpeg-2，第一位流缓冲区的每个图片必须开头的所有数据，如果有任何位流在前面的第一个切片中的当前图片的先前图片的所有数据结束后 (例如，序列标头或图片标头）。

2.  Mpeg-1 和 mpeg-2，每张图片的第一位流缓冲区必须启动 （例如，任何序列标头或图片标头），该图片的第一个切片的切片开始代码中，因为其他参数中提供所有相关数据。

3.  如果找到特定的位流缓冲区中的位流数据切片的开始了，除非包含切片的开始的缓冲区已达到其分配的大小，还必须是该切片结束的位于该同一缓冲区情况。

解码器应管理位流缓冲区，以避免将一个切片的数据放入多个缓冲区填的满。

 

 





