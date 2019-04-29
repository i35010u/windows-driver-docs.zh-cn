---
title: 构建 WIA 微型驱动程序
description: 构建 WIA 微型驱动程序
ms.assetid: 7a13d355-f42e-406d-8cba-4739df1af9fa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6d603118cbf835286e462799a257b2fc1f9d4b9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373310"
---
# <a name="building-a-wia-minidriver"></a>构建 WIA 微型驱动程序





以下标头文件和库文件所需所有 WIA 微型驱动程序。

### <a name="header-files"></a>标头文件

所有 WIA 微型驱动程序必须都包含以下表所示的标头文件。

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
<td><p><em>sti.h</em></p></td>
<td><p>定义 STI 接口、 结构和事件 WIA 微型驱动程序可以使用的 Guid。</p></td>
</tr>
<tr class="even">
<td><p><em>stiusd.h</em></p></td>
<td><p>定义<a href="https://msdn.microsoft.com/library/windows/hardware/ff543827" data-raw-source="[IStiUSD](https://msdn.microsoft.com/library/windows/hardware/ff543827)">IStiUSD</a>所有 WIA 微型驱动程序必须都实现的接口。</p></td>
</tr>
<tr class="odd">
<td><p><em>wiamindr.h</em></p></td>
<td><p>定义<a href="https://msdn.microsoft.com/library/windows/hardware/ff545027" data-raw-source="[IWiaMiniDrv](https://msdn.microsoft.com/library/windows/hardware/ff545027)">IWiaMiniDrv</a>所有 WIA 微型驱动程序必须都实现的接口。 使用 WIA 微型驱动程序的其他接口在此处定义也。</p></td>
</tr>
</tbody>
</table>

 

WIA 微型驱动程序可能需要其他头文件。 所需的标头依赖于设备类型和实现的功能。 在引用部分注明了这些要求。

### <a name="library-files"></a>库文件

WIA 使用下表中所示的库文件。 所有微型驱动程序需要这些库。

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
<td><p><em>wiaguid.lib</em></p></td>
<td><p>导出的类标识符 (Clsid) 和接口的标识符 (Iid)。</p></td>
</tr>
<tr class="even">
<td><p><em>wiaservc.lib</em></p></td>
<td><p>导出 WIA 服务帮助程序函数。</p></td>
</tr>
</tbody>
</table>

 

在生成环境中，WDK *Include*并*Lib*目录应在搜索路径中的第一个目录。 这可确保使用最新版本的标头和库文件。

 

 




