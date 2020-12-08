---
title: 音频驱动程序的规则
description: 音频 (PortCls) 微型端口驱动程序的 DDI 符合性规则验证 PortCls.sys 及其微型端口驱动程序之间的 DDI 接口。
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: d16ea0fde5a6a1f4f28726fc81fccd1d21fc58dc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787621"
---
# <a name="rules-for-audio-drivers"></a>音频驱动程序的规则


音频 (PortCls) 微型端口驱动程序的 DDI 符合性规则验证 PortCls.sys 及其微型端口驱动程序之间的 DDI 接口。

## <a name="in-this-section"></a>在本节中


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
<td align="left"><p>PcAddAdapterDevice 规则指定 PortCls 微型端口驱动程序正确使用 <a href="audio-pcaddadapterdevice.md" data-raw-source="[&lt;strong&gt;PcAddAdapterDevice&lt;/strong&gt;](audio-pcaddadapterdevice.md)"><strong>PcAddAdapterDevice</strong></a> 函数，具体而言， <em>DeviceExtensionSize</em> 应为零 (0) 或小于 PORT_CLASS_DEVICE_EXTENSION_SIZE。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="audio-pcallocateandmappages.md" data-raw-source="[&lt;strong&gt;PcAllocateAndMapPages&lt;/strong&gt;](audio-pcallocateandmappages.md)"><strong>PcAllocateAndMapPages</strong></a></p></td>
<td align="left"><p>PcAllocateAndMapPages 规则指定 PortCls 微型端口驱动程序使用正确的参数调用以下接口：</p>
<ul>
<li>IPortWaveRTStream::AllocatePagesForMdl</li>
<li>IPortWaveRTStream::AllocateContiguousPagesForMdl</li>
<li>IPortWaveRTStream::MapAllocatedPages</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="audio-pcallocatedpages.md" data-raw-source="[&lt;strong&gt;PcAllocatedPages&lt;/strong&gt;](audio-pcallocatedpages.md)"><strong>PcAllocatedPages</strong></a></p></td>
<td align="left"><p>PcAllocatedPages 规则指定 PortCls 微型端口驱动程序通过调用 AllocatePagesForMdl 或 AllocateContiguousPagesForMdl 方法释放以前分配的页面。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="audio-pcirqlddis.md" data-raw-source="[&lt;strong&gt;PcIrqlDDIs&lt;/strong&gt;](audio-pcirqlddis.md)"><strong>PcIrqlDDIs</strong></a></p></td>
<td align="left"><p>PcIrqlDDIs 规则指定 PortCls 微型端口驱动程序必须在正确的 IRQL 级别调用 PortCls DDIs。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="audio-pcirqliport.md" data-raw-source="[&lt;strong&gt;PcIrqlIport&lt;/strong&gt;](audio-pcirqliport.md)"><strong>PcIrqlIport</strong></a></p></td>
<td align="left"><p>PcIrqlIport 规则指定 PortCls 微型端口驱动程序必须在正确的 IRQL 级别调用 PortCls IPort 接口。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="pcporequestpowerirp.md" data-raw-source="[&lt;strong&gt;PcPoRequestPowerIrp&lt;/strong&gt;](pcporequestpowerirp.md)"><strong>PcPoRequestPowerIrp</strong></a></p></td>
<td align="left"><p>此规则验证 PortCls 微型端口驱动程序不应使用<a href="/windows-hardware/drivers/kernel/irp-mn-set-power" data-raw-source="[&lt;strong&gt;IRP_MN_SET_POWER&lt;/strong&gt;](../kernel/irp-mn-set-power.md)"><strong>IRP_MN_SET_POWER</strong></a>调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp" data-raw-source="[&lt;strong&gt;PoRequestPowerIrp&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)"><strong>PoRequestPowerIrp</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="audio-pcpropertyrequest.md" data-raw-source="[&lt;strong&gt;PcPropertyRequest&lt;/strong&gt;](audio-pcpropertyrequest.md)"><strong>PcPropertyRequest</strong></a></p></td>
<td align="left"><p>PcPropertyRequest 规则指定 PortCls 微型端口驱动程序绝不应使用 STATUS_PENDING 的<em>NtStatus</em>值调用<a href="/windows-hardware/drivers/ddi/portcls/nf-portcls-pccompletependingpropertyrequest" data-raw-source="[&lt;strong&gt;PcCompletePendingPropertyRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/portcls/nf-portcls-pccompletependingpropertyrequest)"><strong>PcCompletePendingPropertyRequest</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="audio-pcregisteradapterpower.md" data-raw-source="[&lt;strong&gt;PcRegisterAdapterPower&lt;/strong&gt;](audio-pcregisteradapterpower.md)"><strong>PcRegisterAdapterPower</strong></a></p></td>
<td align="left"><p>PcRegisterAdapterPower 规则指定 PortCls 微型端口驱动程序不应：</p>
<ul>
<li>调用 <a href="/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisteradapterpowermanagement" data-raw-source="[&lt;strong&gt;PcRegisterAdapterPowerManagement&lt;/strong&gt;](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisteradapterpowermanagement)"><strong>PcRegisterAdapterPowerManagement</strong></a> 两次，无需对 <a href="/windows-hardware/drivers/ddi/portcls/nf-portcls-pcunregisteradapterpowermanagement" data-raw-source="[&lt;strong&gt;PcUnregisterAdapterPowerManagement&lt;/strong&gt;](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcunregisteradapterpowermanagement)"><strong>PcUnregisterAdapterPowerManagement</strong></a>调用干预。</li>
<li>请先调用 <a href="/windows-hardware/drivers/ddi/portcls/nf-portcls-pcunregisteradapterpowermanagement" data-raw-source="[&lt;strong&gt;PcUnregisterAdapterPowerManagement&lt;/strong&gt;](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcunregisteradapterpowermanagement)"><strong>PcUnregisterAdapterPowerManagement</strong></a> ，然后再调用 <a href="/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisteradapterpowermanagement" data-raw-source="[&lt;strong&gt;PcRegisterAdapterPowerManagement&lt;/strong&gt;](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisteradapterpowermanagement)"><strong>PcRegisterAdapterPowerManagement</strong></a> 。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="audio-pctimedwavertstreamsetstate.md" data-raw-source="[&lt;strong&gt;PcTimedWaveRtStreamSetState&lt;/strong&gt;](audio-pctimedwavertstreamsetstate.md)"><strong>PcTimedWaveRtStreamSetState</strong></a></p></td>
<td align="left"><p>PcTimedWaveRtStreamSetState 规则指定 ProtCls 微型端口驱动程序通过 <a href="/previous-versions/windows/hardware/drivers/ff536756(v=vs.85)" data-raw-source="[&lt;strong&gt;IMiniportWaveRTStream::SetState&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff536756(v=vs.85))"><strong>IMiniportWaveRTStream：： SetState</strong></a> 在所需时间内进行状态转换。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="audio-pcunmapallocatedpages.md" data-raw-source="[&lt;strong&gt;PcUnmapAllocatedPages&lt;/strong&gt;](audio-pcunmapallocatedpages.md)"><strong>PcUnmapAllocatedPages</strong></a></p></td>
<td align="left"><p>PcUnmapAllocatedPages 规则指定：</p>
<ul>
<li>PortCls 微型端口驱动程序不会映射当前映射的 MDL，而不先取消其映射。</li>
<li>PortCls 微型端口驱动程序在使用 <a href="/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertstream" data-raw-source="[IMiniportWaveRTStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertstream)">IMiniportWaveRTStream</a> 接口释放内存之前 messagebox 取消内存。</li>
</ul></td>
</tr>
</tbody>
</table>

 

