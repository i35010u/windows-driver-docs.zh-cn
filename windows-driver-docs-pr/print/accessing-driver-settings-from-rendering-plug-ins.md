---
title: 从渲染插件访问驱动程序设置
description: 从渲染插件访问驱动程序设置
ms.assetid: d13526f5-85e1-4036-98fb-aea2c6d5a1e3
keywords:
- 呈现插件 WDK 打印，访问驱动程序设置
- 状态信息 WDK 打印插件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 376f013fb7b41c6679e29337e00cc25350bbd0c9
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103130"
---
# <a name="accessing-driver-settings-from-rendering-plug-ins"></a>从渲染插件访问驱动程序设置





呈现插件可以获取打印机功能和其他内部驱动程序信息的当前状态。 以下 COM 接口方法在 Microsoft 的打印机驱动程序中实现，并且可通过呈现插件进行调用。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>Unidrv 呈现插件实现以下方法：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetdriversetting" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvGetDriverSetting&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetdriversetting)"><strong>IPrintOemDriverUni：:D rvGetDriverSetting</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetstandardvariable" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvGetStandardVariable&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetstandardvariable)"><strong>IPrintOemDriverUni：:D rvGetStandardVariable</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetgpddata" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvGetGPDData&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetgpddata)"><strong>IPrintOemDriverUni：:D rvGetGPDData</strong></a></p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>Pscript5 呈现插件实现以下方法：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverps-drvgetdriversetting" data-raw-source="[&lt;strong&gt;IPrintOemDriverPS::DrvGetDriverSetting&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverps-drvgetdriversetting)"><strong>IPrintOemDriverPS：:D rvGetDriverSetting</strong></a></p></td>
</tr>
</tbody>
</table>

 

