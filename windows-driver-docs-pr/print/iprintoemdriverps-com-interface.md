---
title: IPrintOemDriverPS COM 接口
description: IPrintOemDriverPS COM 接口
keywords:
- IPrintOemDriverPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e16b98c2acafd57d6bb700b6b0637fc4e533d4c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835527"
---
# <a name="iprintoemdriverps-com-interface"></a>IPrintOemDriverPS COM 接口





`IPrintOemDriverPS`COM 接口提供了一个呈现插件，其中包含对 Pscript5 的打印机图形 DLL 提供的实用工具操作的访问。 这些操作将数据流发送到打印后台处理程序，并获取驱动程序管理的信息。

下表列出并描述了该接口定义的所有方法 `IPrintOemDriverPS` 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverps-drvgetdriversetting" data-raw-source="[&lt;strong&gt;IPrintOemDriverPS::DrvGetDriverSetting&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverps-drvgetdriversetting)"><strong>IPrintOemDriverPS：:D rvGetDriverSetting</strong></a></p></td>
<td><p>返回打印机功能和其他内部信息的当前状态。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverps-drvwritespoolbuf" data-raw-source="[&lt;strong&gt;IPrintOemDriverPS::DrvWriteSpoolBuf&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverps-drvwritespoolbuf)"><strong>IPrintOemDriverPS：:D rvWriteSpoolBuf</strong></a></p></td>
<td><p>将打印机数据发送到后台处理程序。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅 [实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

