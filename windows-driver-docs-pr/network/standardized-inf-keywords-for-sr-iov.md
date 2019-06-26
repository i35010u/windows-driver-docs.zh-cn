---
title: SR-IOV 的标准化 INF 关键字
description: SR-IOV 的标准化 INF 关键字
ms.assetid: 5CA33B4F-E43A-4EB6-BCAB-365CA1FD3EF2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0303e33adecd3531c462474bd891a1f7885651b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378620"
---
# <a name="standardized-inf-keywords-for-sr-iov"></a>SR-IOV 的标准化 INF 关键字


本主题介绍的单个根 I/O 虚拟化 (SR-IOV) 接口的标准化的 INF 关键字。 这些关键字不适用于微型端口驱动程序的 PCI Express (PCIe) 物理函数 (PF) 的 SR-IOV 网络适配器的 INF 文件。

以下各节所述的 SR-IOV INF 关键字：

[启用或禁用 SR-IOV 支持的标准化的 INF 关键字](#standardized-inf-keywords-for-enabling-or-disabling-sr-iov-support)

[默认 NIC 交换机的配置的标准化的 INF 关键字](#standardized-inf-keywords-for-configuration-of-the-default-nic-switch)

## <a name="standardized-inf-keywords-for-enabling-or-disabling-sr-iov-support"></a>启用或禁用 SR-IOV 支持的标准化的 INF 关键字


标准化的 INF 关键字定义来启用或禁用网络适配器的 SR-IOV 功能的支持。

<a href="" id="-sriov"></a> **\*SRIOV**  
一个描述该设备是否已启用或禁用 SR-IOV 功能的值。

安装该驱动程序后，管理员可以更新 **\*SRIOV**中的关键字值**高级**网络适配器的属性页。 有关高级属性的详细信息，请参阅[的高级属性页指定配置参数](specifying-configuration-parameters-for-the-advanced-properties-page.md)。

**请注意**   中进行更改后的微型端口驱动程序将自动重启**高级**适配器属性页。

 

<a href="" id="-sriovpreferred"></a> **\*SriovPreferred**  
一个值，定义 SR-IOV 功能而不是虚拟机队列 (VMQ)，应启用还是接收方缩放 (RSS) 功能。

这是一个隐藏的关键字值不得指定 INF 文件中并不会显示在**高级**网络适配器的属性页。

有关如何解释 SR-IOV、 VMQ 和 RSS 关键字的详细信息，请参阅[处理 SR-IOV、 VMQ 和 RSS 标准化 INF 关键字](handling-sr-iov--vmq--and-rss-standardized-inf-keywords.md)。

SR-IOV 标准化的 INF 关键字是枚举的关键字和以下表所述。 此表中的列描述枚举关键字的以下属性：

<a href="" id="subkeyname"></a>SubkeyName  
必须在 INF 文件中指定的关键字的名称。 此名称也会出现在注册表 **NDI\\params\\** 关键网络适配器。

<a href="" id="paramdesc"></a>ParamDesc  
与之关联的显示文本**SubkeyName**关键字。

**请注意**   独立硬件供应商 (IHV) 可以为 SubkeyName 定义描述性文本。

 

<a href="" id="value"></a>值  
与每个关联的枚举的整数值**SubkeyName**列表中的关键字。

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
<th align="left">值</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>SRIOV</strong></p></td>
<td align="left"><p>SR-IOV</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>Enabled</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>SriovPreferred</strong></p></td>
<td align="left"><p>此子项的 ParamDesc 和 EnumDesc 项不能使用 INF 文件或用户界面中。</p></td>
<td align="left"><p>0 （默认值）</p></td>
<td align="left"><p>报表基于的 RSS 或 VMQ 功能<strong> <em>VmqOrRssPreferrence</strong>关键字。 不报告 SR-IOV 功能</p>
<p>有关详细信息 <strong></em>VmqOrRssPreferrence</strong>关键字，请参阅<a href="standardized-inf-keywords-for-vmq.md" data-raw-source="[Standardized INF Keywords for VMQ](standardized-inf-keywords-for-vmq.md)">VMQ 的标准化 INF 关键字</a>。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>报表的 SR-IOV 功能。</p></td>
</tr>
</tbody>
</table>

 

有关标准化 INF 关键字的详细信息，请参阅[为网络设备的标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)。

## <a name="standardized-inf-keywords-for-configuration-of-the-default-nic-switch"></a>默认 NIC 交换机的配置的标准化的 INF 关键字


从 Windows Server 2012 开始，SR-IOV 接口只支持一个 NIC 切换上的网络适配器。 此交换机被称为*默认 NIC 开关*，并引用的 NDIS\_默认\_切换\_ID 标识符。

PF 微型端口驱动程序的 INF 文件必须指定 NIC 切换的默认配置的 SR-IOV 网络适配器上。 这样，要将从 INF 的默认交换机配置信息复制到默认开关子项下的微型端口注册表配置的网络安装程序 (**NDI\\params\\NicSwitches\\0**)。

这些关键字不会显示在**高级**属性页上为网络适配器，不能由用户配置。 通过使用指定这些关键字**AddReg**指令**DDInstall** INF 文件部分。 通过单独指定每个关键字**AddReg**指令。

下表描述默认 NIC 开关配置的 SR-IOV 网络适配器的 INF 关键字。 此表中的列描述这些关键字的以下属性：

<a href="" id="subkeyname"></a>SubkeyName  
必须在 INF 文件中指定的关键字的名称。 此名称也会出现在注册表**NDI\\params\\NicSwitches\\0**关键网络适配器。

<a href="" id="data-value"></a>数据值  
与之关联的值**SubkeyName**关键字。

<a href="" id="data-type"></a>数据类型  
数据值的类型。

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
<th align="left">数据值</th>
<th align="left">数据类型</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>标志</strong></p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>关键字必须分配此值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em>SwitchType</strong></p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>关键字必须分配此值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>SwitchId</strong></p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>关键字必须分配此值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em>SwitchName</strong></p></td>
<td align="left"><p>"默认的交换机"</p></td>
<td align="left"><p>REG_SZ</p></td>
<td align="left"><p>关键字必须分配此值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*NumVFs</strong></p></td>
<td align="left"><p>(0-<em>n</em>)，</p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p><em>n</em>是 PCIe 虚函数 (VFs) 的 SR-IOV 网络适配器所支持的最大数目。</p>
<div class="alert">
<strong>请注意</strong>此注册表项定义的网络适配器支持的 VFs 的最大数目。 当微型端口驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes" data-raw-source="[&lt;strong&gt;NdisMSetMiniportAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)"> <strong>NdisMSetMiniportAttributes</strong></a>，它可以播发小于此值具体取决于网络适配器上的可用硬件资源。 有关详细信息，请参阅<a href="determining-nic-switch-capabilities.md" data-raw-source="[Determining NIC Switch Capabilities](determining-nic-switch-capabilities.md)">确定 NIC 交换机功能</a>。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

以下是一种**AddReg** SR-IOV 网络适配器的默认 NIC 交换机配置指令：

``` syntax
HKR, NicSwitches\0, *SwitchId,   0x00010001, 0
HKR, NicSwitches\0, *SwitchName, 0x00000000, “Default Switch”
```

有关语法的详细信息**AddReg**指令，请参阅[ **INF AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)。

有关默认 NIC 开关的详细信息，请参阅[NIC 开关](nic-switches.md)。

 

 





