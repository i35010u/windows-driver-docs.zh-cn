---
title: 获取上次备份信息（功能索引 4）
description: 此函数返回有关已保存的映像的信息。
ms.assetid: F73A763B-4A4A-4CAB-AA62-AFA79849884B
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 76b0e061c53f230e4ba6905a81d69226236bcd30
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386616"
---
# <a name="get-last-backup-information-function-index-4"></a>获取上次备份信息（功能索引 4）


此函数返回有关已保存的映像的信息。

&gt; \[!请注意\]    &gt;用一个星号标记所有寄存器 (\*) 字节可寻址能源支持接口规范中定义的寄存器。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>输入


### <a name="span-idargs3spanspan-idargs3spanspan-idargs3spanargs3"></a><span id="Args3"></span><span id="args3"></span><span id="ARGS3"></span>Args3

无。

## <a name="span-idoutputspanspan-idoutputspanspan-idoutputspanoutput"></a><span id="Output"></span><span id="output"></span><span id="OUTPUT"></span>Output


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
<th align="left">字节偏移</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>状态</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>转到<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>有关信息。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>触发器的信息</strong></td>
<td align="left">4</td>
<td align="left">4</td>
<td align="left"><p>信息是否存在是保存在非易失性内存子系统和保存的触发器源无效的 DRAM 映像操作。</p>
<p><em>字节 0 – <em>CSAVE_INFO0</em> （0，0x80）</p>
<p>保留字节 1 –。</p>
<p>保留字节 2 –。</p>
<p>保留字节 3 –。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>保存失败信息</strong></td>
<td align="left">4</td>
<td align="left">8</td>
<td align="left"><p>失败信息的保存操作。</p>
<p></em>字节 0 – <em>CSAVE_FAIL_INFO0</em> （0，0x84）</p>
<p>*Byte 1 – <em>CSAVE_FAIL_INFO1</em> (0, 0x85)</p>
<p>保留字节 2 –。</p>
<p>保留字节 3 –。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






