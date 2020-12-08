---
title: logonsession
description: Logonsession 扩展显示有关指定登录会话的信息。
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
ms.openlocfilehash: 247aa16a3cd450e24e41bcea90e198f6a7a18b0b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811285"
---
# <a name="logonsession"></a>!logonsession


**！ Logonsession** 扩展显示有关指定登录会话的信息。

免费生成语法

```dbgcmd
!logonsession LUID
```

Checked Build 语法

```dbgcmd
!logonsession LUID [InfoLevel]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______LUID______"></span><span id="_______luid______"></span>*LUID*   
指定要显示的登录会话 (LUID) 的本地唯一标识符。 如果 *LUID* 为0，则显示有关所有登录会话的信息。

若要显示有关已检查生成中的系统会话和所有系统令牌的信息，请输入 **！ logonsession 3e7 1**。 在 Windows 10 版本1803之前，已检查的生成在 windows 的早期版本上可用。

<span id="_______InfoLevel______"></span><span id="_______infolevel______"></span><span id="_______INFOLEVEL______"></span>*InfoLevel*   
仅 (Checked Build) 指定显示多少标记信息。 *InfoLevel* 参数可采用0到4之间的值，0表示最小信息，4表示最多信息。 在 Windows 10 版本1803之前，已检查的生成在 windows 的早期版本上可用。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关登录会话的信息，Microsoft Windows SDK 请参阅 Russinovich 文档和 *Microsoft Windows 内部机制* ，并标记和 David 所罗门群岛。 

<a name="remarks"></a>备注
-------

下面是一个免费版本中此扩展的输出示例：

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

您可以通过在 WinDbg) 中按 CTRL + BREAK (或在 KD) 中按 CTRL + C (，随时停止执行。

 

 





