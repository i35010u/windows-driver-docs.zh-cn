---
title: 生成打印机图形 DLL
description: 生成打印机图形 DLL
keywords:
- 打印机图形 DLL WDK，生成
- 图形 DLL WDK 打印机，生成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b092886ef8dee5255c041f672f3717a87141783c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797757"
---
# <a name="building-a-printer-graphics-dll"></a>生成打印机图形 DLL





生成打印机图形 DLL 时，必须注意用于用户模式执行的 Dll 与用于内核模式执行的 Dll 之间的以下差异。

**注意**   在 Windows Vista 中，打印机图形 Dll 只能在用户模式下执行。 有关详细信息，请参阅 [选择用户模式或内核模式](choosing-user-mode-or-kernel-mode.md)。

 

### <a name="rules-for-building-a-printer-graphics-dll"></a>用于生成打印机图形 DLL 的规则

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>用户模式图形 DLL</th>
<th>内核模式图形 DLL</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>在源文件中设置 TARGETTYPE = DYNLINK。</p></td>
<td><p>在源文件中设置 TARGETTYPE = GDI_DRIVER。</p></td>
</tr>
<tr class="even">
<td><p>在包含 winddi 之前，必须在源文件中定义预处理器宏 USERMODE_DRIVER。</p></td>
<td><p>不得定义预处理器宏 USERMODE_DRIVER。</p></td>
</tr>
<tr class="odd">
<td><p>对象模块必须与 umpdddi 和 gdi32 导入库相关联。</p></td>
<td><p>对象模块必须与 win32k.sys 导入库链接。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows/win32/api/winddi/nf-winddi-drvquerydriverinfo" data-raw-source="[&lt;strong&gt;DrvQueryDriverInfo&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvquerydriverinfo)"><strong>DrvQueryDriverInfo</strong></a>函数必须为 DRVQUERY_USERMODE 返回<strong>TRUE</strong> 。</p></td>
<td><p><a href="/windows/win32/api/winddi/nf-winddi-drvquerydriverinfo" data-raw-source="[&lt;strong&gt;DrvQueryDriverInfo&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-drvquerydriverinfo)"><strong>DrvQueryDriverInfo</strong></a>函数必须为 DRVQUERY_USERMODE 返回<strong>FALSE</strong> 。  (或者，可以省略函数。 ) </p></td>
</tr>
</tbody>
</table>

 

