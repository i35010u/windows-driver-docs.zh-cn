---
title: 实现多个无线访问技术的 IHV 指导
description: 本主题提供有关在 Windows 中实现对多个无线接入技术 (RAT) 和多个运算符的支持信息。
ms.assetid: 17BB2478-F98D-4AE6-A62D-F65E2E1DCDFF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a53128bdde33dc24ccefd68f9fa611fc891680b7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568052"
---
# <a name="ihv-guidance-for-implementing-multimode-and-multicarrier-capable-mb-devices"></a>有关实施多模多载波 MB 设备的 IHV 指导


本主题提供有关在 Windows 中实现对多个无线接入技术 (RAT) 和多个运算符的支持信息。 它可以补充[USB NCM 移动宽带接口模型 (MBIM) V1.0 规范](https://go.microsoft.com/fwlink/p/?linkid=320791)，概述了用于支持多模式的运营商情形所需的 Cid。

本主题中的信息适用于：

-   Windows 8

## <a name="supporting-multimode-devices-with-firmware-switching"></a>支持多模式设备用固件切换


本主题提供有关在 Windows 中实现对多个无线接入技术 (RAT) 和多个运算符的支持 Ihv 指导。 下面提供了在规范的相关度最高部分的简短摘要。

可以将多模式网络具有多个来自于老鼠或移动电话的类。 运营商的设备都能以支持在同一设备中的多个网络提供程序。 其中一个支持多个网络可以是多模式网络。

在本文档中的多个位置是必需的运营商设备报告运营商的提供程序为的 CID 处理部分必须在组可以作为主提供程序。 本部分介绍如何确定是否可为家庭的提供程序设置提供程序。 为家庭的提供程序设置提供程序的功能可能取决于许多因素会与设备相关如不可见，拥有固件支持提供程序，并让 SIM 或同等身份才能注册提供程序。 可能有其他因素。 设备应确保报告为可设置家庭提供程序之前满足运营商的提供程序的设备要求

## <a name="1041-cidmbimdevicecaps"></a>10.4.1 CID\_MBIM\_DEVICE\_CAPS


支持的设备将报告多个受支持移动电话网络中的类 bmCellularClass MBIM\_设备\_CAPS 作为中的指定表 10 月 13 日的规范。 它还会报告对通过 MBIM MBIMCtrlCapsMultiCarrier 掩码的多个运营商的支持\_CTRL\_CAP （表 10 月 13 日）。

单运营商多模式设备必须类似 GSM 的设备。 此类设备必须未设置任何 CDMA 相关的功能在其 MBIM\_设备\_CAPS\_信息。

## <a name="1046-cidmbimhomeprovider"></a>10.4.6 CID\_MBIM\_主页\_提供程序


可以设置家庭的提供程序中指定的那样**10.3.6.4。**

## <a name="1048-cidmbimvisibleproviders"></a>10.4.8 CID\_MBIM\_VISIBLE\_提供程序


可见的提供程序 CID 包含指定是否应为主机的操作字段：

1.  值 0，其中设备会在当前主提供程序的上下文中执行完全扫描。
2.  值 1，其中设备正被查询来查找可为家庭的提供程序设置可见的运营商提供程序。 设备可以选择实现此目的通过完全扫描、 部分进行扫描或静态列表。 多首选提供程序应标记为 MBIM\_提供程序\_状态\_首选\_中可见的提供程序结果中指定为表 10 34 规范的多。

当设备将报告可见运营商的提供程序基于位置的信息的静态列表时，通过编程使用 CID\_MBIM\_位置\_信息，该列表应只包含提供程序对该位置有效。 作为上述规则的扩展，设备不应报告当前已注册的提供程序，则表示其 MCC （移动国家/地区代码） 的位置不同于当前编程设备中的位置时。

## <a name="1049-cidmbimregisterstate"></a>10.4.9 CID\_MBIM\_注册\_状态


设备将指示当前的移动电话类使用 MBIM dwCurrentCellularClass 字段\_注册\_规范的状态表 10-48。

## <a name="10430-cidmbimdeviceservices"></a>10.4.30 CID\_MBIM\_DEVICE\_SERVICES


运营商的设备所需报告 UUID\_（如下所述） 的多设备服务在响应针对此 CID。

单运营商可以将多模式设备都不需要报表 UUID\_运营商的设备服务在响应针对此 CID。

## <a name="10439-cidmbimmulticarrierproviders"></a>10.4.39 CID\_MBIM\_多\_提供程序


设备使用此 CID 来报告当前和以前添加的首选运营商的提供程序。 当设备支持 MBIMCtrlCapsMultiCarrier，才支持此 CID。 当主机设置运营商的首选提供程序时，它不是所需的提供程序是可为家庭的提供程序设置。 但列表是由主机查询后，设备应仅返回运营商可作为主提供程序设置的首选提供程序。

下图提供了在切换设备从其当前模式，基于 host 所指定的位置提示所涉及的步骤的序列图。 操作需要使用设备服务来获取或设置从设备的其他信息如下所述。 一个特定的要求是，设备应确保主机有机会从之前写入一样在总线设备恢复挂起的通知。 在关系图还指定的时间限制和各种操作的性能预期。

![在切换设备从其当前模式，基于 host 所指定的位置提示所涉及的步骤。](images/cid-mbim-multicarrier-providers.png)

## <a name="multi-carrier-device-service"></a>多运营商设备服务


IHV 设备会实现并报告以下设备服务 CID 进行查询时\_MBIM\_设备\_服务。 在部分 10.1 NCM MBIM 规范中定义现有的已知服务。 它被扩展它来定义以下服务。

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
<td align="left"><p>8b569648- 628d-4653-9b9f- 1025404424e1</p></td>
</tr>
</tbody>
</table>

 

具体而言，以下 Cid 定义的 UUID\_运营商的设备服务。

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
<th align="left">Event</th>
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
<td align="left"><p>不可用</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>MBIM_MULTICARRIER_CAPABILITIES</p></td>
</tr>
<tr class="even">
<td align="left"><p>CID_MBIM_LOCATION_INFO</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Y</p></td>
<td align="left"><p>Y</p></td>
<td align="left"><p>N</p></td>
<td align="left"><p>MBIM_LOCATION_INFO</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>MBIM_LOCATION_INFO</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CID_MBIM_MULTICARRIER_CURRENT_CID_LIST</p></td>
<td align="left"><p>3</p></td>
<td align="left"><p>Y</p></td>
<td align="left"><p>N</p></td>
<td align="left"><p>N</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>UUID</p></td>
<td align="left"><p>MBIM_MULTICARRIERMODE_CURRENT_CID_LIST</p></td>
</tr>
</tbody>
</table>

 

## <a name="cidmbimmulticarriercapabilities"></a>CID\_MBIM\_多\_功能


该命令返回信息 MB 设备的多运营商功能。 要求固件重新启动，并相应地设备删除/到达设备应将主机提供使用适当的标志来使宿主能够提供适当的用户体验的提示。

查询 = **InformationBuffer 上 MBIM\_命令\_未使用的消息。MBIM\_多\_InformationBuffer MBIM 中返回的功能\_命令\_完成**

设置 =**不受支持**

未经请求的事件 =**不受支持**

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
<th align="left">设置任何标志</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>MBIM_MC_FLAGS_STATIC_SCAN</p></td>
<td align="left"><p>1h</p></td>
<td align="left"><p>指示为可见的提供程序在扫描结果中报告的结果不会获得完全的网络扫描中。 结果可能来自一个硬编码列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MBIM_MC_FLAGS_¬¬FW_REQUIRES_REBOOT</p></td>
<td align="left"><p>2h</p></td>
<td align="left"><p>指示设备需要支持周期和重启切换固件。</p></td>
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
<th align="left">偏移量</th>
<th align="left">大小</th>
<th align="left">字段</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>dwCapabilities</p></td>
<td align="left"><p>返回从 MBIM_MULTICARRIER_FLAGS 功能</p></td>
</tr>
</tbody>
</table>

 

## <a name="cidmbimlocationinfo"></a>CID\_MBIM\_位置\_信息


使用命令来设置/查询当前的位置信息的主机。 如果需要静态 （没有物理扫描） 到与当前用户位置相关的可见提供程序列表进行筛选，这是适用于设备。

查询 = **InformationBuffer 上 MBIM\_命令\_未使用的消息。MBIM\_位置\_InformationBuffer MBIM 中返回的信息\_命令\_完成**

设置 = **InformationBuffer 上 MBIM\_命令\_MSG 包含 MBIM\_位置\_信息**

未经请求的事件 =**不受支持**

Host 所指定的国家/地区代码将基于地理位置 GEOID 可用在 Windows 上。 有关详细信息，请参阅[表的地理位置 (Windows)](https://msdn.microsoft.com/library/windows/desktop/dd374073)。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">偏移量</th>
<th align="left">大小</th>
<th align="left">字段</th>
<th align="left">描述</th>
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

 

## <a name="cidmbimmulticarriercurrentcidlist"></a>CID\_MBIM\_多\_当前\_CID\_列表


此命令用于查询当前应通过设备服务的 Cid。

查询 = **InformationBuffer 上 MBIM\_命令\_MSG 是设备服务 UUID。MBIM\_MULTICARRIERMODE\_当前\_CID\_InformationBuffer MBIM 中返回列表\_命令\_完成**

设置 =**不受支持**

未经请求的事件 =**不受支持**

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
<th align="left">偏移量</th>
<th align="left">大小</th>
<th align="left">字段</th>
<th align="left">在任务栏的搜索框中键入</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>CidCount</p></td>
<td align="left"><p>UINT32</p></td>
<td align="left"><p>此设备的服务支持的 Cid 的数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p></p></td>
<td align="left"><p>DataBuffer</p></td>
<td align="left"><p>DATABUFFER</p></td>
<td align="left"><p>CidList:此设备的服务支持的 Cid 的列表。 必须在此列表中的条目的 CID 计数数。 每个 CID 是 UINT32 类型。</p></td>
</tr>
</tbody>
</table>

 

 

 





