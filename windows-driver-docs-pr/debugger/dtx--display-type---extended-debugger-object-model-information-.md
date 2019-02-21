---
title: dtx （显示类型的扩展的调试器对象模型信息）
description: Dtx 命令显示使用调试器对象模型的扩展符号类型信息。 Dtx 命令为类似于 dt （显示类型） 命令。
ms.assetid: 758D752E-65A0-4F1D-BB56-06E4ECEC6D48
keywords:
- dtx （显示类型的扩展的调试器对象模型信息） Windows 调试
ms.date: 09/17/2017
topic_type:
- apiref
api_name:
- dtx (Display Type - Extended Debugger Object Model Information)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 148b1f9be720fcdfa9fbe669c64778803b49659f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523652"
---
# <a name="span-iddebuggerdtxdisplaytype-extendeddebuggerobjectmodelinformationspandtx-display-type---extended-debugger-object-model-information"></a><span id="debugger.dtx__display_type_-_extended_debugger_object_model_information_"></span>dtx （显示类型的扩展的调试器对象模型信息）


Dtx 命令显示使用调试器对象模型的扩展符号类型信息。 Dtx 命令是类似于[ **dt （显示类型）** ](dt--display-type-.md)命令。

```dbgcmd
dtx -DisplayOpts [Module!]Name Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="________DisplayOpts_______"></span><span id="________displayopts_______"></span><span id="________DISPLAYOPTS_______"></span> **DisplayOpts**   
使用以下可选标志来更改输出的显示方式。

*-a*显示数组具有其索引的新行中的元素。

*-r \[n\]* 以递归方式转储子类型 （字段） 最多*n*级别。

*-h*显示 dtx 命令的命令行帮助。

<span id="Module______________"></span><span id="module______________"></span><span id="MODULE______________"></span>**模块 ！**   
可选参数，指定定义此结构后, 跟感叹号的模块。 如果没有本地变量或具有全局变量或类型的名称相同的类型，则应包含*模块*名称来指定一个全局变量。

<span id="________Name_______"></span><span id="________name_______"></span><span id="________NAME_______"></span> **名称**   
类型名称或全局符号。

<span id="________Address_______"></span><span id="________address_______"></span><span id="________ADDRESS_______"></span> **Address**   
包含该类型的内存地址。

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

以下示例演示如何使用 dtx 命令。

使用的地址和名称以显示扩展符号类型信息。

```dbgcmd
0: kd> dtx nt!_EPROCESS ffffb607560b56c0
(*((nt!_EPROCESS *)0xffffb607560b56c0))                 [Type: _EPROCESS]
    [+0x000] Pcb              [Type: _KPROCESS]
    [+0x2d8] ProcessLock      [Type: _EX_PUSH_LOCK]
    [+0x2e0] RundownProtect   [Type: _EX_RUNDOWN_REF]
    [+0x2e8] UniqueProcessId  : 0x4 [Type: void *]
    [+0x2f0] ActiveProcessLinks [Type: _LIST_ENTRY]
```

显示使用-r 递归选项的其他信息。

```dbgcmd
0: kd> dtx -r2 HdAudio!CAzMixertopoMiniport fffff806`d24992b8
(*((HdAudio!CAzMixertopoMiniport *)0xfffff806d24992b8))                 [Type: CAzMixertopoMiniport]
    [+0x018] m_lRefCount      : -766760880 [Type: long]
    [+0x020] m_pUnknownOuter  : 0xfffff806d24dbc40 [Type: IUnknown *]
    [+0x028] m_FilterDesc     [Type: PCFILTER_DESCRIPTOR]
        [+0x000] Version          : 0xd24c2890 [Type: unsigned long]
        [+0x008] AutomationTable  : 0xfffff806d24c2780 [Type: PCAUTOMATION_TABLE *]
            [+0x000] PropertyItemSize : 0x245c8948 [Type: unsigned long]
            [+0x004] PropertyCount    : 0x6c894808 [Type: unsigned long]
            [+0x008] Properties       : 0x5718247489481024 [Type: PCPROPERTY_ITEM *]
            [+0x010] MethodItemSize   : 0x55415441 [Type: unsigned long]
            [+0x014] MethodCount      : 0x57415641 [Type: unsigned long]
            [+0x018] Methods          : 0x4ce4334540ec8348 [Type: PCMETHOD_ITEM *]
            [+0x020] EventItemSize    : 0x8b41f18b [Type: unsigned long]
            [+0x024] EventCount       : 0xd8b48f4 [Type: unsigned long]
            [+0x028] Events           : 0x7d2d8d4cfffdf854 [Type: PCEVENT_ITEM *]
            [+0x030] Reserved         : 0x66fffd79 [Type: unsigned long]
        [+0x010] PinSize          : 0xd24aa9b0 [Type: unsigned long]
        [+0x014] PinCount         : 0xfffff806 [Type: unsigned long]
        [+0x018] Pins             : 0xfffff806d24aa740 [Type: PCPIN_DESCRIPTOR *]
            [+0x000] MaxGlobalInstanceCount : 0x57555340 [Type: unsigned long]
            [+0x004] MaxFilterInstanceCount : 0x83485741 [Type: unsigned long]
            [+0x008] MinFilterInstanceCount : 0x8b4848ec [Type: unsigned long]
            [+0x010] AutomationTable  : 0xa5158b48ed33c000 [Type: PCAUTOMATION_TABLE *]
            [+0x018] KsPinDescriptor  [Type: KSPIN_DESCRIPTOR]
```

提示：使用[ **（检查符号） x** ](x--examine-symbols-.md)命令以显示感兴趣的项的地址。

```dbgcmd
0: kd> x /d HdAudio!CazMixertopoMiniport*
...
fffff806`d24992b8 HdAudio!CAzMixertopoMiniport::`vftable' = <no type information>
...
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**dt （显示类型）**](dt--display-type-.md)

 

 






