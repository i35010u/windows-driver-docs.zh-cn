---
title: 主机外 VLD 位流解码操作
description: 主机外 VLD 位流解码操作
ms.assetid: fd339d5f-2d63-4b2f-a5dc-7ab7a6799a6d
keywords:
- 脱离主机 VLD 位流处理 WDK DirectX VA
- 位流 VLD 处理 WDK DirectX VA
- 反量化矩阵缓冲 WDK DirectX VA
- 切片控制缓冲 WDK DirectX VA
- 位流缓冲 WDK DirectX VA
- 压缩的图片解码 WDK DirectX VA，面向宏块的图片解码
- 图片解码 WDK DirectX VA，已压缩
- 视频解码 WDK DirectX VA，压缩图片
- 解码视频 WDK DirectX VA，压缩图片
- 视频解码 WDK DirectX VA，脱离主机 VLD 位流处理
- 解码视频 WDK DirectX VA，脱离主机 VLD 位流处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e314a2c921741c2084f341530205fdf38597b3ff
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063840"
---
# <a name="off-host-vld-bitstream-decoding-operation"></a>主机外 VLD 位流解码操作


## <span id="ddk_off_host_vld_bitstream_decoding_operation_gg"></span><span id="DDK_OFF_HOST_VLD_BITSTREAM_DECODING_OPERATION_GG"></span>


在快捷键上执行原始位流数据的可变长度解码时，由主机发送的用于对图片进行解码的数据划分为以下缓冲区类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">缓冲区类型</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>反量化矩阵</p></td>
<td align="left"><p>提供有关如何对位流数据执行反量化的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>切片控件</p></td>
<td align="left"><p>提供有关位流数据缓冲区中的开始代码和数据位置的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>位流</p></td>
<td align="left"><p>包含根据特定视频编码规范编码的原始数据流。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idinverse-quantization_matrix_buffersspanspan-idinverse-quantization_matrix_buffersspanspan-idinverse-quantization_matrix_buffersspaninverse-quantization-matrix-buffers"></a><span id="Inverse-Quantization_Matrix_Buffers"></span><span id="inverse-quantization_matrix_buffers"></span><span id="INVERSE-QUANTIZATION_MATRIX_BUFFERS"></span>反量化矩阵缓冲区

发送反量化矩阵缓冲区以初始化位流解码的反量化矩阵。 反量化矩阵缓冲区提供有关如何对位流中的所有当前和后续视频进行解码的信息，直到提供新的反量化矩阵缓冲区。  (因此，反量化矩阵是永久性的。 ) 每次只能将一个反量化矩阵缓冲区从主机发送到加速器。 [**DXVA \_ QmatrixData**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_qmatrixdata)结构加载量化视频照片解码的量化矩阵数据。

### <a name="span-idslice-control_buffersspanspan-idslice-control_buffersspanspan-idslice-control_buffersspanslice-control-buffers"></a><span id="Slice-Control_Buffers"></span><span id="slice-control_buffers"></span><span id="SLICE-CONTROL_BUFFERS"></span>切片控件缓冲区

切片控制缓冲区指导 VLD 位流处理的操作。 主机软件解码器确定位流中切片级别重新同步点的位置。 切片定义为 multimacroblock 层，其中包含位流数据中的重新同步点。 在261轨道中，261组块 (GOB) 视为切片。 在轨道中，一个或多个 GOBs 从 GOB 开始代码开始，不包含其他 GOB 开始代码的序列被视为切片。 切片控制缓冲区包含 [**DXVA \_ SliceInfo**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_sliceinfo) 切片控制结构的数组，这些结构应用于相应位流数据缓冲区的内容。

### <a name="span-idbitstream_buffersspanspan-idbitstream_buffersspanspan-idbitstream_buffersspanbitstream-buffers"></a><span id="Bitstream_Buffers"></span><span id="bitstream_buffers"></span><span id="BITSTREAM_BUFFERS"></span>位流缓冲区

如果使用位流缓冲区，则缓冲区只包含来自视频位流的原始字节。 此类型的缓冲区用于脱离主机解码，包括使用可变长度解码的低级别位流分析。

对位流缓冲区的内容施加了某些限制，这是因为加速器接收的数据采用可识别且高效的形式。

1.  除了 MPEG-2 和 MPEG-2 以外，每个图片的第一个位流缓冲区必须以所有数据（如果有）开头，后跟在位流 (中当前图片的第一个切片之前的所有数据（如果有），例如序列标头或图片标题) 。

2.  对于 MPEG-2 和 MPEG-2，每张图片的第一个位流缓冲区必须以图片第一个切片的切片开始代码开头 (例如，不) 序列标头或图片标题，因为其他参数中提供了所有相关数据。

3.  如果位流数据的切片的起始位置位于特定位流缓冲区内，则该切片的结尾还必须位于同一缓冲区内，除非包含切片开头的缓冲区已达到其分配大小。

解码器应该管理位流缓冲区的填充，以避免将一个切片的数据放入多个缓冲区。

 

