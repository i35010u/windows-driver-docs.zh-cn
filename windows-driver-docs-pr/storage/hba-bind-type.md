---
title: HBA \_ 绑定 \_ 类型
description: HBA \_ 绑定 \_ 类型
ms.assetid: a5388574-f48a-4bdc-9ffe-408fa6de1eeb
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 931dffb42e704db774708c4e48948e4e599fb410
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189043"
---
# <a name="hba_bind_type"></a>HBA \_ 绑定 \_ 类型


## <span id="ddk_hba_bind_type_kr"></span><span id="DDK_HBA_BIND_TYPE_KR"></span>


HBA \_ 绑定 \_ 类型 WMI 类限定符指示 hba 及其小型端口驱动程序提供与永久性绑定相关的一组特定功能的能力。

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
<td align="left"><p>指示 HBA 及其小型端口驱动程序接受永久性绑定的功能，该永久性绑定通过其全球端口名称 (WWPN) 来识别光纤通道目标端口。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_CAN_BIND_TO_WWNN</p></td>
<td align="left"><p>指示 HBA 及其小型端口驱动程序接受永久性绑定的功能，该绑定将标识光纤通道目标设备，而不 (其全球节点名称 (WWNN) 中) 目标端口。 在这种情况下，识别多端口设备上的设备是隐含的歧义。 它允许 HBA 和/或构造以特定于供应商的方式解决歧义。</p></td>
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
<td align="left"><p>指示 HBA 及其小型端口驱动程序在光纤通道协议 () FCP 之间生成永久性绑定的功能，以及操作系统用于标识逻辑单元的信息，例如存储在 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbascsiid" data-raw-source="[&lt;strong&gt;HBAScsiID&lt;/strong&gt;](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbascsiid)"><strong>HBAScsiID</strong></a>中的总线和目标编号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_CAN_BIND_AUTOMAP</p></td>
<td align="left"><p>指示 HBA 及其小型端口驱动程序为所有发现的存储资源自动生成目标映射和持久绑定的能力。 如果未指明此功能或此功能已禁用，则只允许在操作系统中显式配置的绑定。 绑定的显式配置有助于逻辑单元号 (LUN) 掩码。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_CAN_BIND_CONFIGURED</p></td>
<td align="left"><p>指示 HBA 及其小型端口驱动程序接受永久性绑定的动态配置的功能。</p></td>
</tr>
</tbody>
</table>

 

通过包含 *Hbaapi* ，你的软件将有权访问与上表中的类型名称对应的一系列符号常量。 这些符号常量的定义不包含在 *Hbapiwmi* 中， (WMI 工具套件编译) 时生成的文件。

 

