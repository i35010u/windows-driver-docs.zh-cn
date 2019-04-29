---
title: 发送固件更新数据（功能索引 23）
description: 此函数将固件数据发送到设备。
ms.assetid: 3F28C89B-040A-407B-B780-96D6767DC5C7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 03fa586e262c45e0e1f80c141bd3fb7732de7827
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372356"
---
# <a name="send-firmware-update-data-function-index-23"></a>发送固件更新数据（功能索引 23）


此函数将固件数据发送到设备。

&gt; \[!请注意\]    &gt;用一个星号标记所有寄存器 (\*) 字节可寻址能源支持接口规范中定义的寄存器。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>输入


### <a name="span-idargs3spanspan-idargs3spanspan-idargs3spanargs3"></a><span id="Args3"></span><span id="args3"></span><span id="ARGS3"></span>Args3

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
<td align="left"><strong>区域长度</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>在此函数正在发送的字节数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>区域 ID</strong></td>
<td align="left">2</td>
<td align="left">4</td>
<td align="left"><p>正在写入的区域的标识。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>块 ID</strong></td>
<td align="left">1</td>
<td align="left">6</td>
<td align="left"><p>正在写入区域内的块的标识。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>固件数据</strong></td>
<td align="left">指定的数量<em>区域长度</em>。</td>
<td align="left">7</td>
<td align="left"><p>固件映像数据的区域大小的数据包。</p></td>
</tr>
</tbody>
</table>

 

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
<td align="left"><p>此函数可返回以下特定于函数的错误代码：</p>
<p>1：没有固件更新操作正在进行中。</p>
<p>2：无效的区域大小。</p>
<p>3：传输因数据损坏而失败。</p>
<p>4:操作已超时。</p>
<p>5:固件提交操作失败。</p>
<p>转到<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>有关详细信息。</p></td>
</tr>
</tbody>
</table>

 

&gt; \[!请注意\]    &gt;此函数应计算的 CRC 固件数据并与之比较\**转发\_区域\_CRC0* （3，0x40） 和\**转发\_区域\_CRC1* （3，将 0x41 向）。 如果值不匹配，该函数应使用特定于函数的错误代码 3 失败。 请参阅字节可寻址能源支持接口 JEDEC 的 CRC 算法规范标准。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[启动固件更新 （函数索引 22）](start-firmware-update--function-index-22-.md)

[完成固件更新 （函数索引 24）](finish-firmware-update--function-index-24-.md)

[选择固件映像槽 （函数索引 25）](select-firmware-image-slot--function-index-25-.md)

[获取固件信息 （函数索引 26）](get-firmware-info--function-index-26-.md)

[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






