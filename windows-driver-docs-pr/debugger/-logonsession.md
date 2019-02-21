---
title: logonsession
description: Logonsession 扩展显示有关指定的登录会话的信息。
ms.assetid: 95746bc0-ab36-43a7-83ad-9f6fdbb15b39
keywords:
- 登录会话
- logonsession Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- logonsession
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 31b45551a4bf8fb778878793b428dd53e69703e2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554053"
---
# <a name="logonsession"></a>！ logonsession


**！ Logonsession**扩展显示有关指定的登录会话的信息。

免费生成语法

```dbgcmd
!logonsession LUID
```

已检验的版本语法

```dbgcmd
!logonsession LUID [InfoLevel]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______LUID______"></span><span id="_______luid______"></span> *LUID*   
指定要显示一个登录会话的本地唯一标识符 (LUID)。 如果*LUID*为 0，则显示有关所有登录会话的信息。

若要在调试内部版本中显示有关系统会话和系统的所有令牌的信息，请输入 **！ logonsession 3e7 1**。

<span id="_______InfoLevel______"></span><span id="_______infolevel______"></span><span id="_______INFOLEVEL______"></span> *InfoLevel*   
（仅已检验的版本）指定显示多少令牌信息。 *InfoLevel*参数可以采用值从 0 到 4，其中 0 表示最少信息和 4 代表大部分信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关登录会话的信息，请参阅 Microsoft Windows SDK 文档和*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 （这些资源可能不可用在某些语言和国家/地区中。）

<a name="remarks"></a>备注
-------

下面是输出的从上免费生成此扩展示例：

```dbgcmd
kd> !logonsession 0

Dumping all logon sessions.

** Session   0 = 0x0
   LogonId     = {0x0 0x0}
   References  = 0
** Session   1 = 0x8ebb50
 LogonId     = {0xe9f1 0x0}
   References  = 21
** Session   2 = 0x6e31e0
   LogonId     = {0x94d1 0x0}
   References  = 1
** Session   3 = 0x8ecd60
   LogonId     = {0x6b31 0x0}
   References  = 0
** Session   4 = 0xe0000106
   LogonId     = {0x0 0x0}
   References  = 0
** Session   5 = 0x0
   LogonId     = {0x0 0x0}
   References  = 0
** Session   6 = 0x8e9720
   LogonId     = {0x3e4 0x0}
   References  = 6
** Session   7 = 0xe0000106
   LogonId     = {0x0 0x0}
   References  = 0
** Session   8 = 0xa2e160
   LogonId     = {0x3e5 0x0}
   References  = 3
** Session   9 = 0xe0000106
   LogonId     = {0x0 0x0}
   References  = 0
** Session  10 = 0x3ca0
   LogonId     = {0x3e6 0x0}
   References  = 2
** Session  11 = 0xe0000106
   LogonId     = {0x0 0x0}
   References  = 0
** Session  12 = 0x1cd0
   LogonId     = {0x3e7 0x0}
   References  = 33
** Session  13 = 0xe0000106
 LogonId     = {0x0 0x0}
 References  = 0
14 sessions in the system.
```

可以通过按 CTRL + BREAK （在 WinDbg) 或 CTRL + C （中 KD) 来停止执行任何时候。

 

 





