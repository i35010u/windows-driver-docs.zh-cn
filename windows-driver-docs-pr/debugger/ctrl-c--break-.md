---
title: CTRL+C（中断）
description: CTRL + C 键中断调试器，停止目标应用程序或目标计算机，并取消调试器命令。
keywords:
- CTRL + C (Break) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+C (Break)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 76c443d96848a154d04c6e0d1dbffb59c244b65b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787001"
---
# <a name="ctrlc-break"></a>CTRL+C（中断）


CTRL + C 键中断调试器，停止目标应用程序或目标计算机，并取消调试器命令。

CDB 语法

```dbgcmd
CTRL+C 
```

KD 语法

```dbgcmd
CTRL+C 
```

目标计算机语法

```dbgcmd
SYSRQ 
ALT+SYSRQ 
F12 
```

## <span id="ddk_meta_ctrl_c_dbg"></span><span id="DDK_META_CTRL_C_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>调试器</strong></p></td>
<td align="left"><p>仅限 CDB 和 KD</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关发出此命令的其他方法以及相关命令的概述，请参阅 [控制目标](controlling-the-target.md)。

<a name="remarks"></a>备注
-------

**使用 CDB 时：**

在用户模式下，CTRL + C 键会使目标应用程序中断到调试器中。 目标应用程序会冻结，调试程序将变为活动状态，并且可以进入调试器命令。

如果调试器已处于活动状态，则 CTRL + C 不会影响目标应用程序。 不过，可以使用它来终止调试器命令。 例如，如果您请求了长时间的显示并且不再需要查看它，则 CTRL + C 将结束显示并返回到调试器命令提示符。

通过 CDB 执行远程调试时，可以在主计算机的键盘上按 CTRL + C。 如果要从目标计算机的键盘发出中断，请使用 x86 计算机上的 CTRL + C。

当正在调试的应用程序繁忙时，可以使用 F12 键来获取命令提示符。 将焦点设置在目标应用程序的一个窗口上，并在目标计算机上按 F12 键。

**使用 KD 时：**

在内核模式下，CTRL + C 键导致目标计算机中断到调试器。 这会锁定目标计算机并唤醒调试器。

调试仍在运行的系统时，必须在主机键盘上按 CTRL + C 以获取初始命令提示符。

如果调试器已处于活动状态，则 CTRL + C 不会影响目标计算机。 不过，可以使用它来终止调试器命令。 例如，如果您请求了长时间的显示并且不再需要查看它，则 CTRL + C 将结束显示并返回到调试器命令提示符。

当调试器命令正在生成长时间显示或目标计算机繁忙时，还可以使用 CTRL + C 来获取命令提示符。 在调试 x86 计算机时，可以在主机或目标键盘上按下。

增强型键盘上的 SYSRQ (或 ALT + SYSRQ) 类似。 它适用于任何处理器上的主机或目标键盘。 但是，它仅在通过按 CTRL + C 之前至少一次获得了提示的情况下才起作用。

可以通过编辑注册表来禁用 SYSRQ 键。 在注册表项中

```text
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\i8042prt\Parameters
```

创建一个名为 **BreakOnSysRq** 的值，并将其设置为等于 DWORD 0x0。 然后重新启动。 完成此操作后，按目标计算机键盘上的 SYSRQ 键不会进入内核调试器。

**用 CDB 调试 KD 时：**

如果正在使用 CDB 调试 KD，则主机调试器会截获 CTRL + C (CDB) 。 若要中断目标调试器 (KD) ，应改为使用 [**CTRL + F**](ctrl-f--break-to-kd-.md) 。

**注意**   请注意，在 WinDbg 中，CTRL + C 是用于从窗口复制文本的 [快捷键](keyboard-shortcuts.md) 。 若要在 WinDbg 中发出 break 命令，请使用 [CTRL + break](debug---break.md) 或选择 Debug |从菜单中中断。

 

 

 





