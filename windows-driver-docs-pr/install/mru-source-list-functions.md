---
title: MRU 源列表函数
description: MRU 源列表函数
ms.assetid: 62c6b144-5883-45cf-a114-7b82453f275f
keywords:
- 安装程序 Api 函数 WDK，最近使用的源列表
- 最近使用的源列表 WDK SetupAPI
- MRU 源列表 WDK SetupAPI
- 源列表 WDK MRU
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 119a8ce44075f8146fe3654c60c40865bf08ad5f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383816"
---
# <a name="mru-source-list-functions"></a>MRU 源列表函数





最近使用 (过的 MRU) 源列表是驻留在用户计算机上的包含有关在以前安装中使用的源路径的信息。 提示用户输入的源路径时，可以使用此信息。

*设备安装应用程序*可访问特定于用户的源列表和应用程序具有管理员权限，整个系统源列表。 设备安装应用程序还可以创建一个临时源列表，其中的设备安装应用程序退出时将被丢弃。 通过调用**SetupSetSourceList**，设备安装应用程序标识它将在安装期间使用的源列表。

下表列出了可用于处理源列表的函数。 有关详细的功能描述，请参阅 Microsoft Windows SDK 文档。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa376981" data-raw-source="[&lt;strong&gt;SetupAddToSourceList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa376981)"><strong>SetupAddToSourceList</strong></a></p></td>
<td align="left"><p>将条目添加到源列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa376983" data-raw-source="[&lt;strong&gt;SetupCancelTemporarySourceList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa376983)"><strong>SetupCancelTemporarySourceList</strong></a></p></td>
<td align="left"><p>取消使用的临时列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377241" data-raw-source="[&lt;strong&gt;SetupFreeSourceList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377241)"><strong>SetupFreeSourceList</strong></a></p></td>
<td align="left"><p>释放通过以前调用分配的资源<a href="https://msdn.microsoft.com/library/windows/desktop/aa377441" data-raw-source="[&lt;strong&gt;SetupSetSourceList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377441)"> <strong>SetupSetSourceList</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377419" data-raw-source="[&lt;strong&gt;SetupQuerySourceList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377419)"><strong>SetupQuerySourceList</strong></a></p></td>
<td align="left"><p>查询当前的安装源列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377431" data-raw-source="[&lt;strong&gt;SetupRemoveFromSourceList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377431)"><strong>SetupRemoveFromSourceList</strong></a></p></td>
<td align="left"><p>从安装源列表中删除一个条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377441" data-raw-source="[&lt;strong&gt;SetupSetSourceList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377441)"><strong>SetupSetSourceList</strong></a></p></td>
<td align="left"><p>将安装源列表设置为系统 MRU 列表、 用户 MRU 列表中或临时列表。</p></td>
</tr>
</tbody>
</table>

 

 

 





