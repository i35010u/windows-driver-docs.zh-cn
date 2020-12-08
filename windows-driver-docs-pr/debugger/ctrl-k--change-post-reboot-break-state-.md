---
title: CTRL+K（更改重新启动后的中断状态）
description: CTRL + K 键会改变调试器自动中断到目标计算机的条件。
keywords:
- CTRL + K (更改重新启动后中断状态) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+K (Change Post-Reboot Break State)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: eedef53f9e49300484ebad5f2aced55388c627c6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786991"
---
# <a name="ctrlk-change-post-reboot-break-state"></a>CTRL+K（更改重新启动后的中断状态）


CTRL + K 键会改变调试器自动中断到目标计算机的条件。

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
<td align="left"><p>仅限 KD 和 WinDbg</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅限内核模式</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关相关命令的概述以及重新启动过程如何影响调试器的说明，请参阅 [崩溃并重新启动目标计算机](crashing-and-rebooting-the-target-computer.md)。

<a name="remarks"></a>备注
-------

此控制键会导致内核调试器遍历以下三种状态：

<span id="No_break"></span><span id="no_break"></span><span id="NO_BREAK"></span>**无中断**  
在此状态下，除非按下 [**CTRL + C**](ctrl-c--break-.md)，否则调试器不会中断目标计算机。

<span id="Break_on_reboot"></span><span id="break_on_reboot"></span><span id="BREAK_ON_REBOOT"></span>**重新启动时中断**  
在此状态下，调试程序将在初始化内核后中断到重新启动的目标计算机。 这等效于通过 **-b**[命令行选项](command-line-options.md)启动 KD 或 WinDbg。

<span id="Break_on_first_module_load"></span><span id="break_on_first_module_load"></span><span id="BREAK_ON_FIRST_MODULE_LOAD"></span>**第一次模块加载时中断**  
在此状态下，在加载第一个内核模块后，调试器将中断到重新启动的目标计算机。  (这将导致中断早于 " **重新启动时中断** " 选项。 ) 这等效于通过 **-d**[命令行选项](command-line-options.md)启动 KD 或 WinDbg。

使用 CTRL + K 时，将显示新的中断状态。

在 WinDbg，还可以通过选择 "调试" [|内核连接 |循环初始中断](debug---kernel-connection---cycle-initial-break.md)。

 

 





