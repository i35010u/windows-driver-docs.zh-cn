---
title: 用于实现多种无线访问技术的 IHV 指南
description: 本主题提供有关在 Windows 中 (RAT) 和多个操作员实现多个无线电访问技术支持的信息。
ms.assetid: 17BB2478-F98D-4AE6-A62D-F65E2E1DCDFF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b2582e74848aecb83e4143fcb6215ace7778518
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212905"
---
# <a name="ihv-guidance-for-implementing-multimode-and-multicarrier-capable-mb-devices"></a>有关实施多模多载波 MB 设备的 IHV 指导


本主题提供有关在 Windows 中 (RAT) 和多个操作员实现多个无线电访问技术支持的信息。 它补充了 [USB NCM Mobile 宽带接口模型 (MBIM) 1.0 版规范](https://go.microsoft.com/fwlink/p/?linkid=320791) ，其中概述了支持多模式多方案所需的 cid。

本主题中的信息适用于：

-   Windows 8

## <a name="supporting-multimode-devices-with-firmware-switching"></a>支持通过固件切换的多模式设备


本主题向 Ihv 提供有关在 Windows 中实现对多个无线电访问技术 (RAT) 和多个操作员的支持的准则。 下面提供了该规范最相关部分的简短摘要。

多模式网络具有多个 Rat 或手机网络类。 多设备能够支持同一设备内的多个网络提供商。 支持的众多网络之一可以是多模式网络。

在本文档的很多位置，必须将多设备报告的多提供程序设置为 CID 处理的一部分，才能将其设置为 home 提供程序。 本部分介绍如何确定提供程序是否可作为 home 提供程序进行设置。 将提供程序设置为 home 提供程序的功能可能取决于许多因素，这些因素是设备相关的，它们具有提供程序的固件支持，并具有 SIM 或等效于向提供程序注册。 可能有其他因素。 设备应确保满足多提供程序的设备要求，然后再将其报告为可设置的主提供程序

## <a name="1041-cid_mbim_device_caps"></a>10.4.1 CID \_ MBIM \_ 设备 \_ cap


支持的设备将报告 \_ 规范的表10-13 中指定的 bmCellularClass 中的多个受支持的手机网络类 \_ 。 它还将通过 MBIM \_ CTRL + \_ (表 10-13) 中的 MBIMCtrlCapsMultiCarrier 掩码来报告对多个运营商的支持。

单运营商多模式设备的行为必须与 GSM 设备类似。 此类设备不得在其 MBIM \_ 设备 cap 信息中设置任何 CDMA 相关的功能 \_ \_ 。

## <a name="1046-cid_mbim_home_provider"></a>10.4.6 CID \_ MBIM \_ HOME \_ 提供程序


可以按10.3.6.4 中的指定设置 home 提供程序 **。**

## <a name="1048-cid_mbim_visible_providers"></a>10.4.8 CID \_ MBIM \_ 可见 \_ 提供程序


Visible 提供程序 CID 包含一个操作字段，该操作字段指定宿主是否应为：

1.  值0，其中设备在当前主提供程序的上下文中执行完全扫描。
2.  值1：正在查询设备以查找可作为 home 提供程序设置的可见多提供程序。 设备可以选择通过完全扫描、部分扫描或静态列表来实现此目的。 在规范的表10-34 中指定的可见提供程序结果中，应将多首选提供程序标记为 MBIM \_ 提供程序 \_ 状态 \_ 首选 \_ 多。

当设备报告基于位置信息的可见多提供程序的静态列表（使用 CID MBIM 位置信息编程）时 \_ \_ \_ ，该列表应仅包含对该位置有效的提供程序。 作为上述规则的扩展，如果其 MCC (Mobile 国家/地区代码) 的位置与当前在设备中编程的位置不同，则设备不会报告当前注册的提供程序。

## <a name="1049-cid_mbim_register_state"></a>10.4.9 CID \_ MBIM \_ 寄存器 \_ 状态


设备使用 \_ 规范的表10-48 中 "MBIM" 注册状态的 "dwCurrentCellularClass" 字段指示当前蜂窝类类 \_ 。

## <a name="10430-cid_mbim_device_services"></a>10.4.30 CID \_ MBIM \_ 设备 \_ 服务


需要多设备 \_ 在) 设备服务中报告 UUID 多 (来响应此 CID。

单载体多模式设备无需报告 UUID \_ 多设备服务来响应此 CID。

## <a name="10439-cid_mbim_multicarrier_providers"></a>10.4.39 CID \_ MBIM \_ 多 \_ 提供程序


设备使用此 CID 来报告当前和之前添加的首选多提供程序。 当设备支持 MBIMCtrlCapsMultiCarrier 时，支持此 CID。 当主机设置多首选提供程序时，不需要提供程序作为 home 提供程序的设置。 但当主机查询列表时，设备应该只返回可设置为 home 提供程序的多首选提供程序。

下图提供了根据主机指定的位置提示从当前模式切换设备所涉及步骤的序列图。 此操作需要使用下面所述的设备服务从设备获取/设置其他信息。 一个具体的要求是，设备应确保主机有机会在设备离开总线之前从设备恢复挂起的通知。 该关系图还指定了各种操作的时间范围和性能预期。

![基于主机指定的位置提示从当前模式切换设备所涉及的步骤。](images/cid-mbim-multicarrier-providers.png)

## <a name="multi-carrier-device-service"></a>多载波设备服务


当 CID \_ MBIM 设备服务进行查询时，IHV 设备将实现并报告以下设备服务 \_ \_ 。 现有的已知服务在第10.1 节的 NCM MBIM 规范中定义。 它已扩展为定义以下服务。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">服务名称</th>
<th align="left">UUID</th>
<th align="left">UUID 值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>多运营商</p></td>
<td align="left"><p>UUID_MULTICARRIER</p></td>
<td align="left"><p>8b569648-628d-copy to-9b9f-1025404424e1</p></td>
</tr>
</tbody>
</table>

 

具体而言，以下 Cid 是为 UUID \_ 多设备服务定义的。

<table>
<colgroup>
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">CID</th>
<th align="left">命令代码</th>
<th align="left">查询</th>
<th align="left">设置</th>
<th align="left">事件</th>
<th align="left">设置 InformationBuffer 有效负载</th>
<th align="left">查询 InformationBuffer 有效负载</th>
<th align="left">完成 InformationBuffer 有效负载</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>CID_MBIM_MULTICARRIER_CAPABILITIES</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Y</p></td>
<td align="left"><p>N</p></td>
<td align="left"><p>N</p></td>
<td align="left"><p>空值</p></td>
<td align="left"><p>空值</p></td>
<td align="left"><p>MBIM_MULTICARRIER_CAPABILITIES</p></td>
</tr>
<tr class="even">
<td align="left"><p>CID_MBIM_LOCATION_INFO</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Y</p></td>
<td align="left"><p>Y</p></td>
<td align="left"><p>N</p></td>
<td align="left"><p>MBIM_LOCATION_INFO</p></td>
<td align="left"><p>空值</p></td>
<td align="left"><p>MBIM_LOCATION_INFO</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CID_MBIM_MULTICARRIER_CURRENT_CID_LIST</p></td>
<td align="left"><p>3</p></td>
<td align="left"><p>Y</p></td>
<td align="left"><p>N</p></td>
<td align="left"><p>N</p></td>
<td align="left"><p>空值</p></td>
<td align="left"><p>UUID</p></td>
<td align="left"><p>MBIM_MULTICARRIERMODE_CURRENT_CID_LIST</p></td>
</tr>
</tbody>
</table>

 

## <a name="cid_mbim_multicarrier_capabilities"></a>CID \_ MBIM \_ 多 \_ 功能


此命令返回有关 MB 设备的多运营商功能的信息。 需要重新启动固件并相应地进行设备删除/到达的设备应使用适当的标志为主机提供提示，以使主机能够提供适当的用户体验。

查询 = ** \_ 未使用 MBIM 命令消息上的 InformationBuffer \_ 。\_ \_ InformationBuffer MBIM 命令中返回的 MBIM 多功能已 \_ \_ 完成**

Set = **不受支持**

主动事件 = **不受支持**

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">MBIM_MC_FLAGS_NONE</th>
<th align="left">0h</th>
<th align="left">未设置标志</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>MBIM_MC_FLAGS_STATIC_SCAN</p></td>
<td align="left"><p>1小时</p></td>
<td align="left"><p>指示为扫描结果中的可见提供程序报告的结果无法从完全网络扫描获得。 可能会从硬编码列表中获取结果。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MBIM_MC_FLAGS_ FW_REQUIRES_REBOOT</p></td>
<td align="left"><p>下半年</p></td>
<td align="left"><p>指示设备需要通电周期，并重新启动以切换固件。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Offset</th>
<th align="left">大小</th>
<th align="left">字段</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>dwCapabilities</p></td>
<td align="left"><p>返回 MBIM_MULTICARRIER_FLAGS 的功能</p></td>
</tr>
</tbody>
</table>

 

## <a name="cid_mbim_location_info"></a>CID \_ MBIM \_ 位置 \_ 信息


命令用于设置/查询主机的当前位置信息。 如果设备需要筛选静态 (的列表，而不) 可见提供程序与当前用户位置相关的提供程序，则此方法非常有用。

查询 = ** \_ 未使用 MBIM 命令消息上的 InformationBuffer \_ 。已 \_ \_ \_ \_ 完成 InformationBuffer MBIM 命令中返回的 MBIM 位置信息**

Set = **InformationBuffer ON MBIM \_ 命令 \_ MSG 包含 MBIM \_ LOCATION \_ INFO**

主动事件 = **不受支持**

主机指定的国家/地区代码将基于 Windows 上可用的地理位置 GEOID。 有关详细信息，请参阅 [ (Windows) 的地理位置表 ](/windows/desktop/Intl/table-of-geographical-locations)。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Offset</th>
<th align="left">大小</th>
<th align="left">字段</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>国家/地区</p></td>
<td align="left"><p>基于 GEOID 的地理位置。</p></td>
</tr>
</tbody>
</table>

 

## <a name="cid_mbim_multicarrier_current_cid_list"></a>CID \_ MBIM \_ 多 \_ 当前 \_ CID \_ 列表


此命令用于查询设备服务当前所用的 Cid。

Query = **MBIM \_ 命令消息的 InformationBuffer \_ 是设备服务的 UUID。MBIM \_ MULTICARRIERMODE \_ \_ \_ 在 InformationBuffer MBIM 命令中返回的当前 CID 列表已 \_ \_ 完成**

Set = **不受支持**

主动事件 = **不受支持**

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Offset</th>
<th align="left">大小</th>
<th align="left">字段</th>
<th align="left">类型</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>CidCount</p></td>
<td align="left"><p>UINT32</p></td>
<td align="left"><p>此设备服务支持的 Cid 数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p></p></td>
<td align="left"><p>DataBuffer</p></td>
<td align="left"><p>DATABUFFER</p></td>
<td align="left"><p>CidList：此设备服务支持的 Cid 列表。 此列表中的条目数必须为 CID 计数。 每个 CID 都是 UINT32 类型。</p></td>
</tr>
</tbody>
</table>

 

 

