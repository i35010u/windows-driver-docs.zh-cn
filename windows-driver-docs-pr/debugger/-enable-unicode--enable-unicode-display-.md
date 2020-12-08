---
title: .enable_unicode（启用 Unicode 显示）
description: .Enable_unicode 命令指定调试器是否将 USHORT 指针和数组显示为 Unicode 字符串。
keywords:
- " ( .enable_unicode) 命令启用 Unicode 显示"
- UNICODE_STRING 结构
- .enable_unicode (在 Windows 调试) 启用 Unicode 显示
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .enable_unicode (Enable Unicode Display)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4e8ca2187a2b672af5b5c0c412db6008b9e44fbe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818723"
---
# <a name="enable_unicode-enable-unicode-display"></a>。启用 \_ unicode (启用 Unicode 显示) 


**. Enable \_ unicode** 命令指定调试器是否将 USHORT 指针和数组显示为 unicode 字符串。

```dbgcmd
.enable_unicode 0 
.enable_unicode 1
```

## <a name="span-idddk_meta_enable_unicode_display_dbgspanspan-idddk_meta_enable_unicode_display_dbgspanparameters"></a><span id="ddk_meta_enable_unicode_display_dbg"></span><span id="DDK_META_ENABLE_UNICODE_DISPLAY_DBG"></span>参数


<span id="_______0______"></span>**0**   
以短整数的形式显示所有16位 (USHORT) 数组和指针。 这是调试器的默认行为。

<span id="_______1______"></span>**1**   
显示所有16位 (USHORT) 数组和指针作为 Unicode 字符串。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**Enable \_ unicode** 命令会影响 [**dt (显示类型)**](dt--display-type-.md)命令的输出。

在 WinDbg 中， **enable \_ unicode** 命令还会影响在 "局部变量" [窗口](locals-window.md) 和 "监视窗口" 中的显示。 发出后，这些窗口会自动更新 **。启用 \_ unicode**。

你还可以选择或清除 "在局部变量或监视窗口的快捷菜单上以 Unicode 的形式 **显示16位值** ，以便为 USHORT 数组和指针指定显示。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**ds、dS（显示字符串）**](ds--ds--display-string-.md)

 

 






