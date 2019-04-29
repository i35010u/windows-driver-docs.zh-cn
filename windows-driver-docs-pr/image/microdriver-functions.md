---
title: 微驱动程序函数
description: 微驱动程序函数
ms.assetid: 491b954a-8ffa-4899-8c7d-0aee409f4742
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ee0dc57d1b5eaa075e3218c90d22306aea426ef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379678"
---
# <a name="microdriver-functions"></a>微驱动程序函数





WIA 平板驱动程序从 WIA 服务响应请求通过调用 WIA microdriver 函数。 这些函数必须由每个供应商提供 microdriver 实现，并包括以下：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545248" data-raw-source="[&lt;strong&gt;MicroEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545248)"><strong>MicroEntry</strong></a></p></td>
<td><p>响应发出 WIA 平板驱动程序的命令。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff547322" data-raw-source="[&lt;strong&gt;Scan&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547322)"><strong>Scan</strong></a></p></td>
<td><p>从设备读取数据并将数据返回到 WIA 平板驱动程序。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548129" data-raw-source="[&lt;strong&gt;SetPixelWindow&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548129)"><strong>SetPixelWindow</strong></a></p></td>
<td><p>设置要扫描的区域。</p></td>
</tr>
</tbody>
</table>

 

 

 




