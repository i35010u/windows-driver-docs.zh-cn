---
title: wdfkd.wdfinterrupt
description: Wdfkd.wdfinterrupt 扩展显示有关 WDFINTERRUPT 对象的信息。
ms.assetid: 3e032095-94fe-41d5-aeed-645d6b544105
keywords:
- wdfkd.wdfinterrupt Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfinterrupt
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 58158aead119ad37bf6eca40e4c1fabbda2e7070
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520652"
---
# <a name="wdfkdwdfinterrupt"></a>!wdfkd.wdfinterrupt


**！ Wdfkd.wdfinterrupt**扩展显示 WDFINTERRUPT 对象有关的信息。

```dbgcmd
!wdfkd.wdfinterrupt Handle [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *句柄*   
WDFINTERRUPT 对象的句柄。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
可选。 指定要显示信息的种类。 *标志*可以是以下位的任意组合。 默认值为 0x0。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
显示与此 WDFINTERRUPT 对象相关联的中断调度表 (IDT) 中断服务例程 (Isr)。 设置此标志等效于以下 **！ wdfinterrupt**扩展名[ **！ idt** ](-idt.md)扩展。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架

KMDF 1，UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

下面的示例演示的输出 **！ wdfinterrupt**位 0 设置使用的扩展*标志*参数 （因此，输出会显示有关 IDT 信息）。

```dbgcmd
kd> !wdfkd.wdfinterrupt 0x7a988698  1 

# Dumping WDFINTERRUPT 0x7a988698
=========================
  Interrupt Type: Line-based, Connected, Enabled
  Vector: 0xa1 (!idt 0xa1)
  Irql: 0x9
  Mode: LevelSensitive
  Polarity: WdfInterruptPolarityUnknown
  ShareDisposition: CmResourceShareShared
  FloatingSave: FALSE
  Interrupt Priority Policy: WdfIrqPriorityUndefined
  Processor Affinity Policy: WdfIrqPolicyOneCloseProcessor
  Processor Group: 0
  Processor Affinity: 0x3

  dt nt!KINTERRUPT 0x8594eb28

  EvtInterruptIsr: 1394ohci!Interrupt::WdfEvtInterruptIsr (0x8d580552)
  EvtInterruptDpc: 1394ohci!Interrupt::WdfEvtInterruptDpc (0x8d580682)

Dumping IDT:

a1:          85167a58 ndis!ndisMiniportIsr (KINTERRUPT 85167a00)
                                    Wdf01000!FxInterrupt::_InterruptThunk (KINTERRUPT 85987500)

To get ISR from KINTERRUPT: 
   dt <KINTERRUPT> nt!KINTERRUPT ServiceContext
   dt <ServiceContext> wdf01000!FxInterrupt m_EvtInterruptIsr
```

在前面的示例中，显示具有两个建议以结束[ **dt （显示类型）** ](dt--display-type-.md)命令，可以用于显示其他数据。

 

 





