---
title: MRU 源列表函数
description: MRU 源列表函数
ms.assetid: 62c6b144-5883-45cf-a114-7b82453f275f
keywords:
- Setupapi.log 函数 WDK，最近使用的源列表
- 最近使用的源列表 WDK Setupapi.log
- MRU 源列表 WDK Setupapi.log
- 源列出 WDK MRU
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72e6f9f36404131e059b035c577a7be6a2678547
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716350"
---
# <a name="mru-source-list-functions"></a>MRU 源列表函数





最近使用的 (MRU) 源列表驻留在用户的计算机上，并包含与以前的安装中使用的源路径有关的信息。 提示用户输入源路径时，可以使用此信息。

如果应用程序具有管理员权限，则 *设备安装应用程序* 可以访问该系统范围内的源列表。 设备安装应用程序还可以创建一个临时源列表，该列表在设备安装应用程序退出时被丢弃。 通过调用 **SetupSetSourceList**，设备安装应用程序将标识它将在安装过程中使用的源列表。

下表列出了可用于操作源列表的函数。 有关详细的函数说明，请参阅 Microsoft Windows SDK 文档。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setupaddtosourcelista" data-raw-source="[&lt;strong&gt;SetupAddToSourceList&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setupaddtosourcelista)"><strong>SetupAddToSourceList</strong></a></p></td>
<td align="left"><p>向源列表中添加项。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setupcanceltemporarysourcelist" data-raw-source="[&lt;strong&gt;SetupCancelTemporarySourceList&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setupcanceltemporarysourcelist)"><strong>SetupCancelTemporarySourceList</strong></a></p></td>
<td align="left"><p>取消使用临时列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setupfreesourcelista" data-raw-source="[&lt;strong&gt;SetupFreeSourceList&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setupfreesourcelista)"><strong>SetupFreeSourceList</strong></a></p></td>
<td align="left"><p>释放先前对 <a href="/windows/win32/api/setupapi/nf-setupapi-setupsetsourcelista" data-raw-source="[&lt;strong&gt;SetupSetSourceList&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setupsetsourcelista)"><strong>SetupSetSourceList</strong></a>的调用分配的资源。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setupquerysourcelista" data-raw-source="[&lt;strong&gt;SetupQuerySourceList&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setupquerysourcelista)"><strong>SetupQuerySourceList</strong></a></p></td>
<td align="left"><p>查询当前安装源列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setupremovefromsourcelista" data-raw-source="[&lt;strong&gt;SetupRemoveFromSourceList&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setupremovefromsourcelista)"><strong>SetupRemoveFromSourceList</strong></a></p></td>
<td align="left"><p>从安装源列表中删除条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setupsetsourcelista" data-raw-source="[&lt;strong&gt;SetupSetSourceList&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setupsetsourcelista)"><strong>SetupSetSourceList</strong></a></p></td>
<td align="left"><p>将安装源列表设置为系统 MRU 列表、用户 MRU 列表或临时列表。</p></td>
</tr>
</tbody>
</table>

 

