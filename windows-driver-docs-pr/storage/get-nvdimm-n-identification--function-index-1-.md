---
title: 获取 NVDIMM-N 标识（功能索引 1）
description: 此函数返回特定于设备的信息。
ms.assetid: 350E764D-634C-4C60-9C74-E26B01636C02
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e3398aa1e52831e03496f7f850715362bba5a2ec
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349648"
---
# <a name="span-idstoragegetnvdimm-nidentificationfunctionindex1spanget-nvdimm-n-identification-function-index-1"></a><span id="storage.get_nvdimm-n_identification__function_index_1_"></span>获取 NVDIMM N 标识 （函数索引 1）


此函数返回特定于设备的信息。

&gt; \[!请注意\]    &gt;用一个星号标记所有寄存器 (\*) 字节可寻址能源支持接口规范中定义的寄存器。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>输入


### <a name="span-idarg3spanspan-idarg3spanspan-idarg3spanarg3"></a><span id="Arg3"></span><span id="arg3"></span><span id="ARG3"></span>Arg3

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
<td align="left"><strong>规范修订版本</strong></td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left"><p>该模块支持的规范版本。</p>
<p><em>字节 0 – <em>SPECREV</em>该寄存器 （0，0x06:sp） 是可寻址的能源履行接口注册一个字节。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>标准的页面数</strong></td>
<td align="left">1</td>
<td align="left">5</td>
<td align="left"><p>该模块支持的标准定义页的数目。</p>
<p></em>Byte 0 – <em>STD_NUM_PAGES</em> (0, 0x01)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>第一个供应商页</strong></td>
<td align="left">1</td>
<td align="left">6</td>
<td align="left"><p>特定于供应商的页面起始页码。</p>
<p><em>Byte 0 – <em>VENDOR_START_PAGES</em> (0, 0x02)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>供应商页面数</strong></td>
<td align="left">1</td>
<td align="left">7</td>
<td align="left"><p>该模块支持的特定于供应商的页面数。</p>
<p></em>Byte 0 – <em>VENDOR_NUM_PAGES</em> (0, 0x03)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>硬件版本</strong></td>
<td align="left">4</td>
<td align="left">8</td>
<td align="left"><p>控制器的硬件版本。</p>
<p><em>字节 0 – <em>HWREV</em> （0，0x04）</p>
<p>保留字节 1。</p>
<p>保留字节 2。</p>
<p>保留字节 3。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>固件修订版</strong></td>
<td align="left">2</td>
<td align="left">12</td>
<td align="left"><p>活动固件插槽的固件版本。</p>
<p></em>Byte 0 – <em>SLOTX_FWREV0</em> (0, 0x07/0x09)</p>
<p><em>Byte 1 – <em>SLOTX_FWREV1</em> (0, 0x08/0x0A)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>当前固件槽</strong></td>
<td align="left">1</td>
<td align="left">14</td>
<td align="left"><p>正在运行的固件映像的槽数。</p>
<p></em>字节 0 – [7:4] 位数<em>FW_SLOT_INFO</em> （3，0x42） 注册 (<em>RUNNING_FW_SLOT</em>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>固件插槽计数</strong></td>
<td align="left">1</td>
<td align="left">15</td>
<td align="left"><p>可用的固件插槽数。 对于符合 jedec 的设备，此字段应为 2。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>功能</strong></td>
<td align="left">1</td>
<td align="left">16</td>
<td align="left"><p>有关该模块支持的功能的信息。</p>
<p><em>字节 0 –<em>功能</em>（0，0x10）</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>支持备份触发器</strong></td>
<td align="left">1</td>
<td align="left">17</td>
<td align="left"><p>保存触发器，该模块的受支持。</p>
<p></em>字节 0 – <em>CSAVE_TRIGGER_SUPPORT</em> （0，0x16）</p></td>
</tr>
<tr class="even">
<td align="left"><strong>最大操作重试计数</strong></td>
<td align="left">1</td>
<td align="left">18</td>
<td align="left"><p>建议重试计数到主机，如果保存，还原或擦除操作将失败或超出最大超时值。</p>
<p><em>字节 0 – <em>HOST_MAX_OPERATION_RETRY</em> （0，0x15）</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>支持的通知事件</strong></td>
<td align="left">1</td>
<td align="left">19</td>
<td align="left"><p>事件信息模块将生成的通知。</p>
<p></em>字节 0 – <em>EVENT_NOTIFICATION_SUPPORT</em> （0，0x17）</p></td>
</tr>
<tr class="even">
<td align="left"><strong>保存操作超时</strong></td>
<td align="left">4</td>
<td align="left">20</td>
<td align="left"><p>最坏情况下保存毫秒或秒中完成延迟。</p>
<p><em>字节 0 – <em>CSAVE_TIMEOUT0</em> （0，从 0x18）</p>
<p></em>1 – 字节<em>CSAVE_TIMEOUT1</em> （0，0x19）</p>
<p>保留字节 2。</p>
<p>保留字节 3。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>还原操作超时</strong></td>
<td align="left">4</td>
<td align="left">24</td>
<td align="left"><p>最坏情况下还原完成毫秒或秒的延迟。</p>
<p><em>字节 0 – <em>RESTORE_TIMEOUT0</em> （0，0x1C）</p>
<p></em>1 – 字节<em>RESTORE_TIMEOUT1</em> （0，0x1D）</p>
<p>保留字节 2。</p>
<p>保留字节 3。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>清除操作超时</strong></td>
<td align="left">4</td>
<td align="left">28</td>
<td align="left"><p>最坏情况下清除完成毫秒或秒的延迟。</p>
<p><em>字节 0 – <em>ERASE_TIMEOUT0</em> （0，0x1E）</p>
<p></em>1 – 字节<em>ERASE_TIMEOUT1</em> （0，0x1F）</p>
<p>保留字节 2。</p>
<p>保留字节 3。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>Arm 操作超时</strong></td>
<td align="left">4</td>
<td align="left">32</td>
<td align="left"><p>中毫秒或秒的最差事例 arm 完成延迟。</p>
<p>字节 0 – <em>ARM_TIMEOUT0</em> （0，0x20）</p>
<p>1 – 字节<em>ARM_TIMEOUT1</em> （0，0x21）</p>
<p>保留字节 2。</p>
<p>保留字节 3。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>固件操作超时</strong></td>
<td align="left">4</td>
<td align="left">36</td>
<td align="left"><p>最差事例固件操作完成中的延迟毫秒或秒。</p>
<p><em>字节 0 – <em>FIRMWARE_OPS_TIMEOUT0</em> （0，0x22）</p>
<p></em>1 – 字节<em>FIRMWARE_OPS_TIMEOUT1</em> （0，0x23）</p>
<p>保留字节 2。</p>
<p>保留字节 3。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>中止操作超时</strong></td>
<td align="left">4</td>
<td align="left">40</td>
<td align="left"><p></p>
<p><em>字节 0 – <em>ABORT_CMD_TIMEOUT0</em> （0，0x24）</p>
<p>保留字节 1 –。</p>
<p>保留字节 2。</p>
<p>保留字节 3。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>最小工作温度</strong></td>
<td align="left">1</td>
<td align="left">44</td>
<td align="left"><p>运行温度以摄氏度最小值。</p>
<p></em>字节 0 – <em>MIN_OPERATING_TEMP</em> （0，0x25）</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>最大工作温度</strong></td>
<td align="left">1</td>
<td align="left">45</td>
<td align="left"><p>最大工作温度以摄氏度。</p>
<p><em>字节 0 – <em>MAX_OPERATING_TEMP</em> （0，0x26）</p></td>
</tr>
<tr class="even">
<td align="left"><strong>区域的块大小</strong></td>
<td align="left">4</td>
<td align="left">46</td>
<td align="left"><p>区域大小的 32 字节的倍数。</p>
<p></em>Byte 0 – <em>REGION_BLOCK_SIZE</em> (0, 0x32)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






