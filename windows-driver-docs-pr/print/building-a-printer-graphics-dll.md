---
title: 生成打印机图形 DLL
description: 生成打印机图形 DLL
ms.assetid: bec1e9cc-a846-43e5-bc9e-e43a151ef6c4
keywords:
- 打印机图形 DLL WDK，构建
- 图形 DLL WDK 打印机、 构建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e203066f09f027d734a131089edb42948f218eb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330385"
---
# <a name="building-a-printer-graphics-dll"></a>生成打印机图形 DLL





在生成时打印机图形 DLL，您必须注意以下差异适用于用户模式下执行和那些适用于内核模式执行的 Dll 间。

**请注意**  在 Windows Vista 中，在用户模式下只能执行打印机图形 Dll。 有关详细信息，请参阅[选择用户模式或内核模式](choosing-user-mode-or-kernel-mode.md)。

 

### <a name="rules-for-building-a-printer-graphics-dll"></a>用于构建打印机图形 DLL 规则

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
<td><p>设置 TARGETTYPE = DYNLINK 源文件中的。</p></td>
<td><p>设置 TARGETTYPE = GDI_DRIVER 源文件中的。</p></td>
</tr>
<tr class="even">
<td><p>包含 winddi.h 之前，必须在源文件中定义预处理器宏 USERMODE_DRIVER。</p></td>
<td><p>预处理器宏 USERMODE_DRIVER 必须未定义。</p></td>
</tr>
<tr class="odd">
<td><p>对象模块必须与链接 umpdddi.lib 和 gdi32.lib 导入库。</p></td>
<td><p>必须与 win32k.lib 导入库链接对象模块。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556261" data-raw-source="[&lt;strong&gt;DrvQueryDriverInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556261)"> <strong>DrvQueryDriverInfo</strong> </a>函数必须返回<strong>TRUE</strong> DRVQUERY_USERMODE 的。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556261" data-raw-source="[&lt;strong&gt;DrvQueryDriverInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556261)"> <strong>DrvQueryDriverInfo</strong> </a>函数必须返回<strong>FALSE</strong> DRVQUERY_USERMODE 的。 （或者，该函数可以省略。）</p></td>
</tr>
</tbody>
</table>

 

 

 




