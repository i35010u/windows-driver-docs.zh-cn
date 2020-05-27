---
title: 发送固件更新数据（功能索引 23）
description: 此函数将固件数据发送到设备。
ms.assetid: 3F28C89B-040A-407B-B780-96D6767DC5C7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: be9d74fe6e2bb02a7568056a1f66bfd717b7b434
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851252"
---
# <a name="send-firmware-update-data-function-index-23"></a>发送固件更新数据（功能索引 23）


此函数将固件数据发送到设备。

> [!NOTE]
> 标有星号（）的所有寄存器 \* 都是在可通过字节寻址的可处理电源接口规范中定义的寄存器。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>送


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
<th align="left">字节偏移量</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>区域长度</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>此函数中发送的字节数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>区域 ID</strong></td>
<td align="left">2</td>
<td align="left">4</td>
<td align="left"><p>要写入的区域的标识。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>块 ID</strong></td>
<td align="left">1</td>
<td align="left">6</td>
<td align="left"><p>在该区域中写入的块的标识。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>固件数据</strong></td>
<td align="left">按<em>区域长度</em>指定的数字。</td>
<td align="left">7</td>
<td align="left"><p>区域大小的固件映像数据的数据包。</p></td>
</tr>
</tbody>
</table>

 

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
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>状态</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>此函数可以返回以下特定于函数的错误代码：</p>
<p>1：没有正在进行的固件更新操作。</p>
<p>2：区域大小无效。</p>
<p>3：传输因数据损坏而失败。</p>
<p>4：操作超时。</p>
<p>5：固件提交操作失败。</p>
<p>有关详细信息，请参阅<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>。</p></td>
</tr>
</tbody>
</table>

 

> [!NOTE]
> 此函数应计算固件数据的 CRC，并将其与 \* *fw \_ 区域 \_ CRC0* （3、0x40）和 \* *fw \_ region \_ CRC1* （3，0x41 向）进行比较。 如果值不匹配，则函数将失败，并出现函数特定的错误代码3。 请参阅 CRC 算法规范的以字节寻址的支持能源支持的接口 JEDEC 标准。

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[启动固件更新（功能索引 22）](start-firmware-update--function-index-22-.md)

[完成固件更新（功能索引 24）](finish-firmware-update--function-index-24-.md)

[选择固件映像槽（功能索引 25）](select-firmware-image-slot--function-index-25-.md)

[获取固件信息（功能索引 26）](get-firmware-info--function-index-26-.md)

[\_用于字节寻址的支持能源的函数类的 DSM 接口（Function Interface 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






