---
title: 构建 WIA 微型驱动程序
description: 构建 WIA 微型驱动程序
ms.assetid: 7a13d355-f42e-406d-8cba-4739df1af9fa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8493f6d3f64d2513f8ad5614171247fb4599f1d4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840887"
---
# <a name="building-a-wia-minidriver"></a>构建 WIA 微型驱动程序





所有 WIA 微型驱动程序都需要以下标头文件和库文件。

### <a name="header-files"></a>标头文件

所有 WIA 微型驱动程序都必须包含下表中所示的标头文件。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>标头文件</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>sti</em></p></td>
<td><p>定义 WIA 微型驱动程序可以使用的 STI 接口、结构和事件 Guid。</p></td>
</tr>
<tr class="even">
<td><p><em>stiusd</em></p></td>
<td><p>定义所有 WIA 微型驱动程序必须实现的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index" data-raw-source="[IStiUSD](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)">IStiUSD</a>接口。</p></td>
</tr>
<tr class="odd">
<td><p><em>wiamindr</em></p></td>
<td><p>定义所有 WIA 微型驱动程序必须实现的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv" data-raw-source="[IWiaMiniDrv](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)">IWiaMiniDrv</a>接口。 WIA 微型驱动程序使用的其他接口也在此处定义。</p></td>
</tr>
</tbody>
</table>

 

WIA 微型驱动程序可能需要额外的标头文件。 所需的标头取决于设备类型和所实现的功能。 参考部分中注明了这些要求。

### <a name="library-files"></a>库文件

WIA 使用下表中显示的库文件。 所有微型驱动程序都需要这些库。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>库文件</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>wiaguid</em></p></td>
<td><p>导出类标识符（Clsid）和接口标识符（Iid）。</p></td>
</tr>
<tr class="even">
<td><p><em>wiaservc</em></p></td>
<td><p>导出 WIA 服务帮助程序函数。</p></td>
</tr>
</tbody>
</table>

 

在生成环境中，WDK*包含*和*Lib*目录应为搜索路径中的第一个目录。 这可确保使用最新版本的标头和库文件。

 

 




