---
title: 微驱动程序函数
description: 微驱动程序函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ceedf2a3f4e31f1e6c3fe37fc3536eb5cbc2df84
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792235"
---
# <a name="microdriver-functions"></a>微驱动程序函数





WIA 平板驱动程序通过调用 WIA microdriver 函数来响应来自 WIA 服务的请求。 这些函数必须由供应商提供的每个 microdriver 实现，并且包含以下各项：

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
<td><p><a href="/windows-hardware/drivers/ddi/wiamicro/nf-wiamicro-microentry" data-raw-source="[&lt;strong&gt;MicroEntry&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamicro/nf-wiamicro-microentry)"><strong>MicroEntry</strong></a></p></td>
<td><p>响应 WIA 平板驱动程序发送的命令。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiamicro/nf-wiamicro-scan" data-raw-source="[&lt;strong&gt;Scan&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamicro/nf-wiamicro-scan)"><strong>扫描</strong></a></p></td>
<td><p>从设备读取数据并将数据返回到 WIA 平板驱动程序。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiamicro/nf-wiamicro-setpixelwindow" data-raw-source="[&lt;strong&gt;SetPixelWindow&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiamicro/nf-wiamicro-setpixelwindow)"><strong>SetPixelWindow</strong></a></p></td>
<td><p>设置要扫描的区域。</p></td>
</tr>
</tbody>
</table>

 

