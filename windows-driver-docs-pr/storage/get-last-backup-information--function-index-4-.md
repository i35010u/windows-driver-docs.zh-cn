---
title: 获取上次备份信息（功能索引 4）
description: 此函数返回有关保存的图像的信息。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 844811609d18ebe74539ebc06c4970ce6a31799f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804593"
---
# <a name="get-last-backup-information-function-index-4"></a>获取上次备份信息（功能索引 4）


此函数返回有关保存的图像的信息。

> [!NOTE]
> 标记为星形 () 的所有寄存器 \* 都是在可通过字节可寻址的、支持电源的接口规范中定义的寄存器。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>送


### <a name="span-idargs3spanspan-idargs3spanspan-idargs3spanargs3"></a><span id="Args3"></span><span id="args3"></span><span id="ARGS3"></span>Args3

无。

## <a name="span-idoutputspanspan-idoutputspanspan-idoutputspanoutput"></a><span id="Output"></span><span id="output"></span><span id="OUTPUT"></span>输出


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字段</th>
<th align="left">字节长度</th>
<th align="left">字节偏移量</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>状态</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>请参阅 <a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a> 获取详细信息。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>触发器信息</strong></td>
<td align="left">4</td>
<td align="left">4</td>
<td align="left"><p>有关非易失性内存子系统中是否有有效的 DRAM 映像以及保存操作的触发器源的信息。</p>
<p><em>Byte 0 – <em>CSAVE_INFO0</em> (0，0x80) </p>
<p>Byte 1 – Reserved。</p>
<p>Byte 2 – Reserved。</p>
<p>字节3–预留。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>保存失败信息</strong></td>
<td align="left">4</td>
<td align="left">8</td>
<td align="left"><p>保存操作的失败信息。</p>
<p></em>Byte 0 – <em>CSAVE_FAIL_INFO0 (</em>) </p>
<p>* Byte 1 – <em>CSAVE_FAIL_INFO1</em> (0，0x85) </p>
<p>Byte 2 – Reserved。</p>
<p>字节3–预留。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[\_用于字节寻址的支持能源的函数类 (函数接口 1) 的 DSM 接口 ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






