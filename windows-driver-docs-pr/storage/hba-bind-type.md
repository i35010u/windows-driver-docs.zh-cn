---
title: HBA\_绑定\_类型
description: HBA\_绑定\_类型
ms.assetid: a5388574-f48a-4bdc-9ffe-408fa6de1eeb
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 682959a9a7c1832667884ede58694b3611528741
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523545"
---
# <a name="hbabindtype"></a>HBA\_绑定\_类型


## <span id="ddk_hba_bind_type_kr"></span><span id="DDK_HBA_BIND_TYPE_KR"></span>


HBA\_绑定\_类型 WMI 类限定符表示 HBA 的功能和其微型端口驱动程序提供一组特定的永久性绑定与相关的功能。

下表列出了限定符名称和每个名称的含义：

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
<td align="left"><p>指示 HBA 的功能和其微型端口驱动程序接受按地址标识符标识的光纤通道目标端口永久绑定。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_CAN_BIND_TO_WWPN</p></td>
<td align="left"><p>指示 HBA 的功能和其微型端口驱动程序接受通过其全球范围内的端口名称 (WWPN) 标识的光纤通道目标端口永久绑定。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_CAN_BIND_TO_WWNN</p></td>
<td align="left"><p>指示 HBA 的功能和其微型端口驱动程序由其全球范围内的节点名称 (WWNN) 接受标识的光纤通道目标设备 （而不是目标端口） 的永久性绑定。 此方法来确定多端口设备上的设备中的隐式歧义是刻意设计的。 它允许 HBA 和/或在构造为供应商特定的方式解析多义性。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_CAN_BIND_TO_LUID</p></td>
<td align="left"><p>指示 HBA 的功能和其微型端口驱动程序接受标识的逻辑单元派生自 SCSI 查询数据的标识描述符的光纤通道逻辑单元的持久绑定。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_CAN_BIND_ANY_LUNS</p></td>
<td align="left"><p>指示 HBA 的功能和其微型端口驱动程序接受指定的操作系统和光纤通道逻辑单元号的永久绑定设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_CAN_BIND_TARGETS</p></td>
<td align="left"><p>指示 HBA 的功能和其微型端口驱动程序来生成逻辑单元的光纤通道协议 (FCP) 标识符用于标识逻辑单元，如的总线和目标操作系统的信息之间的永久绑定中存储的数字<a href="https://msdn.microsoft.com/library/windows/hardware/ff556042" data-raw-source="[&lt;strong&gt;HBAScsiID&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556042)"> <strong>HBAScsiID</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBA_CAN_BIND_AUTOMAP</p></td>
<td align="left"><p>指示 HBA 的功能和其微型端口驱动程序以自动生成目标映射和持久性绑定所有已发现的存储资源。 如果此功能未指定，或者已禁用，则允许的唯一绑定是指那些在操作系统中显式配置。 绑定的显式配置可加快逻辑单元号 (LUN) 的屏蔽。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HBA_CAN_BIND_CONFIGURED</p></td>
<td align="left"><p>指示 HBA 的功能和其微型端口驱动程序接受永久绑定的动态配置。</p></td>
</tr>
</tbody>
</table>

 

通过包括*Hbaapi.h*您的软件有权访问一系列的对应于上表中的类型名称的符号常量。 这些符号常量的定义中不包括*Hbapiwmi.h* （WMI 工具套件时对其进行编译，生成的文件）。

 

 





