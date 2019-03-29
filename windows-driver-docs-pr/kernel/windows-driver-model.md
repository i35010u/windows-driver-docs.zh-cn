---
title: Windows 驱动程序模型 (WDM)
description: 本部分介绍 Windows 驱动程序模型 (WDM)，并讨论了 WDM 驱动程序、 设备配置、 驱动程序分层和 WDM 版本控制的类型。
ms.assetid: 9e76c5a8-a19a-44cf-867a-b2246ea8eaf1
keywords:
- 内核模式驱动程序 WDK、 WDM 驱动程序
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8374c462e319a70ca92430cec01a41b310020238
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350002"
---
# <a name="windows-driver-model-wdm"></a>Windows 驱动程序模型 (WDM)


本部分介绍*Windows 驱动程序模型*(WDM)，并讨论了 WDM 驱动程序、 设备配置、 驱动程序分层和 WDM 版本控制的类型。 WDM 简化了编写在多个版本的 Windows 操作系统上运行的内核模式驱动程序的设计。




## <a name="in-this-section"></a>本节内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="introduction-to-wdm.md" data-raw-source="[Introduction to WDM](introduction-to-wdm.md)">WDM 简介</a></p></td>
<td><p>若要使驱动程序开发人员编写设备驱动程序，将源代码兼容跨所有 Microsoft Windows 操作系统中， <em>Windows 驱动程序模型</em>(WDM) 引入。 遵循 WDM 规则的内核模式驱动程序被称为<em>WDM 驱动程序</em>。</p></td>
</tr>
<tr class="even">
<td><p><a href="types-of-wdm-drivers.md" data-raw-source="[Types of WDM Drivers](types-of-wdm-drivers.md)">WDM 驱动程序的类型</a></p></td>
<td><p>有三种类型的 WDM 驱动程序： 总线驱动程序、 函数驱动程序和筛选器驱动程序。</p></td>
</tr>
<tr class="odd">
<td><p><a href="device-configurations-and-layered-drivers.md" data-raw-source="[Device Configurations and Layered Drivers](device-configurations-and-layered-drivers.md)">设备配置和分层驱动程序</a></p></td>
<td><p>对于最常见类型的设备，Windows Driver Kit (WDK) 提供了完全正常运行的系统驱动程序的一组示例。 各个示例驱动程序可以用作模型，开发新的驱动程序的相似类型的设备时。 但是，系统的驱动程序有一个额外的设计要求： 若要轻松地开发新的设备驱动程序。 因此，有许多系统的驱动程序的分层式体系结构，以便可以重复使用某些驱动程序以支持新的驱动程序的类似的设备。</p></td>
</tr>
<tr class="even">
<td><p><a href="wdm-versions.md" data-raw-source="[WDM Versions](wdm-versions.md)">WDM 版本</a></p></td>
<td><p>更高版本的 WDM 通常支持所有的 WDM; 早期版本中提供的功能也就是说，WDM 每个新版本是以前的 WDM 版本的超集。 如果可能，应为在任何操作系统上的最低 WDM 版本符合跨系统驱动程序。</p></td>
</tr>
</tbody>
</table>

 

 

 




