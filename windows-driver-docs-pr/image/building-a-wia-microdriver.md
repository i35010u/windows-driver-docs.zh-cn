---
title: 构建 WIA 微驱动程序
description: 构建 WIA 微驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f64eb3c78b61acbef8a71546442cfacba36349d6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831429"
---
# <a name="building-a-wia-microdriver"></a>构建 WIA 微驱动程序





所有 WIA microdrivers 都需要以下标头文件和库文件。

### <a name="header-files"></a>标头文件

所有 WIA microdrivers 都必须包含下表中所示的标头文件。

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
<td><p><em>wiamicro</em></p></td>
<td><p>定义 WIA microdriver 所需的函数原型和结构。</p></td>
</tr>
</tbody>
</table>

 

WIA microdrivers 可能需要额外的标头文件。 所需的标头取决于设备类型和所实现的功能。 参考部分中注明了这些要求。

### <a name="library-files"></a>库文件

WIA 使用下表中显示的库文件。

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
<td><p>导出类标识符 (Clsid) 和接口标识符 (Iid) 。 所有 WIA microdrivers 都需要此库。</p></td>
</tr>
</tbody>
</table>

 

在生成环境中，WDK *包含* 和 *Lib* 目录应为搜索路径中的第一个目录。 这可确保使用最新版本的标头和库文件。

**注意**  如果你希望在生成 microdriver 时使用日志记录和 Visual C++ 6.0，请使用 Windows Me 驱动程序开发工具包 (DDK) 附带的 *Wialogcfg.exe* 程序打开 *Wiafbdrv.dll* 日志记录。 同时，检查 INF 文件以确保 microdriver 名称正确。 在 INF 中，查看 MicroDriver = "YOURNAME.DLL" 的 **DeviceData** 部分。

 

 

 




