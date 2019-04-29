---
title: NDIS QoS 的标准化 INF 关键字
description: NDIS QoS 的标准化 INF 关键字
ms.assetid: 7967D633-850F-4707-9577-9262AEB1A597
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 236ea7fa353a460c774fc4786b96903d84289291
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345979"
---
# <a name="standardized-inf-keywords-for-ndis-qos"></a>NDIS QoS 的标准化 INF 关键字


标准化的 INF 关键字定义来启用或禁用微型端口驱动程序上对 NDIS 服务质量 (QoS) 的支持。

支持 NDIS QoS 的适配器的微型端口驱动程序的 INF 文件必须指定 **\*QOS**标准化 INF 关键字。 安装该驱动程序后，管理员可以更新 **\*QOS**中的关键字值**高级**适配器属性页。 有关高级属性的详细信息，请参阅[的高级属性页指定配置参数](specifying-configuration-parameters-for-the-advanced-properties-page.md)。

**请注意**  中进行更改后的微型端口驱动程序将自动重启**高级**适配器属性页。

 

 **\*QOS** INF 关键字是一个枚举的关键字。 下表描述了可能 INF 条目 **\*QOS** INF 关键字。 此表中的列描述枚举关键字的以下属性：

<a href="" id="subkeyname"></a>SubkeyName  
必须在 INF 文件中指定的关键字的名称。 此名称也会出现在注册表**NDI\\params\\** 关键网络适配器。

<a href="" id="paramdesc"></a>ParamDesc  
显示文本与 SubkeyName 相关联。

**请注意**  独立硬件供应商 (IHV) 可以为 SubkeyName 定义描述性文本。

 

<a href="" id="value"></a>值  
枚举的整数值与列表中每个 SubkeyName 相关联。

<a href="" id="enumdesc"></a>EnumDesc  
与每个菜单中显示的值相关联的显示文本。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">ReplTest1</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>*QOS</strong></p></td>
<td align="left"><p>NDIS QoS</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>QoS 已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>启用了 QoS</p></td>
</tr>
</tbody>
</table>

 

当 NDIS 调用微型端口驱动程序[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数，该驱动程序必须执行以下操作：

-   微型端口驱动程序必须注册的网络适配器支持的 NDIS QoS 硬件功能。

-   微型端口驱动程序还必须读取 **\*QOS**注册表注册适配器的 NDIS QoS 硬件功能的当前状态中的关键字值。

当它注册的 NDIS QoS 硬件功能的当前状态时，微型端口驱动程序必须遵循以下准则：

-   如果 **\*QOS**关键字的一个值，则微型端口驱动程序必须注册为当前已启用的所有 NDIS QoS 硬件功能。 该驱动程序必须启用而不考虑以下其 NDIS QoS 硬件功能：

    -   是否安装或 Windows Server 2012 和更高版本的 Windows Server 上启用 Microsoft 数据中心桥接 (DCB) 服务器功能。 有关此服务器功能和相关的组件的详细信息，请参阅[NDIS QoS 体系结构的数据中心桥接](ndis-qos-architecture-for-data-center-bridging.md)。

    -   是否已在网络适配器上启用本地数据中心桥接交换 (DCBX) 愿意状态。 启用此状态时，网络适配器和微型端口驱动程序可以解决其操作的 NDIS QoS 参数从远程对等方接收到的远程 NDIS QoS 参数。 有关详细信息，请参阅[管理本地 DCBX 愿意状态](managing-the-local-dcbx-willing-state.md)。

    有关如何注册 QoS 硬件和当前功能的详细信息，请参阅[注册的 NDIS QoS 功能](registering-ndis-qos-capabilities.md)。

    **请注意**  微型端口驱动程序必须始终发出[ **NDIS\_状态\_QOS\_操作\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439810)并[ **NDIS\_状态\_QOS\_远程\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状态如果其 NDIS QoS 硬件功能当前已启用的指示。 分别从 Windows Server 2012 上的当前操作和远程 QoS 参数设置，这些状态指示报表。 这些指示允许系统管理员查看 NDIS QoS 和 DCB 设置而不考虑是否安装了 Microsoft DCB 服务器功能。 有关详细信息，请参阅[，该值指示 NDIS QoS 参数状态](indicating-ndis-qos-parameter-status.md)。

     

-   如果 **\*QOS**关键字的值为零、 微型端口驱动程序必须报告为当前已禁用所有 NDIS QoS 硬件功能。 在这种情况下，操作系统将不配置驱动程序与的 NDIS QoS 功能。

    **请注意**  驱动程序必须禁用 DCB 和 DCBX 网络适配器上如果 **\*QOS**关键字的值为零。

     

-   如果 **\*QOS**关键字不是在注册表中存在，微型端口驱动程序必须报告任何 NDIS QoS 硬件功能。 在这种情况下，操作系统将不配置驱动程序与的 NDIS QoS 功能。

    **请注意**  驱动程序必须禁用 DCB 和 DCBX 网络适配器上如果 **\*QOS**关键字不在注册表中存在。

     

除了 **\*QOS**关键字，微型端口驱动程序必须读取 **\*PriorityVLANTag**关键字。 此关键字指定是否启用网络适配器以插入 802.1Q 标记数据包优先级和虚拟 Lan (Vlan)。

下表总结了之间的关系 **\*QOS**并 **\*PriorityVLANTag**关键字值。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>QOS 关键字设置</th>
<th align="left"></em>PriorityVLANTag 关键字设置</th>
<th align="left">* PriorityVLANTag 设置说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">0 或不存在</td>
<td align="left"><p>0</p></td>
<td align="left"><p>数据包优先级&amp;禁用 VLAN</p></td>
</tr>
<tr class="even">
<td align="left">0 或不存在</td>
<td align="left"><p>1</p></td>
<td align="left"><p>启用数据包优先级</p></td>
</tr>
<tr class="odd">
<td align="left">0 或不存在</td>
<td align="left"><p>2</p></td>
<td align="left"><p>已启用 VLAN</p></td>
</tr>
<tr class="even">
<td align="left">0 或不存在</td>
<td align="left"><p>3 （默认值）</p></td>
<td align="left"><p>数据包优先级和已启用 VLAN</p></td>
</tr>
<tr class="odd">
<td align="left">1</td>
<td align="left"><p>0</p></td>
<td align="left"><p>启用数据包优先级</p></td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left"><p>1</p></td>
<td align="left"><p>启用数据包优先级</p></td>
</tr>
<tr class="odd">
<td align="left">1</td>
<td align="left"><p>2</p></td>
<td align="left"><p>数据包优先级和已启用 VLAN</p></td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left"><p>3 （默认值）</p></td>
<td align="left"><p>数据包优先级和已启用 VLAN</p></td>
</tr>
</tbody>
</table>

 

有关详细信息 **\*PriorityVLANTag**关键字，请参阅[枚举关键字](enumeration-keywords.md)。

有关标准化 INF 关键字的详细信息，请参阅[为网络设备的标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)。

有关如何注册的 NDIS QoS 功能的详细信息，请参阅[注册的 NDIS QoS 功能](registering-ndis-qos-capabilities.md)。

 

 





