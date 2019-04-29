---
title: CTRL+K（更改重新启动后的中断状态）
description: CTRL + K 键更改在其调试程序将自动中断到目标计算机的条件。
ms.assetid: 74f57775-63ad-4a96-9ba5-bfedd4c8c826
keywords:
- CTRL + K （更改重启后中断状态） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+K (Change Post-Reboot Break State)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 918a4ccd632f2d8534b5fca185c94fd19d6efd10
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374975"
---
# <a name="ctrlk-change-post-reboot-break-state"></a>CTRL+K（更改重新启动后的中断状态）


CTRL + K 键更改在其调试程序将自动中断到目标计算机的条件。

KD 语法

```dbgcmd
CTRL+K  ENTER 
```

WinDbg 语法

```dbgcmd
CTRL+ALT+K 
```

## <span id="ddk_meta_ctrl_k_dbg"></span><span id="DDK_META_CTRL_K_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>调试器</strong></p></td>
<td align="left"><p>KD 和 WinDbg 仅</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>内核模式下</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

相关命令的概述和重启过程是如何影响调试器的说明，请参阅[崩溃和重新启动目标计算机](crashing-and-rebooting-the-target-computer.md)。

<a name="remarks"></a>备注
-------

此控制密钥会导致以下三个状态之间循环内核调试器：

<span id="No_break"></span><span id="no_break"></span><span id="NO_BREAK"></span>**无分隔符**  
在此状态下，调试器不会中断到目标计算机按，否则[ **CTRL + C**](ctrl-c--break-.md)。

<span id="Break_on_reboot"></span><span id="break_on_reboot"></span><span id="BREAK_ON_REBOOT"></span>**在重新启动时中断**  
在此状态下，调试器将中断到重新启动的目标计算机后进行初始化。 这相当于启动 KD 或的 WinDbg **-b**[命令行选项](command-line-options.md)。

<span id="Break_on_first_module_load"></span><span id="break_on_first_module_load"></span><span id="BREAK_ON_FIRST_MODULE_LOAD"></span>**第一个模块加载时中断**  
在此状态下，调试器将中断到重新启动的目标计算机后加载第一个内核模块。 (这将导致要比前面**上重新启动中断**选项。)这相当于启动 KD 或的 WinDbg **-d**[命令行选项](command-line-options.md)。

当使用 CTRL + K 时，显示新的中断状态。

在 WinDbg 中，还可以通过选择[调试 |内核连接 |周期初始中断](debug---kernel-connection---cycle-initial-break.md)。

 

 





