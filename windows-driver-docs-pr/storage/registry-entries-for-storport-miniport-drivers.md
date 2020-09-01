---
title: StorPort 微型端口驱动程序的注册表项
description: StorPort 定义一组注册表项，以配置 StorPort 和微型端口操作的行为。
ms.assetid: 543EC6A4-113C-4525-8063-28854B50760E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7909b2e96c6ac885a97991d46d00cb4a8e19e680
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189245"
---
# <a name="registry-entries-for-storport-miniport-drivers"></a>StorPort 微型端口驱动程序的注册表项


StorPort 定义一组注册表项，以配置 StorPort 和微型端口操作的行为。 值是在微型端口驱动程序或每个实例的作用域中设置的。

## <a name="span-idservice_entriesspanspan-idservice_entriesspanspan-idservice_entriesspanservice-entries"></a><span id="Service_Entries"></span><span id="service_entries"></span><span id="SERVICE_ENTRIES"></span>服务项


微型端口的注册表项由* \\ 参数*子项和微型端口的服务密钥的* \\ 参数 \\ 设备*子项键控。 对于单个适配器条目，该子项已扩展为包含适配器索引，如* \\ 参数 \\ Device1*。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名称</td>
<td align="left"><strong>DriverParameter</strong></td>
</tr>
<tr class="even">
<td align="left">类型</td>
<td align="left">任意</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>微型端口范围：</p>
<p>HKLM\System\CurrentControlSet\Services &lt; 微型端口名称 &gt; \Parameters\Device</p>
<p>适配器作用域：</p>
<p>HKLM\System\CurrentControlSet\Services &lt; 微型端口名称 &gt; \Parameters\Device &lt; 适配器#&gt;</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>任何微型端口特定数据。</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>Storport 检索此注册表数据，并在它调用微型端口的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter" data-raw-source="[&lt;strong&gt;HwStorFindAdapter&lt;/strong&gt;](/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)"><strong>HwStorFindAdapter</strong></a>例程时将缓冲区作为<em>参数</em>传递给微型端口。</p></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>从 Windows Server 2003 开始。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名称</td>
<td align="left"><strong>LinkDownTimeoutValue</strong></td>
</tr>
<tr class="even">
<td align="left">类型</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>微型端口范围：</p>
<p>HKLM\System\CurrentControlSet\Services &lt; 微型端口名称 &gt; \Parameters\Device</p>
<p>适配器作用域：</p>
<p>HKLM\System\CurrentControlSet\Services &lt; 微型端口名称 &gt; \Parameters\Device &lt; 适配器#&gt;</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>默认值：30</p>
<p>最大值：600</p>
<p>单位：秒</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>此值由微型端口驱动程序用来通知 Storport，链接关闭后，在重新启动到微型端口驱动程序的 i/o 之前，StorPort 应等待多长时间。</p></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>从 Windows Server 2003 开始。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名称</td>
<td align="left"><strong>MaximumLogicalUnit</strong></td>
</tr>
<tr class="even">
<td align="left">类型</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>微型端口范围：</p>
<p>HKLM\System\CurrentControlSet\Services &lt; 微型端口名称 &gt; \Parameters\Device</p>
<p>适配器作用域：</p>
<p>HKLM\System\CurrentControlSet\Services &lt; 微型端口名称 &gt; \Parameters\Device &lt; 适配器#&gt;</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>默认值：255</p>
<p>最大值：在注册表中设置为8</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>此值设置目标设备 (LUN) 的最大逻辑单元数。</p></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>从 Windows Server 2003 开始。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名称</td>
<td align="left"><strong>MaximumUCXAddress</strong></td>
</tr>
<tr class="even">
<td align="left">类型</td>
<td align="left">REG_BINARY</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>微型端口范围：</p>
<p>HKLM\System\CurrentControlSet\Services &lt; 微型端口名称 &gt; \Parameters\Device</p>
<p>适配器作用域：</p>
<p>HKLM\System\CurrentControlSet\Services &lt; 微型端口名称 &gt; \Parameters\Device &lt; 适配器#&gt;</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>默认值：0xffffffff</p>
<p>如果为0，则 StorPort 使用默认值</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>此值设置非缓存扩展的最大地址值。</p></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>从 Windows Server 2003 开始。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名称</td>
<td align="left"><strong>MinimumUCXAddress</strong></td>
</tr>
<tr class="even">
<td align="left">类型</td>
<td align="left">REG_BINARY</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>微型端口范围：</p>
<p>HKLM\System\CurrentControlSet\Services &lt; 微型端口名称 &gt; \Parameters\Device</p>
<p>适配器作用域：</p>
<p>HKLM\System\CurrentControlSet\Services &lt; 微型端口名称 &gt; \Parameters\Device &lt; 适配器#&gt;</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>默认值：0x00000000</p>
<p>如果 MinimumUCXAddress &gt; = PAGE_SIZE MaximumUCXAddress，则 StorPort 使用默认值。</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>此值设置非缓存扩展的最小地址值。</p></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>从 Windows Server 2003 开始。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名称</td>
<td align="left"><strong>UncachedExtAlignment</strong></td>
</tr>
<tr class="even">
<td align="left">类型</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>微型端口范围：</p>
<p>HKLM\System\CurrentControlSet\Services &lt; 微型端口名称 &gt; \Parameters\Device</p>
<p>适配器作用域：</p>
<p>HKLM\System\CurrentControlSet\Services &lt; 微型端口名称 &gt; \Parameters\Device &lt; 适配器#&gt;</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>默认值：0</p>
<p>最小值：3</p>
<p>最大值：16</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>StorPort 使用此值计算以2为底的指数 (例如 1 &lt; &lt; 值) ，以用作未缓存扩展缓冲区分配的对齐值。</p></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>从 Windows Server 2003 开始。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名称</td>
<td align="left"><strong>NumberOfRequests</strong></td>
</tr>
<tr class="even">
<td align="left">类型</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>微型端口范围：</p>
<p>HKLM\System\CurrentControlSet\Services &lt; 微型端口名称 &gt; \Parameters\Device</p>
<p>适配器作用域：</p>
<p>HKLM\System\CurrentControlSet\Services &lt; 微型端口名称 &gt; \Parameters\Device &lt; 适配器#&gt;</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>默认值：1000</p>
<p>最小值：16</p>
<p>最大值：255</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>适配器可处理的一个或多个请求。 设置后，范围小于默认值。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名称</td>
<td align="left"><strong>BusType</strong></td>
</tr>
<tr class="even">
<td align="left">类型</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>微型端口范围：</p>
<p>HKLM\System\CurrentControlSet\Services &lt; 微型端口名称 &gt; \Parameters</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>默认值：6， <strong>BusTypeFiber</strong></p>
<p>最大值：0x7f，任何大于的值都被视为默认值。</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>此值用于指示微型端口驱动程序管理的适配器的总线类型。 该值对应于总线枚举类型： <strong>STORAGE_BUS_TYPE</strong>。</p></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>从 Windows Server 2003 开始。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名称</td>
<td align="left"><strong>IoTimeoutValue</strong></td>
</tr>
<tr class="even">
<td align="left">类型</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>微型端口范围：</p>
<p>HKLM\System\CurrentControlSet\Services &lt; 微型端口名称 &gt; \Parameters</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>最小值：0</p>
<p>最大值：65535</p>
<p>单位：秒</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>指示微型端口驱动程序管理的设备的 i/o 超时值。 如果此注册表值不存在，系统将使用全局磁盘 i/o 超时值。</p></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>从 Windows 8 开始。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名称</td>
<td align="left"><strong>IoLatencyCap</strong></td>
</tr>
<tr class="even">
<td align="left">类型</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>微型端口范围：</p>
<p>HKLM\System\CurrentControlSet\Services &lt; 微型端口名称 &gt; \Parameters</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>默认值：0</p>
<p>单位：毫秒</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>如果此注册表值为 &gt; 0，则在指定的时间段内，如果发送到微型端口驱动程序的任何 i/o 请求未完成，则 StorPort 会将传入 i/o 请求保存在队列中。</p></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>从 Windows 8 开始。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-iddevice_enumeration_entriesspanspan-iddevice_enumeration_entriesspanspan-iddevice_enumeration_entriesspandevice-enumeration-entries"></a><span id="Device_Enumeration_Entries"></span><span id="device_enumeration_entries"></span><span id="DEVICE_ENUMERATION_ENTRIES"></span>设备枚举条目


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名称</td>
<td align="left"><strong>TotalSenseDataBytes</strong></td>
</tr>
<tr class="even">
<td align="left">类型</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>适配器作用域：</p>
<p>HKLM\System\CurrentControlSet\Enum &lt; 实例路径 &gt; \Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>默认值：255</p>
<p>最小值：18</p>
<p>最大值：255</p>
<p>单位：字节</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>指示微型端口驱动程序返回到 StorPort 的 <em>感知数据</em> 大小。</p></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>从 Windows Server 2003 开始。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名称</td>
<td align="left"><strong>QueueFullWaitIoPercentage</strong></td>
</tr>
<tr class="even">
<td align="left">类型</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>逻辑单元范围：</p>
<p>HKLM\CurrentControlSet\Enum\SCSI &lt; HardwareId &gt; &lt; InstanceId &gt; \Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>默认值：25</p>
<p>最大值：100</p>
<p>单位：队列深度百分比</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>当微型端口通过在<strong>SRB</strong>的<strong>ScsiStatus</strong>中设置<strong>SCSISTAT_QUEUE_FULL</strong>来报告设备繁忙情况时，StorPort 将暂停逻辑单元队列，并等待，直到在发送任何其他请求之前，小型端口完成特定的 i/o 请求。 根据当前发送到小型端口的 i/o 请求计数，使用此注册表值计算 StorPort 等待的 i/o 请求量。</p></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>从 Windows Server 2003 开始。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名称</td>
<td align="left"><strong>BusyPauseTime</strong></td>
</tr>
<tr class="even">
<td align="left">类型</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>逻辑单元范围：</p>
<p>HKLM\CurrentControlSet\Enum\SCSI &lt; HardwareId &gt; &lt; InstanceId &gt; \Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>默认值：250</p>
<p>单位：毫秒</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>当微型端口通过在<strong>SRB</strong>的<strong>SrbStatus</strong>中设置<strong>SRB_STATUS_BUSY</strong>来报告设备忙时，StorPort 将暂停单元队列并等待指定的时间，然后再开始发送 i/o 请求。</p></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>从 Windows Server 2003 开始。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名称</td>
<td align="left"><strong>BusyPauseTime</strong></td>
</tr>
<tr class="even">
<td align="left">类型</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>逻辑单元范围：</p>
<p>HKLM\CurrentControlSet\Enum\SCSI &lt; HardwareId &gt; &lt; InstanceId &gt; \Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>默认值：250</p>
<p>单位：毫秒</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>当微型端口通过在<strong>SRB</strong>的<strong>SrbStatus</strong>中设置<strong>SRB_STATUS_BUSY</strong>来报告设备忙时，StorPort 将暂停逻辑单元队列并等待指定的时间，然后再开始发送 i/o 请求。</p></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>从 Windows Server 2003 开始。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名称</td>
<td align="left"><strong>BusyRetryCount</strong></td>
</tr>
<tr class="even">
<td align="left">类型</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>逻辑单元范围：</p>
<p>HKLM\CurrentControlSet\Enum\SCSI &lt; HardwareId &gt; &lt; InstanceId &gt; \Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>默认值：10</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>当微型端口报告设备忙或链接关闭时，重试 StorPort 重新发出 <strong>Srb</strong> 。</p></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>从 Windows Server 2003 开始。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名称</td>
<td align="left"><strong>EnableIdlePowerManagement</strong></td>
</tr>
<tr class="even">
<td align="left">类型</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>适配器作用域：</p>
<p>HKLM\System\CurrentControlSet\Enum &lt; 实例路径 &gt; \Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>默认值：0，已禁用</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>如果此注册表值为 &gt; 0，则启用空闲电源管理。 空闲电源管理适用于连接到适配器的逻辑单元。</p></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>从 Windows 7 开始。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名称</td>
<td align="left"><strong>DisableIdlePowerManagement</strong></td>
</tr>
<tr class="even">
<td align="left">类型</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>逻辑单元范围：</p>
<p>HKLM\CurrentControlSet\Enum\SCSI &lt; HardwareId &gt; &lt; InstanceId &gt; \Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>默认值：0，已启用</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>如果此注册表值为 &gt; 0，则将为此逻辑单元禁用空闲电源管理。</p></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>从 Windows 8 开始。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名称</td>
<td align="left"><strong>MinimumIdleTimeoutInMS</strong></td>
</tr>
<tr class="even">
<td align="left">类型</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>逻辑单元范围：</p>
<p>HKLM\CurrentControlSet\Enum\SCSI &lt; HardwareId &gt; &lt; InstanceId &gt; \Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>默认值： MAXULONG，指示未设置。 如果微型端口未提供超时值，则实际默认值为5分钟，即 5 * 60 * 1000。</p>
<p>单位：毫秒</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>此值指定在逻辑单元处于空闲状态后，power framework 必须等待的最短时间。</p></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>从 Windows 8 开始。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名称</td>
<td align="left"><strong>DisableRuntimePowerManagement</strong></td>
</tr>
<tr class="even">
<td align="left">类型</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>适配器作用域：</p>
<p>HKLM\System\CurrentControlSet\Enum &lt; 实例路径 &gt; \Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>默认值：已启用</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>如果值为 &gt; 0，则禁用 "适配器的运行时电源管理"。 这会禁用特定适配器的运行时电源管理。</p>
<div class="alert">
<strong>注意</strong>   附加到此适配器的设备的运行时电源管理不受影响。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>从 Windows 8 开始。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名称</td>
<td align="left"><strong>IdleTimeoutInMS</strong></td>
</tr>
<tr class="even">
<td align="left">类型</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>适配器作用域：</p>
<p>HKLM\System\CurrentControlSet\Enum &lt; 实例路径 &gt; \Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>默认：60</p>
<p>单位：秒</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>指定在关闭空闲适配器之前运行时电源框架需要等待的时间。</p></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>从 Windows 8 开始。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名称</td>
<td align="left"><strong>DisableD3Cold</strong></td>
</tr>
<tr class="even">
<td align="left">类型</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>适配器作用域：</p>
<p>HKLM\System\CurrentControlSet\Enum &lt; 实例路径 &gt; \Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>默认值：支持 D3Cold 时启用 () </p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>如果值 &gt; 为0，则禁用对适配器的 D3Cold 支持。</p></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>从 Windows 8 开始。</p></td>
</tr>
</tbody>
</table>

 

 

