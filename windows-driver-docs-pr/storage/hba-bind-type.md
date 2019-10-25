---
title: HBA\_绑定\_类型
description: HBA\_绑定\_类型
ms.assetid: a5388574-f48a-4bdc-9ffe-408fa6de1eeb
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c41cf021eecbf8b236150fc9844f954341022425
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837999"
---
# <a name="hba_bind_type"></a>HBA\_绑定\_类型


## <span id="ddk_hba_bind_type_kr"></span><span id="DDK_HBA_BIND_TYPE_KR"></span>


HBA\_绑定\_类型的 WMI 类限定符指示 HBA 及其小型端口驱动程序提供与永久性绑定相关的一组特定功能的能力。

下表列出了每个名称的限定符名称和含义：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">类型</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>HBA_CAN_BIND_TO_D_ID</p></td>
<td align="left"><p>指示 HBA 及其小型端口驱动程序接受永久性绑定的功能，该永久性绑定通过其地址标识符来标识光纤通道目标端口。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_CAN_BIND_TO_WWPN</p></td>
<td align="left"><p>指示 HBA 及其小型端口驱动程序接受通过其全球端口名称（WWPN）识别光纤通道目标端口的永久性绑定的能力。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_CAN_BIND_TO_WWNN</p></td>
<td align="left"><p>指示 HBA 及其小型端口驱动程序接受通过其全球节点名称（WWNN）识别光纤通道目标设备（而非目标端口）的永久绑定的能力。 在这种情况下，识别多端口设备上的设备是隐含的歧义。 它允许 HBA 和/或构造以特定于供应商的方式解决歧义。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_CAN_BIND_TO_LUID</p></td>
<td align="left"><p>指示 HBA 及其小型端口驱动程序接受永久性绑定的功能，该永久性绑定通过派生自逻辑单元的 SCSI 查询数据的标识描述符来识别光纤通道逻辑单元。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_CAN_BIND_ANY_LUNS</p></td>
<td align="left"><p>指示 HBA 及其微型端口驱动程序接受同时指定操作系统和光纤通道逻辑单元号的永久性绑定设置的能力。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_CAN_BIND_TARGETS</p></td>
<td align="left"><p>指示 HBA 及其小型端口驱动程序在逻辑单元的光纤通道协议（FCP）标识符之间生成永久性绑定的能力，以及操作系统用于标识逻辑单元（如总线和目标）的信息存储在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbascsiid" data-raw-source="[&lt;strong&gt;HBAScsiID&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbascsiid)"><strong>HBAScsiID</strong></a>中的数字。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_CAN_BIND_AUTOMAP</p></td>
<td align="left"><p>指示 HBA 及其小型端口驱动程序为所有发现的存储资源自动生成目标映射和持久绑定的能力。 如果未指明此功能或此功能已禁用，则只允许在操作系统中显式配置的绑定。 绑定的显式配置有助于逻辑单元号（LUN）掩码。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_CAN_BIND_CONFIGURED</p></td>
<td align="left"><p>指示 HBA 及其小型端口驱动程序接受永久性绑定的动态配置的功能。</p></td>
</tr>
</tbody>
</table>

 

通过包含*Hbaapi* ，你的软件将有权访问与上表中的类型名称对应的一系列符号常量。 这些符号常量的定义不包括在*Hbapiwmi*中（WMI 工具套件编译时生成的文件）。

 

 





