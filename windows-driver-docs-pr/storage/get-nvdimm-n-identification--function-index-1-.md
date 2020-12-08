---
title: 获取 NVDIMM-N 标识（功能索引 1）
description: 此函数返回特定于设备的信息。
ms.localizationpriority: medium
ms.date: 01/08/2020
ms.openlocfilehash: 6c21c500b0e9c867d37ad7e571d669825e91aa79
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804589"
---
# <a name="get-nvdimm-n-identification-function-index-1"></a>获取 NVDIMM-N 标识（功能索引 1）

此函数返回特定于设备的信息。

> [!NOTE]
> 标记为星形 () 的所有寄存器 \* 都是在可通过字节可寻址的、支持电源的接口规范中定义的寄存器。

## <a name="input"></a>输入

### <a name="arg3"></a>Arg3

无。

## <a name="output"></a>输出

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
<td align="left"><strong>规范修订版本</strong></td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left"><p>模块支持的规范版本。</p>
<p>Byte 0 – <em>SPECREV</em> (0，0X06) 此寄存器是一个可通过字节寻址的支持能源的接口注册。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>标准页数</strong></td>
<td align="left">1</td>
<td align="left">5</td>
<td align="left"><p>模块支持的标准已定义页的数目。</p>
<p>Byte 0 – <em>STD_NUM_PAGES</em> (0，0x01) </p></td>
</tr>
<tr class="even">
<td align="left"><strong>第一个供应商页</strong></td>
<td align="left">1</td>
<td align="left">6</td>
<td align="left"><p>供应商特定页的起始页码。</p>
<p>Byte 0 – <em>VENDOR_START_PAGES</em> (0，0x02) </p></td>
</tr>
<tr class="odd">
<td align="left"><strong>供应商页数</strong></td>
<td align="left">1</td>
<td align="left">7</td>
<td align="left"><p>模块支持的特定于供应商的页的数目。</p>
<p>Byte 0 – <em>VENDOR_NUM_PAGES (</em>) </p></td>
</tr>
<tr class="even">
<td align="left"><strong>硬件修订</strong></td>
<td align="left">4</td>
<td align="left">8</td>
<td align="left"><p>控制器硬件修订。</p>
<p>Byte 0 – <em>HWREV</em> (0，0x04) </p>
<p>字节 1-保留。</p>
<p>字节 2-保留。</p>
<p>字节 3-保留。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>固件版本</strong></td>
<td align="left">2</td>
<td align="left">12</td>
<td align="left"><p>活动固件槽的固件版本。</p>
<p>Byte 0 – <em>SLOTX_FWREV0</em> (0，0x07/0x09) </p>
<p>字节1– <em>SLOTX_FWREV1</em> (0、0X08/0x0A) </p></td>
</tr>
<tr class="even">
<td align="left"><strong>当前固件槽</strong></td>
<td align="left">1</td>
<td align="left">14</td>
<td align="left"><p>正在运行的固件映像的插槽号。</p>
<p>字节0– <em>FW_SLOT_INFO</em> 的位 [7:4] (3，0x42) register (<em>RUNNING_FW_SLOT</em>) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>固件槽计数</strong></td>
<td align="left">1</td>
<td align="left">15</td>
<td align="left"><p>可用的固件槽数。 对于 JEDEC 兼容设备，此字段应为2。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>功能</strong></td>
<td align="left">1</td>
<td align="left">16</td>
<td align="left"><p>有关该模块支持的功能的信息。</p>
<p>Byte 0 – <em>CAPABILITIES0</em> (0，0x10) </p>
<p>Byte 1 – <em>CAPABILITIES1</em> (0，0x11) </p></td>
</tr>
<tr class="odd">
<td align="left"><strong>支持的备份触发器</strong></td>
<td align="left">1</td>
<td align="left">17</td>
<td align="left"><p>模块支持的保存触发器。</p>
<p></em>Byte 0 – <em>CSAVE_TRIGGER_SUPPORT (</em>) </p></td>
</tr>
<tr class="even">
<td align="left"><strong>最大操作重试次数</strong></td>
<td align="left">1</td>
<td align="left">18</td>
<td align="left"><p>如果 "保存"、"还原" 或 "清除" 操作失败或超出最大超时值，则为主机推荐的重试次数。</p>
<p>Byte 0 – <em>HOST_MAX_OPERATION_RETRY (</em>) </p></td>
</tr>
<tr class="odd">
<td align="left"><strong>支持的通知事件</strong></td>
<td align="left">1</td>
<td align="left">19</td>
<td align="left"><p>模块将为其生成通知的事件信息。</p>
<p>Byte 0 – <em>EVENT_NOTIFICATION_SUPPORT (</em>) </p></td>
</tr>
<tr class="even">
<td align="left"><strong>保存操作超时</strong></td>
<td align="left">4</td>
<td align="left">20</td>
<td align="left"><p>最坏的情况是以毫秒或秒为单位保存完成延迟。</p>
<p>Byte 0 – <em>CSAVE_TIMEOUT0 (</em>) </p>
<p>字节1– <em>CSAVE_TIMEOUT1</em> (0，0x19) </p>
<p>字节 2-保留。</p>
<p>字节 3-保留。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>还原操作超时</strong></td>
<td align="left">4</td>
<td align="left">24</td>
<td align="left"><p>最坏的情况下，还原完成延迟时间，以毫秒或秒为单位。</p>
<p>Byte 0 – <em>RESTORE_TIMEOUT0 (</em>) </p>
<p>字节1– <em>RESTORE_TIMEOUT1</em> (0，0x1D) </p>
<p>字节 2-保留。</p>
<p>字节 3-保留。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>擦除操作超时</strong></td>
<td align="left">4</td>
<td align="left">28</td>
<td align="left"><p>最坏的情况是以毫秒或秒为单位删除完成延迟。</p>
<p>Byte 0 – <em>ERASE_TIMEOUT0 (</em>) </p>
<p>字节1– <em>ERASE_TIMEOUT1</em> (0，0x1F) </p>
<p>字节 2-保留。</p>
<p>字节 3-保留。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>Arm 操作超时</strong></td>
<td align="left">4</td>
<td align="left">32</td>
<td align="left"><p>最坏的 case 完成延迟，以毫秒或秒为单位。</p>
<p>Byte 0 – <em>ARM_TIMEOUT0</em> (0，0x20) </p>
<p>字节1– <em>ARM_TIMEOUT1</em> (0，0x21) </p>
<p>字节 2-保留。</p>
<p>字节 3-保留。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>固件操作超时</strong></td>
<td align="left">4</td>
<td align="left">36</td>
<td align="left"><p>最坏情况下的固件操作完成延迟，以毫秒或秒为单位。</p>
<p>Byte 0 – <em>FIRMWARE_OPS_TIMEOUT0 (</em>) </p>
<p>字节1– <em>FIRMWARE_OPS_TIMEOUT1</em> (0，0x23) </p>
<p>字节 2-保留。</p>
<p>字节 3-保留。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>中止操作超时</strong></td>
<td align="left">4</td>
<td align="left">40</td>
<td align="left"><p></p>
<p>Byte 0 – <em>ABORT_CMD_TIMEOUT</em> (0，0x24) </p>
<p>Byte 1 – Reserved。</p>
<p>字节 2-保留。</p>
<p>字节 3-保留。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>区域块大小</strong></td>
<td align="left">4</td>
<td align="left">46</td>
<td align="left"><p>区域大小为32个字节的倍数。</p>
<p>Byte 0 – <em>REGION_BLOCK_SIZE (</em>) </p></td>
</tr>
<tr class="even">
<td align="left"><strong>最小运行温度</strong></td>
<td align="left">1</td>
<td align="left">44</td>
<td align="left"><p>最小运行温度（摄氏度）。</p>
<p>Byte 0 – <em>MIN_OPERATING_TEMP0 (</em>) </p>
<p>字节1– <em>MIN_OPERATING_TEMP1</em> (0，0x39) </p></td>
</tr>
<tr class="odd">
<td align="left"><strong>最高操作温度</strong></td>
<td align="left">1</td>
<td align="left">45</td>
<td align="left"><p>最大温度，以摄氏度为单位。</p>
<p>Byte 0 – <em>MAX_OPERATING_TEMP0 (</em>) </p>
<p>字节1– <em>MAX_OPERATING_TEMP1</em> (0，0x3B) </p></td>
</tr>
</tbody>
</table>

## <a name="related-topics"></a>相关主题

[\_用于字节寻址的支持能源的函数类 (函数接口 1) 的 DSM 接口 ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)
