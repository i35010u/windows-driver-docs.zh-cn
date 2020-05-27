---
title: 重置为出厂默认设置（功能索引 21）
description: 此函数将 NVDIMM-N 重置回供应商预先配置的设置。
ms.assetid: 64CEF5C8-FC2A-4C6E-829C-27E18A4EDC26
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 455f32429fc67349788dde17465a2980a6d6c379
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851262"
---
# <a name="reset-to-factory-defaults-function-index-21"></a>重置为出厂默认设置（功能索引 21）


此函数将 NVDIMM-N 重置回供应商预先配置的设置。

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
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>状态</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>此函数可以返回以下特定于函数的错误代码：</p>
<p>1：操作超时。</p>
<p>有关详细信息，请参阅<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>。</p></td>
</tr>
</tbody>
</table>

 

> [!NOTE]
> 平台应等待完成出厂默认操作的最大保存超时的三倍（例如，如果最大保存超时为60秒，则平台将等待180秒）。 如果操作所用时间超过该时间间隔，则平台应中止操作并返回与函数特定的错误代码1（操作超时）。

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[\_用于字节寻址的支持能源的函数类的 DSM 接口（Function Interface 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






