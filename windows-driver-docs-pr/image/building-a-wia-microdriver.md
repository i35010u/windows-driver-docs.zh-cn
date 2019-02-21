---
title: 构建 WIA Microdriver
description: 构建 WIA Microdriver
ms.assetid: dcec3079-2844-4d87-b2e4-0c1850118192
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fe2bdb19ccc7141c2a32cf72b7305339d2207ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524353"
---
# <a name="building-a-wia-microdriver"></a>构建 WIA Microdriver





以下标头文件和库文件所需所有 WIA microdrivers。

### <a name="header-files"></a>标头文件

所有 WIA microdrivers 必须都包含以下表所示的标头文件。

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
<td><p><em>wiamicro.h</em></p></td>
<td><p>定义的函数原型和 WIA microdriver 要求的结构。</p></td>
</tr>
</tbody>
</table>

 

WIA microdrivers 可能需要其他头文件。 所需的标头依赖于设备类型和实现的功能。 在引用部分注明了这些要求。

### <a name="library-files"></a>库文件

WIA 使用下表中所示的库文件。

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
<td><p>导出的类标识符 (Clsid) 和接口的标识符 (Iid)。 所有 WIA microdrivers 都需要此库。</p></td>
</tr>
</tbody>
</table>

 

在生成环境中，WDK *Include*并*Lib*目录应在搜索路径中的第一个目录。 这可确保使用最新版本的标头和库文件。

**请注意**  如果你想要随 Visual c + + 6.0 一起使用日志记录，生成 microdriver 时，启用日志记录*Wiafbdrv.dll*通过*Wialogcfg.exe*自带程序Windows Me 驱动程序开发工具包 (DDK)。 另外，检查以确保 microdriver 名称是正确的 INF 文件。 在 INF，检查**DeviceData**部分，了解 MicroDriver ="YOURNAME。DLL"。

 

 

 




