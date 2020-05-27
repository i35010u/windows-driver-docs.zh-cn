---
title: 获取固件信息（功能索引 26）
description: 此函数检索有关固件映像槽的信息。
ms.assetid: ABE67651-6351-4D8E-BCFF-0488D2A34DC5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 82253e65ea939a7ae4821708cd517d056820b656
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851332"
---
# <a name="get-firmware-info-function-index-26"></a>获取固件信息（功能索引 26）


此函数检索有关固件映像槽的信息。 调用[获取 Nvdimm-n 标识（函数索引1）](get-nvdimm-n-identification--function-index-1-.md)以检索当前槽号。

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
<td align="left"><strong>固件槽</strong></td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left"><p>要报告其信息的固件图像槽。</p></td>
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
<td align="left"><p>请参阅<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>获取详细信息。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>版本</strong></td>
<td align="left">2</td>
<td align="left">4</td>
<td align="left"><p>指定插槽中固件映像的固件版本。</p>
<p><em>Byte 0 – <em>SLOTX_FWVER0</em> （0，0x07/0x09）</p>
<p></em>Byte 1 – <em>SLOTX_FWVER1</em> （0，0X08/0x0A）</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[启动固件更新（功能索引 22）](start-firmware-update--function-index-22-.md)

[发送固件更新数据（功能索引 23）](send-firmware-update-data--function-index-23-.md)

[完成固件更新（功能索引 24）](finish-firmware-update--function-index-24-.md)

[选择固件映像槽（功能索引 25）](select-firmware-image-slot--function-index-25-.md)

[\_用于字节寻址的支持能源的函数类的 DSM 接口（Function Interface 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






