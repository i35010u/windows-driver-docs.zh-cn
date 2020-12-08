---
title: 启动固件更新（功能索引 22）
description: 此函数启动对特定固件槽的固件更新。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 95508c6cfef489d18798eefee4abd4e741c107f0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806697"
---
# <a name="start-firmware-update-function-index-22"></a>启动固件更新（功能索引 22）


此函数启动对特定固件槽的固件更新。 在任意给定时间，只能有一个固件更新操作。

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
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>固件槽</strong></td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left"><p>正在更新的固件槽。</p></td>
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
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>状态</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>此函数可能返回以下 Function-Specific 错误代码：</p>
<p>1：目前正在进行固件更新操作。</p>
<p>有关详细信息，请参阅 <a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a> 。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


主机调用以下固件功能来更新 & 激活固件：

1.  主机调用开始固件更新 (函数索引 22) 开始固件更新操作。 在此步骤中，主机将选择它正在更新哪个固件槽。

2.  主机反复调用 [发送固件更新数据 (函数 Index 23) ](send-firmware-update-data--function-index-23-.md) 将数据传输到设备。 每个调用传输一个区域大小的数据块;如果最后一次传输不是区域大小的，主机负责填充。

3.  主机调用 [完成固件更新 (函数 Index 24) ](finish-firmware-update--function-index-24-.md) 向平台发出固件更新操作的信号。

4.  主机调用 " [选择固件映像槽" (函数索引 25) ](select-firmware-image-slot--function-index-25-.md) 以便激活新的固件映像。 此更新将在下一次系统重新启动时生效。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[发送固件更新数据（功能索引 23）](send-firmware-update-data--function-index-23-.md)

[完成固件更新（功能索引 24）](finish-firmware-update--function-index-24-.md)

[选择固件映像槽（功能索引 25）](select-firmware-image-slot--function-index-25-.md)

[获取固件信息（功能索引 26）](get-firmware-info--function-index-26-.md)

[\_用于字节寻址的支持能源的函数类 (函数接口 1) 的 DSM 接口 ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






