---
title: 适用于 Windows 10 的 GNSS 驱动程序设计指南
description: 介绍用于在 Windows 10 中聚合的 Windows 位置堆栈 GNSS (UMDF 2.0) 设计要求和通用 Windows 驱动程序的体系结构。
ms.assetid: FD8503DC-A43F-43B2-A1E9-D80778E326F9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9f1bcc473217f096d655dadd3be7ba9d80f6e7e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371125"
---
# <a name="gnss-driver-design-guide-for-windows-10"></a>适用于 Windows 10 的 GNSS 驱动程序设计指南


本指南介绍了设计和通用 Windows 驱动程序的体系结构为 GNSS (UMDF 2.0) 的 Windows 10 中的聚合 Windows 位置堆栈。

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
<td><p><a href="gnss-driver-overview.md" data-raw-source="[GNSS driver overview](gnss-driver-overview.md)">GNSS 驱动程序概述</a></p></td>
<td><p>使用 GNSS 驱动程序设计指南，了解如何实现<strong>DeviceIoControl</strong> GNSS 驱动程序的 Api，以便像 GNSS 适配器的高级别的操作系统组件 (HLOS) 可以访问所需的 GNSS 功能。</p></td>
</tr>
<tr class="even">
<td><p><a href="gnss-driver-requirements.md" data-raw-source="[GNSS driver requirements](gnss-driver-requirements.md)">GNSS 驱动程序要求</a></p></td>
<td><p>介绍适用于 Windows 10 开发 GNSS 驱动程序时要考虑的要求，假设和约束。</p></td>
</tr>
<tr class="odd">
<td><p><a href="gnss-driver-architecture.md" data-raw-source="[GNSS driver architecture](gnss-driver-architecture.md)">GNSS 驱动程序体系结构</a></p></td>
<td><p>概述了 GNSS UMDF 2.0 驱动程序体系结构，I/O 注意事项，并讨论了几种类型的跟踪和修补程序的会话。</p></td>
</tr>
<tr class="even">
<td><p><a href="gnss-driver-design.md" data-raw-source="[GNSS driver design](gnss-driver-design.md)">GNSS 驱动程序设计</a></p></td>
<td><p>讨论开发包括数据结构、 错误报告和驱动程序版本控制的 Windows 10 GNSS 驱动程序时要考虑的设计原则。</p></td>
</tr>
</tbody>
</table>

 

 

 




