---
title: 音频驱动程序的规则
description: 音频 (PortCls) 微型端口驱动程序的 DDI 符合性规则验证 PortCls.sys 和其微型端口驱动程序之间的 DDI 接口。
ms.assetid: 65078F78-B7F2-41A7-BD3B-A90A4A77750F
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: f553a2646aa231db3ed31543b1a36197cdbcde5b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542409"
---
# <a name="rules-for-audio-drivers"></a>音频驱动程序的规则


音频 (PortCls) 微型端口驱动程序的 DDI 符合性规则验证 PortCls.sys 和其微型端口驱动程序之间的 DDI 接口。

## <a name="in-this-section"></a>本部分内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="audio-pcaddadapterdevice.md" data-raw-source="[&lt;strong&gt;PcAddAdapterDevice&lt;/strong&gt;](audio-pcaddadapterdevice.md)"><strong>PcAddAdapterDevice</strong></a></p></td>
<td align="left"><p>PcAddAdapterDevice 规则指定 PortCls 微型端口驱动程序正确使用<a href="audio-pcaddadapterdevice.md" data-raw-source="[&lt;strong&gt;PcAddAdapterDevice&lt;/strong&gt;](audio-pcaddadapterdevice.md)"> <strong>PcAddAdapterDevice</strong> </a>函数，具体而言， <em>DeviceExtensionSize</em>应为零 (0) 或不短于 PORT_CLASS_DEVICE_EXTENSION_SIZE。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="audio-pcallocateandmappages.md" data-raw-source="[&lt;strong&gt;PcAllocateAndMapPages&lt;/strong&gt;](audio-pcallocateandmappages.md)"><strong>PcAllocateAndMapPages</strong></a></p></td>
<td align="left"><p>PcAllocateAndMapPages 规则指定 PortCls 微型端口驱动程序调用以下接口，使用正确的参数：</p>
<ul>
<li>IPortWaveRTStream::AllocatePagesForMdl</li>
<li>IPortWaveRTStream::AllocateContiguousPagesForMdl</li>
<li>IPortWaveRTStream::MapAllocatedPages</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="audio-pcallocatedpages.md" data-raw-source="[&lt;strong&gt;PcAllocatedPages&lt;/strong&gt;](audio-pcallocatedpages.md)"><strong>PcAllocatedPages</strong></a></p></td>
<td align="left"><p>PcAllocatedPages 规则指定 PortCls 微型端口驱动程序通过调用 AllocatePagesForMdl 或 AllocateContiguousPagesForMdl 方法释放以前分配的页。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="audio-pcirqlddis.md" data-raw-source="[&lt;strong&gt;PcIrqlDDIs&lt;/strong&gt;](audio-pcirqlddis.md)"><strong>PcIrqlDDIs</strong></a></p></td>
<td align="left"><p>PcIrqlDDIs 规则指定，PortCls 微型端口驱动程序必须调用 PortCls DDIs 在正确的 IRQL 级别。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="audio-pcirqliport.md" data-raw-source="[&lt;strong&gt;PcIrqlIport&lt;/strong&gt;](audio-pcirqliport.md)"><strong>PcIrqlIport</strong></a></p></td>
<td align="left"><p>PcIrqlIport 规则指定，PortCls 微型端口驱动程序必须调用 PortCls IPort 接口在正确的 IRQL 级别。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="pcporequestpowerirp.md" data-raw-source="[&lt;strong&gt;PcPoRequestPowerIrp&lt;/strong&gt;](pcporequestpowerirp.md)"><strong>PcPoRequestPowerIrp</strong></a></p></td>
<td align="left"><p>此规则验证 PortCls 微型端口驱动程序不应调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff559734" data-raw-source="[&lt;strong&gt;PoRequestPowerIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559734)"> <strong>PoRequestPowerIrp</strong> </a>与<a href="https://msdn.microsoft.com/library/windows/hardware/ff551744" data-raw-source="[&lt;strong&gt;IRP_MN_SET_POWER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551744)"> <strong>IRP_MN_SET_POWER</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="audio-pcpropertyrequest.md" data-raw-source="[&lt;strong&gt;PcPropertyRequest&lt;/strong&gt;](audio-pcpropertyrequest.md)"><strong>PcPropertyRequest</strong></a></p></td>
<td align="left"><p>PcPropertyRequest 规则指定 PortCls 微型端口驱动程序应永远不会调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff537687" data-raw-source="[&lt;strong&gt;PcCompletePendingPropertyRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537687)"> <strong>PcCompletePendingPropertyRequest</strong> </a>与<em>NtStatus</em> STATUS_ 值挂起。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="audio-pcregisteradapterpower.md" data-raw-source="[&lt;strong&gt;PcRegisterAdapterPower&lt;/strong&gt;](audio-pcregisteradapterpower.md)"><strong>PcRegisterAdapterPower</strong></a></p></td>
<td align="left"><p>PcRegisterAdapterPower 规则指定 PortCls 微型端口驱动程序不应：</p>
<ul>
<li>调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff537724" data-raw-source="[&lt;strong&gt;PcRegisterAdapterPowerManagement&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537724)"> <strong>PcRegisterAdapterPowerManagement</strong> </a>两次而无需对的干预调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff537735" data-raw-source="[&lt;strong&gt;PcUnregisterAdapterPowerManagement&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537735)"> <strong>PcUnregisterAdapterPowerManagement</strong></a>。</li>
<li>调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff537735" data-raw-source="[&lt;strong&gt;PcUnregisterAdapterPowerManagement&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537735)"> <strong>PcUnregisterAdapterPowerManagement</strong> </a>而无需调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff537724" data-raw-source="[&lt;strong&gt;PcRegisterAdapterPowerManagement&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537724)"> <strong>PcRegisterAdapterPowerManagement</strong> </a>第一个。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="audio-pctimedwavertstreamsetstate.md" data-raw-source="[&lt;strong&gt;PcTimedWaveRtStreamSetState&lt;/strong&gt;](audio-pctimedwavertstreamsetstate.md)"><strong>PcTimedWaveRtStreamSetState</strong></a></p></td>
<td align="left"><p>PcTimedWaveRtStreamSetState 规则指定 ProtCls 微型端口驱动程序，可通过状态转换<a href="https://msdn.microsoft.com/library/windows/hardware/ff536756" data-raw-source="[&lt;strong&gt;IMiniportWaveRTStream::SetState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536756)"> <strong>IMiniportWaveRTStream::SetState</strong> </a>内所需的时间。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="audio-pcunmapallocatedpages.md" data-raw-source="[&lt;strong&gt;PcUnmapAllocatedPages&lt;/strong&gt;](audio-pcunmapallocatedpages.md)"><strong>PcUnmapAllocatedPages</strong></a></p></td>
<td align="left"><p>PcUnmapAllocatedPages 规则指定：</p>
<ul>
<li>PortCls 微型端口驱动程序不&#39;t 映射当前映射而无需第一个取消映射 MDL。</li>
<li>PortCls 微型端口驱动程序取消映射之前释放其使用的内存<a href="https://msdn.microsoft.com/library/windows/hardware/ff536738" data-raw-source="[IMiniportWaveRTStream](https://msdn.microsoft.com/library/windows/hardware/ff536738)">IMiniportWaveRTStream</a>接口。</li>
</ul></td>
</tr>
</tbody>
</table>

 

 

 





