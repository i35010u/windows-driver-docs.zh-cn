---
title: dreg
description: Dreg 扩展显示注册表信息。
ms.assetid: a54ed14e-eb9d-48fd-877d-d6d0fe4a8d3f
keywords:
- dreg Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dreg
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 163f816b7026bafb6091f5cae9c42d77a9c2769c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564956"
---
# <a name="dreg"></a>!dreg


**！ Dreg**扩展显示注册表信息。

```dbgcmd
!dreg [-d|-w] KeyPath[!Value] 
!dreg
```

## <a name="span-idddkdregdbgspanspan-idddkdregdbgspanparameters"></a><span id="ddk__dreg_dbg"></span><span id="DDK__DREG_DBG"></span>参数


<span id="_______-d______"></span><span id="_______-D______"></span> **-d**   
导致二进制值显示为 dword 值。

<span id="_______-w______"></span><span id="_______-W______"></span> **-w**   
导致二进制值显示为单词。

<span id="_______KeyPath______"></span><span id="_______keypath______"></span><span id="_______KEYPATH______"></span> *KeyPath*   
指定的注册表项路径。 它可以开始使用任何下列缩写：

<span id="hklm"></span><span id="HKLM"></span>**hklm**  
HKEY\_本地\_机

<span id="hkcu"></span><span id="HKCU"></span>**hkcu**  
HKEY\_当前\_用户

<span id="hkcr"></span><span id="HKCR"></span>**hkcr**  
HKEY\_类\_根

<span id="hku"></span><span id="HKU"></span>**hku**  
HKEY\_用户

如果不使用缩写词，HKEY\_本地\_假定计算机。

<span id="_______Value______"></span><span id="_______value______"></span><span id="_______VALUE______"></span> *值*   
指定要显示的注册表值的名称。 如果星号 (\*) 是使用时，将显示所有值。 如果*值*是省略，将显示所有子项。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ntsdexts.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ntsdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关注册表的信息，请参阅 Windows Driver Kit (WDK) 文档和*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 （这些资源可能不可用在某些语言和国家/地区中。）

<a name="remarks"></a>备注
-------

**！ Dreg**扩展可用于在用户模式下调试过程中显示注册表。

它是在远程调试过程中最有用的因为它允许您浏览远程计算机的注册表。 也很有用时控制用户模式下的调试程序与内核调试程序，因为它已被冻结时，不能在目标计算机上运行标准注册表编辑器。 (可以使用[ **.sleep** ](-sleep--pause-debugger-.md)命令实现此目的以及。 请参阅[控制用户模式下调试程序与内核调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)有关详细信息。)

本地调试，作为信息中的易读的格式呈现时，它是也很有用。

如果 **！ dreg**使用内核模式调试中，在显示的结果将为主机计算机，而不是目标计算机。 若要显示目标计算机的原始注册表信息，请使用[ **！ reg** ](-reg.md)扩展相反。

下面是一些示例。 下面将显示指定的注册表项的所有子项：

```dbgcmd
!dreg hkcu\Software\Microsoft
```

下面将显示所有值中指定的注册表项：

```dbgcmd
!dreg System\CurrentControlSet\Services\Tcpip!*
```

以下将在指定的注册表项中显示的值开始：

```dbgcmd
!dreg System\CurrentControlSet\Services\Tcpip!Start
```

键入 **！ dreg**没有任何参数将在调试器命令窗口中显示此扩展的一些简要帮助文本。

 

 





