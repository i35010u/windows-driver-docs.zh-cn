---
title: WDI_TLV_DATAPATH_CAPABILITIES
description: WDI_TLV_DATAPATH_CAPABILITIES 是包含数据路径功能的 TLV。
ms.assetid: 7B545858-56A2-4655-91D5-37CA4EB61E1E
ms.date: 07/18/2017
keywords:
- WDI_TLV_DATAPATH_CAPABILITIES 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2120ebfc5bf9fc9d93ae75f0e4a97eae3ca40598
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844502"
---
# <a name="wdi_tlv_datapath_capabilities"></a>WDI\_TLV\_数据路径\_功能


WDI\_TLV\_数据路径\_功能是包含数据路径功能的 TLV。

## <a name="tlv-type"></a>TLV 类型


0xB9

## <a name="length"></a>长度


所有包含的元素的大小的总和（以字节为单位）。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>在任务栏的搜索框中键入</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ne-dot11wdi-_wdi_interconnect_type" data-raw-source="[&lt;strong&gt;WDI_INTERCONNECT_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ne-dot11wdi-_wdi_interconnect_type)"><strong>WDI_INTERCONNECT_TYPE</strong></a> （UINT32）</td>
<td>互连类型。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>对等方的最大数目。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>指定传输功能：目标优先级队列。
<p>有效值为0和1。 如果设置为0，则 WDI 将按对等机和 TID 来分类 Tx 帧，并利用完整计划程序选择要传输的 TX 队列。 建议将此值设置为 false，除非目标能够进行分类和对等互连。 如果设置为1，则 WDI 会按对等互连和 TID 来分类 Tx 帧，并且仅在端口级别提供队列。 WDI 使用全局 DRR 计划囤积的端口队列。</p></td>
</tr>
<tr class="even">
<td>UINT16</td>
<td>指定传输功能：帧中的最大散播集合元素数。
<p>WDI 根据需要合并帧，以便 IHV 微型端口不会接收到需要超过此功能所指定的分散收集元素的帧。 为了获得最佳性能，建议将此功能设置为高于典型帧，因为合并需要内存复制。 如果此功能不大于最大帧大小除以页面大小，则 WDI 可能无法成功合并该帧，可能会将其删除。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>指定传输功能：需要显式发送完成标志。
<p>有效值为0和1。 如果设置为0，则目标/TAL 将为所有帧生成 TX 发送完成。 如果设置为1，则仅针对在框架的元数据中设置了此标志的帧生成 TX 发送完成指示。</p></td>
</tr>
<tr class="even">
<td>UINT16</td>
<td>指定传输功能：最小有效帧大小。
<p>出列帧时，TxMgr 会将小于此值的帧视为具有此值的有效大小。</p></td>
</tr>
<tr class="odd">
<td>UINT16</td>
<td>指定传输功能：帧大小粒度。
<p>此值等于每帧的内存分配粒度。 出于出列的目的，TxMgr 会将一个帧视为有效大小等于帧大小加上最小填充量，以便有效大小为此值的整数倍。 此值必须设置为2的幂。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定传输功能： Rx Tx 转发。
<p>有效值为0和1。 如果设置为1，则目标可以转发接收的帧。</p></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>指定传输功能：最大吞吐量（以 0.5 Mbps 为单位）。
<p>此值用于分配描述符和缓冲区。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




