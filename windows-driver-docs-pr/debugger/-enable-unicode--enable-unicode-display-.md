---
title: .enable_unicode（启用 Unicode 显示）
description: .Enable_unicode 命令指定调试器为 Unicode 字符串是否显示 USHORT 指针和数组。
ms.assetid: bb029ff4-1802-4d91-ba4b-9db10fa7c055
keywords:
- 启用 Unicode 显示 (.enable_unicode) 命令
- UNICODE_STRING 结构
- .enable_unicode （启用 Unicode 显示器） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .enable_unicode (Enable Unicode Display)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bbab1c0d18f3d1adeba498da7f58ed2f9ec2d790
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334526"
---
# <a name="enableunicode-enable-unicode-display"></a>.enable\_unicode （启用 Unicode 显示屏）


**.Enable\_unicode**命令指定调试器为 Unicode 字符串是否显示 USHORT 指针和数组。

```dbgcmd
.enable_unicode 0 
.enable_unicode 1
```

## <a name="span-idddkmetaenableunicodedisplaydbgspanspan-idddkmetaenableunicodedisplaydbgspanparameters"></a><span id="ddk_meta_enable_unicode_display_dbg"></span><span id="DDK_META_ENABLE_UNICODE_DISPLAY_DBG"></span>参数


<span id="_______0______"></span> **0**   
将所有的 16 位 (USHORT) 数组和指针显示为短整数。 这是在调试器的默认行为。

<span id="_______1______"></span> **1**   
将所有的 16 位 (USHORT) 数组和指针显示为 Unicode 字符串。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**.Enable\_unicode**命令影响的输出[ **dt （显示类型）** ](dt--display-type-.md)命令。

在 WinDbg 中， **.enable\_unicode**命令还会影响在显示[局部变量窗口](locals-window.md)和监视窗口。 这些窗口会自动更新后发出 **.enable\_unicode**。

您还可以选择或清除**显示 16 位值**为局部变量或监视的快捷菜单上的 Unicode 窗口指定 USHORT 数组和指针的显示。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**ds，dS （显示字符串）**](ds--ds--display-string-.md)

 

 






