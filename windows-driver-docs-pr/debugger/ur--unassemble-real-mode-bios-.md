---
title: ur（取消汇编实际模式 BIOS）
description: 你的命令将显示指定的16位实模式代码的程序集转换。
keywords:
- " (Unassemble 实模式 BIOS) Windows 调试"
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ur (Unassemble Real Mode BIOS)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5bfcea5a629c9468adbd6dd5069bf9dbbe0f2f5e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803239"
---
# <a name="ur-unassemble-real-mode-bios"></a>ur（取消汇编实际模式 BIOS）


**你** 的命令将显示指定的16位实模式代码的程序集转换。

```dbgcmd
ur Range 
ur Address
ur 
```

## <a name="span-idddk_cmd_unassemble_real_mode_bios_dbgspanspan-idddk_cmd_unassemble_real_mode_bios_dbgspanparameters"></a><span id="ddk_cmd_unassemble_real_mode_bios_dbg"></span><span id="DDK_CMD_UNASSEMBLE_REAL_MODE_BIOS_DBG"></span>参数


<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span>*范围*   
指定包含要拆装的指令的内存范围。 有关语法的详细信息，请参阅 [address 和 Address Range 语法](address-and-address-range-syntax.md)。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定要反汇编的内存范围的开始位置。 基于 x86 的 processorare unassembled 上的八个说明。 有关语法的详细信息，请参阅 [address 和 Address Range 语法](address-and-address-range-syntax.md)。

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关如何调试 BIOS 代码的详细信息，请参阅 [调试 Bios 代码](debugging-bios-code.md)。

<a name="remarks"></a>备注
-------

如果不指定 *范围* 或 *地址*，则反汇编将从当前地址开始，并在基于 x86 的处理器上扩展八个指令。

如果要在基于 x86 的处理器上检查16位实模式代码， **则命令和** [**u (Unassemble)**](u--unassemble-.md) 命令均会获得正确的结果。

但是，如果实模式代码存在于调试器不期望的位置 (例如，运行或通过插件卡模拟基于 x86 的 BIOS 代码的非 x86 计算机) ，则 **必须使用来正确地拆装** 此代码。

如果使用的是32位或64位代码，则该 **命令将尝试** 反汇编代码，就像它是16位代码一样。 这种情况会产生无意义的结果。

 

 





