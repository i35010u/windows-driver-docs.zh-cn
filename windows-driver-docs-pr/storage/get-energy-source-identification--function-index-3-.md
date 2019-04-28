---
title: 获取能量源标识（功能索引 3）
description: 此函数返回的标识信息有关能源源 (ES)，可以管理的主机或设备管理。
ms.assetid: E1589FD0-5D03-42EF-8078-0AE53CFB1ACA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5c76bff652d9cad466c66907bc26828a0395c435
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348060"
---
# <a name="get-energy-source-identification-function-index-3"></a>获取能量源标识（功能索引 3）


此函数返回的标识信息有关能源源 (ES)，可以管理的主机或设备管理。

&gt; \[!Note\]   
&gt;用一个星号标记所有寄存器 (\*) 字节可寻址能源支持接口规范中定义的寄存器。



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
<td align="left"><strong>能量源策略</strong></td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left"><p>有关该模块支持的能量源策略的信息。</p>
<p>* 字节 0 – <em>ENERGY_SOURCE_POLICY</em> （0，0x14）</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>设备管理 ES 标识</strong></td>
<td align="left">11</td>
<td align="left">5</td>
<td align="left">&amp;gt; [!Note]<br/><p>&amp;g t;此字段包含有效的数据，仅当当前 ES 策略为设备管理 （即位设置 SET_ES_POLICY_STATUS （0，0x70） 2）。 对于所有其他 ES 策略，此字段应为 0。</p>

<p>有关信息，请参阅 Device-Managed ES 标识。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>主机托管 ES 标识</strong></td>
<td align="left">3</td>
<td align="left">16</td>
<td align="left">&amp;gt; [!Note]<br/><p>&amp;g t;此字段包含有效的数据，仅当当前 ES 策略为管理的主机 （即位 3 SET_ES_POLICY_STATUS （0，0x70） 设置）。 对于所有其他 ES 策略，此字段应为 0。</p>

<p>有关信息，请参阅 Host-Managed ES 标识。</p></td>
</tr>
</tbody>
</table>



### <a name="span-iddevicemanagedesidentificationspanspan-iddevicemanagedesidentificationspanspan-iddevicemanagedesidentificationspandevice-managed-es-identification"></a><span id="Device_Managed_ES_Identification"></span><span id="device_managed_es_identification"></span><span id="DEVICE_MANAGED_ES_IDENTIFICATION"></span>设备管理 ES 标识

如果 ES 策略的值为 0，Device-Managed ES 标识字段有效且具有以下字段：

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
<td align="left"><strong>ES 硬件版本</strong></td>
<td align="left">2</td>
<td align="left">5</td>
<td align="left"><p>ES 硬件修订版本。</p>
<p><em>字节 0 – <em>ES_HWREV</em> （1，0x04）</p>
<p>保留字节 1。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ES 固件修订版</strong></td>
<td align="left">2</td>
<td align="left">7</td>
<td align="left"><p>ES 固件修订版本。</p>
<p></em>Byte 0 – <em>ES_FWREV0</em> (1, 0x06)</p>
<p><em>Byte 1 – <em>ES_FWREV1</em> (1, 0x07)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ES 运行状况检查频率</strong></td>
<td align="left">1</td>
<td align="left">9</td>
<td align="left"><p>当前模块的 ES 运行状况评估的频率。</p>
<p></em>字节 0 – <em>AUTO_ES_HEALTH_CHECK_FREQUENCY</em> （0，0xA9）</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ES 费用超时</strong></td>
<td align="left">2</td>
<td align="left">10</td>
<td align="left"><p>最坏的情况下，（在秒为单位） ES 收费时间。 值应大于 0。</p>
<p><em>字节 0 – <em>ES_CHARGE_TIMEOUT0</em> （1，0x10）</p>
<p></em>1 – 字节<em>ES_CHARGE_TIMEOUT1</em> （1，0x11）</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ES 最小工作温度</strong></td>
<td align="left">1</td>
<td align="left">12</td>
<td align="left"><p>运行温度 （单位为摄氏度） ES 的最小值。 支持的最小值应为 0。</p>
<p><em>字节 0 – <em>MIN_ES_OPERATING_TEMP</em> （1，0x12）</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ES 最大工作温度</strong></td>
<td align="left">1</td>
<td align="left">13</td>
<td align="left"><p>最大工作温度 （摄氏度） ES。</p>
<p></em>字节 0 – <em>MAX_ES_OPERATING_TEMP</em> （1，0x13）</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ES 属性</strong></td>
<td align="left">1</td>
<td align="left">14</td>
<td align="left"><p>有关 ES 的特性。</p>
<p><em>字节 0 – <em>ES_ATTRIBUTES</em> （1，0x14）</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ES 技术</strong></td>
<td align="left">1</td>
<td align="left">15</td>
<td align="left"><p>ES 中使用的技术。</p>
<p></em>字节 0 – <em>ES_TECH</em> （1，0x15）</p></td>
</tr>
</tbody>
</table>



### <a name="span-idhostmanagedesidentificationspanspan-idhostmanagedesidentificationspanspan-idhostmanagedesidentificationspanhost-managed-es-identification"></a><span id="Host_Managed_ES_Identification"></span><span id="host_managed_es_identification"></span><span id="HOST_MANAGED_ES_IDENTIFICATION"></span>主机托管 ES 标识

如果 ES 策略的值为 1，Host-Managed ES 标识字段有效且具有以下字段：

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
<td align="left"><strong>ES 运行状况检查频率</strong></td>
<td align="left">1</td>
<td align="left">16</td>
<td align="left"><p>当前平台的 ES 运行状况评估的频率。</p>
<p><em>字节 0 – <em>AUTO_ES_HEALTH_FREQUENCY</em> （0，0xA9）。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ES 属性</strong></td>
<td align="left">1</td>
<td align="left">17</td>
<td align="left"><p>主机托管能量源特性。</p>
<p></em>字节 0 – <em>HOST_MANAGED_ES_ATTRIBUTES</em> （2，0x82）</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ES 技术</strong></td>
<td align="left">1</td>
<td align="left">18</td>
<td align="left"><p>位掩码：</p>
<ul>
<li><p>[0] :未定义</p></li>
<li><p>[1] :Supercapacitor</p></li>
<li><p>[2] :电池</p></li>
<li><p>[3] :混合电容器</p></li>
<li><p>[7:4] 保留</p></li>
</ul></td>
</tr>
</tbody>
</table>



## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)










