---
title: StorPort 微型端口驱动程序的注册表项
description: StorPort 定义一组注册表项来配置 StorPort 和微型端口操作的行为。
ms.assetid: 543EC6A4-113C-4525-8063-28854B50760E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d449dd4d6051b90abe5e05425df851f3ebc016a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562049"
---
# <a name="registry-entries-for-storport-miniport-drivers"></a>StorPort 微型端口驱动程序的注册表项


StorPort 定义一组注册表项来配置 StorPort 和微型端口操作的行为。 中的微型端口驱动程序或每个实例的作用域可设置值。

## <a name="span-idserviceentriesspanspan-idserviceentriesspanspan-idserviceentriesspanservice-entries"></a><span id="Service_Entries"></span><span id="service_entries"></span><span id="SERVICE_ENTRIES"></span>服务条目


由微型端口的注册表项进行键控*\\参数*子项并*\\参数\\设备*子项的微型端口的服务密钥。 对于单个适配器条目，该子项经过扩展，包括适配器下标，如下所述*\\参数\\Device1*。

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
<td align="left">在任务栏的搜索框中键入</td>
<td align="left">Any</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>微型端口范围：</p>
<p>HKLM\System\CurrentControlSet\Services&amp;lt;miniport name&gt;\Parameters\Device</p>
<p>适配器作用域：</p>
<p>HKLM\System\CurrentControlSet\Services&amp;lt;miniport name&gt;\Parameters\Device&lt;adapter#&gt;</p></td>
</tr>
<tr class="even">
<td align="left">ReplTest1</td>
<td align="left"><p>任何微型端口特定的数据。</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>Storport 检索此注册表数据，并将缓冲区传递到作为微型端口<em>参数</em>时，它调用的微型端口<a href="https://msdn.microsoft.com/library/windows/hardware/ff557390" data-raw-source="[&lt;strong&gt;HwStorFindAdapter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557390)"> <strong>HwStorFindAdapter</strong> </a>例程。</p></td>
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
<td align="left">在任务栏的搜索框中键入</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>微型端口范围：</p>
<p>HKLM\System\CurrentControlSet\Services&amp;lt;miniport name&gt;\Parameters\Device</p>
<p>适配器作用域：</p>
<p>HKLM\System\CurrentControlSet\Services&amp;lt;miniport name&gt;\Parameters\Device&lt;adapter#&gt;</p></td>
</tr>
<tr class="even">
<td align="left">ReplTest1</td>
<td align="left"><p>Default：30</p>
<p>最长：600</p>
<p>单位： 秒</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>微型端口驱动程序使用此值以通知 Storport、 链接中断，如何长时间后重新启动到微型端口驱动程序的 I/O 之前应等待 StorPort。</p></td>
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
<td align="left">在任务栏的搜索框中键入</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>微型端口范围：</p>
<p>HKLM\System\CurrentControlSet\Services&amp;lt;miniport name&gt;\Parameters\Device</p>
<p>适配器作用域：</p>
<p>HKLM\System\CurrentControlSet\Services&amp;lt;miniport name&gt;\Parameters\Device&lt;adapter#&gt;</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>Default：255</p>
<p>最长：如果在注册表中设置的 8</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>此值设置为目标设备的逻辑单元 (LUN) 的最大数目。</p></td>
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
<td align="left">在任务栏的搜索框中键入</td>
<td align="left">REG_BINARY</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>微型端口范围：</p>
<p>HKLM\System\CurrentControlSet\Services&amp;lt;miniport name&gt;\Parameters\Device</p>
<p>适配器作用域：</p>
<p>HKLM\System\CurrentControlSet\Services&amp;lt;miniport name&gt;\Parameters\Device&lt;adapter#&gt;</p></td>
</tr>
<tr class="even">
<td align="left">ReplTest1</td>
<td align="left"><p>Default：0xffffffff</p>
<p>StorPort 时 0，使用默认值</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>此值设置未缓存扩展的最大的地址值。</p></td>
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
<td align="left">在任务栏的搜索框中键入</td>
<td align="left">REG_BINARY</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>微型端口范围：</p>
<p>HKLM\System\CurrentControlSet\Services&amp;lt;miniport name&gt;\Parameters\Device</p>
<p>适配器作用域：</p>
<p>HKLM\System\CurrentControlSet\Services&amp;lt;miniport name&gt;\Parameters\Device&lt;adapter#&gt;</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>Default：0x00000000</p>
<p>当 MinimumUCXAddress &gt;= MaximumUCXAddress-PAGE_SIZE、 StorPort 使用默认值。</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>此值设置未缓存扩展的最小地址值。</p></td>
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
<td align="left">“属性”</td>
<td align="left"><strong>UncachedExtAlignment</strong></td>
</tr>
<tr class="even">
<td align="left">在任务栏的搜索框中键入</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>微型端口范围：</p>
<p>HKLM\System\CurrentControlSet\Services&amp;lt;miniport name&gt;\Parameters\Device</p>
<p>适配器作用域：</p>
<p>HKLM\System\CurrentControlSet\Services&amp;lt;miniport name&gt;\Parameters\Device&lt;adapter#&gt;</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>Default：0</p>
<p>最低：3</p>
<p>最长：16</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>StorPort 使用此值来计算基本的 2 个指数 (例如 1 &lt; &lt;值) 用作未缓存的扩展缓冲区分配的对齐值。</p></td>
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
<td align="left">在任务栏的搜索框中键入</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>微型端口范围：</p>
<p>HKLM\System\CurrentControlSet\Services&amp;lt;miniport name&gt;\Parameters\Device</p>
<p>适配器作用域：</p>
<p>HKLM\System\CurrentControlSet\Services&amp;lt;miniport name&gt;\Parameters\Device&lt;adapter#&gt;</p></td>
</tr>
<tr class="even">
<td align="left">ReplTest1</td>
<td align="left"><p>Default：1000</p>
<p>最低：16</p>
<p>最长：255</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>适配器可以处理的请求或数。 设置时，范围为小于默认值。</p></td>
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
<td align="left">在任务栏的搜索框中键入</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>微型端口范围：</p>
<p>HKLM\System\CurrentControlSet\Services&amp;lt;miniport name&gt;\Parameters</p></td>
</tr>
<tr class="even">
<td align="left">ReplTest1</td>
<td align="left"><p>Default：6, <strong>BusTypeFiber</strong></p>
<p>最长：0x7f，更高版本的任何值被视为默认值。</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>此值用于指示微型端口驱动程序管理的适配器的总线类型。 值对应于总线枚举类型：<strong>STORAGE_BUS_TYPE</strong>。</p></td>
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
<td align="left">在任务栏的搜索框中键入</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>微型端口范围：</p>
<p>HKLM\System\CurrentControlSet\Services&amp;lt;miniport name&gt;\Parameters</p></td>
</tr>
<tr class="even">
<td align="left">ReplTest1</td>
<td align="left"><p>最低：0</p>
<p>最长：65535</p>
<p>单位： 秒</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>指示由微型端口驱动程序管理的设备的 I/O 超时值。 如果不存在此注册表值，则系统将使用全局磁盘 I/O 超时值。</p></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>随着 Windows 8 启动。</p></td>
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
<td align="left">“属性”</td>
<td align="left"><strong>IoLatencyCap</strong></td>
</tr>
<tr class="even">
<td align="left">在任务栏的搜索框中键入</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>微型端口范围：</p>
<p>HKLM\System\CurrentControlSet\Services&amp;lt;miniport name&gt;\Parameters</p></td>
</tr>
<tr class="even">
<td align="left">ReplTest1</td>
<td align="left"><p>Default：0</p>
<p>单位： 毫秒</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>如果此注册表值为&gt;0，StorPort 将传入的 I/O 请求在队列中时保存任何 I/O 请求发送到微型端口驱动程序未在指定的时间段内完成。</p></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>随着 Windows 8 启动。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-iddeviceenumerationentriesspanspan-iddeviceenumerationentriesspanspan-iddeviceenumerationentriesspandevice-enumeration-entries"></a><span id="Device_Enumeration_Entries"></span><span id="device_enumeration_entries"></span><span id="DEVICE_ENUMERATION_ENTRIES"></span>设备枚举项


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">“属性”</td>
<td align="left"><strong>TotalSenseDataBytes</strong></td>
</tr>
<tr class="even">
<td align="left">在任务栏的搜索框中键入</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>适配器作用域：</p>
<p>HKLM\System\CurrentControlSet\Enum&amp;lt;instance path&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">ReplTest1</td>
<td align="left"><p>Default：255</p>
<p>最低：18</p>
<p>最长：255</p>
<p>单元： 字节</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>指示<em>检测数据</em>StorPort 微型端口驱动程序返回的大小。</p></td>
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
<td align="left">“属性”</td>
<td align="left"><strong>QueueFullWaitIoPercentage</strong></td>
</tr>
<tr class="even">
<td align="left">在任务栏的搜索框中键入</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>逻辑单元作用域：</p>
<p>HKLM\CurrentControlSet\Enum\SCSI&amp;lt;HardwareId&gt;&amp;lt;InstanceId&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">ReplTest1</td>
<td align="left"><p>Default：25</p>
<p>最长：100</p>
<p>单位：队列深度的百分比</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>当微型端口报告设备忙通过设置<strong>SCSISTAT_QUEUE_FULL</strong>中<strong>ScsiStatus</strong>的<strong>SRB</strong>，StorPort 暂停逻辑单元队列，并等待一定我/O 请求发送的任何请求之前完成的微型端口。 使用此注册表值相对于当前微型端口到发送的 I/O 请求数计算的 StorPort 等待 I/O 请求数。</p></td>
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
<td align="left">在任务栏的搜索框中键入</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>逻辑单元作用域：</p>
<p>HKLM\CurrentControlSet\Enum\SCSI&amp;lt;HardwareId&gt;&amp;lt;InstanceId&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">ReplTest1</td>
<td align="left"><p>Default：250</p>
<p>单位： 毫秒</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>当微型端口报告设备忙通过设置<strong>SRB_STATUS_BUSY</strong>中<strong>SrbStatus</strong>的<strong>SRB</strong>，StorPort 暂停单元队列，等待指定的时间之前启动重新发送的 I/O 请求。</p></td>
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
<td align="left">“属性”</td>
<td align="left"><strong>BusyPauseTime</strong></td>
</tr>
<tr class="even">
<td align="left">在任务栏的搜索框中键入</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>逻辑单元作用域：</p>
<p>HKLM\CurrentControlSet\Enum\SCSI&amp;lt;HardwareId&gt;&amp;lt;InstanceId&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>Default：250</p>
<p>单位： 毫秒</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>当微型端口报告设备忙通过设置<strong>SRB_STATUS_BUSY</strong>中<strong>SrbStatus</strong>的<strong>SRB</strong>，StorPort 暂停逻辑单元队列，等待指定开始重新发送的 I/O 请求之前的长时间。</p></td>
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
<td align="left">在任务栏的搜索框中键入</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>逻辑单元作用域：</p>
<p>HKLM\CurrentControlSet\Enum\SCSI&amp;lt;HardwareId&gt;&amp;lt;InstanceId&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">ReplTest1</td>
<td align="left"><p>Default：10</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>StorPort 以重新颁发的重试<strong>Srb</strong>微型端口时向下报告了设备繁忙或链接。</p></td>
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
<td align="left">在任务栏的搜索框中键入</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>适配器作用域：</p>
<p>HKLM\System\CurrentControlSet\Enum&amp;lt;instance path&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>Default：0 禁用</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>如果此注册表值为&gt;启用了 0，则空闲电源管理。 空闲的电源管理适用于连接到适配器的逻辑单元。</p></td>
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
<td align="left">“属性”</td>
<td align="left"><strong>DisableIdlePowerManagement</strong></td>
</tr>
<tr class="even">
<td align="left">在任务栏的搜索框中键入</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>逻辑单元作用域：</p>
<p>HKLM\CurrentControlSet\Enum\SCSI&amp;lt;HardwareId&gt;&amp;lt;InstanceId&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>Default：0 启用</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>如果此注册表值为&gt;0，则空闲电源管理禁用为此逻辑单元。</p></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>随着 Windows 8 启动。</p></td>
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
<td align="left">在任务栏的搜索框中键入</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>逻辑单元作用域：</p>
<p>HKLM\CurrentControlSet\Enum\SCSI&amp;lt;HardwareId&gt;&amp;lt;InstanceId&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">ReplTest1</td>
<td align="left"><p>Default：MAXULONG，指示未设置。 如果微型端口不提供任何超时值，实际默认值是 5 分钟或 5 * 60 * 1000。</p>
<p>单位： 毫秒</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>此值指定的最小电源框架必须等待关闭逻辑单元的电源后在空闲时间量。</p></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>随着 Windows 8 启动。</p></td>
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
<td align="left">“属性”</td>
<td align="left"><strong>DisableRuntimePowerManagement</strong></td>
</tr>
<tr class="even">
<td align="left">在任务栏的搜索框中键入</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>适配器作用域：</p>
<p>HKLM\System\CurrentControlSet\Enum&amp;lt;instance path&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>默认值： 已启用</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>如果值&gt;0，则运行时的适配器的电源管理会禁用。 这会禁用为特定的适配器运行时电源管理。</p>
<div class="alert">
<strong>请注意</strong>  运行时电源管理的设备连接到此适配器不会受到影响。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>随着 Windows 8 启动。</p></td>
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
<td align="left">在任务栏的搜索框中键入</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>适配器作用域：</p>
<p>HKLM\System\CurrentControlSet\Enum&amp;lt;instance path&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>Default：60</p>
<p>单位： 秒</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>指定的时间该运行时电源框架需要关闭空闲适配器前等待。</p></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>随着 Windows 8 启动。</p></td>
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
<td align="left">在任务栏的搜索框中键入</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">路径</td>
<td align="left"><p>适配器作用域：</p>
<p>HKLM\System\CurrentControlSet\Enum&amp;lt;instance path&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">值</td>
<td align="left"><p>默认值： 已启用 （如果支持 D3Cold）</p></td>
</tr>
<tr class="odd">
<td align="left">描述</td>
<td align="left"><p>如果值&gt;0，则 D3Cold 支持的适配器处于禁用状态。</p></td>
</tr>
<tr class="even">
<td align="left">应用</td>
<td align="left"><p>随着 Windows 8 启动。</p></td>
</tr>
</tbody>
</table>

 

 

 




