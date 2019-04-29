---
title: CTRL+C（中断）
description: CTRL + C 键进入调试器，停止目标应用程序或目标计算机，并取消调试器命令。
ms.assetid: ee9df6d7-4a40-4006-90df-478e06899e3a
keywords:
- CTRL + C （中断） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+C (Break)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 82745fadf91909aad4b85c6760f3012a3eab3b4e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374422"
---
# <a name="ctrlc-break"></a>CTRL+C（中断）


CTRL + C 键进入调试器，停止目标应用程序或目标计算机，并取消调试器命令。

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
<td align="left"><p>CDB 和 KD 仅</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

发出此命令，并概述的相关命令的其他方法，请参阅[控制目标](controlling-the-target.md)。

<a name="remarks"></a>备注
-------

**当使用 CDB:**

在用户模式下的 CTRL + C 键将导致目标应用程序运行中断到调试器。 目标应用程序冻结，调试器将变为活动状态，并且可以输入调试器命令。

如果调试器已处于活动状态，CTRL + C 不会影响目标应用程序。 它，但是，可用来终止调试器命令。 例如，如果已请求很长并且不想再看到它，CTRL + C 将结束显示并使你返回到调试器命令提示符下。

在执行使用 CDB 进行远程调试时，可以在主计算机的键盘上按 CTRL + C。 如果你想要发出从目标计算机的键盘中断，使用 CTRL + C 在 x86 计算机。

F12 键可以用于获取命令提示符下，当正在调试的应用程序正在使用中。 其中一个目标应用程序的 windows 上设置焦点并在目标计算机上按 F12 键。

**当使用 KD:**

在内核模式下的 CTRL + C 键将导致目标计算机进入调试器。 这将锁定目标计算机并唤醒调试器。

在调试时仍在运行的系统，主机键盘上按 CTRL + C，必须获取初始的命令提示符。

如果调试器已处于活动状态，CTRL + C 不会影响目标计算机。 它可以使用，但是，若要终止的调试器命令。 例如，如果已请求很长并且不想再看到它，CTRL + C 将结束显示并使你返回到调试器命令提示符下。

此外可以使用 CTRL + C 调试器命令生成很长或当目标计算机是繁忙时获取命令提示符。 当调试 x86 计算机，它可以在主机或目标键盘上按下。

SYSRQ （或增强型键盘上的 ALT + SYSRQ） 是类似。 它适用于任何处理器主机或目标键盘。 但是，它仅适用于已通过按 CTRL + C 至少一次之前获取提示。

可以通过编辑注册表禁用 SYSRQ 密钥。 注册表项中

```text
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\i8042prt\Parameters
```

创建一个名为值**BreakOnSysRq**，并将其设置为等于 DWORD 0x0。 然后重新启动。 此操作完成后，目标计算机的键盘上按 SYSRQ 键不会中断到内核调试程序。

**调试与 CDB KD 时：**

如果你正在调试使用 CDB KD，CTRL + C 将截获由主机调试器 (CDB)。 若要进入目标调试器 (KD)，应使用[ **CTRL + F** ](ctrl-f--break-to-kd-.md)相反。

**请注意**  请注意，在 WinDbg 中，CTRL + C[快捷键](keyboard-shortcuts.md)用于从窗口中复制的文本。 若要发出中断命令在 WinDbg 中的，使用[CTRL + BREAK](debug---break.md)或选择调试 |从菜单中断。

 

 

 





