---
title: wdfkd.wdfforwardprogress
description: Wdfkd. wdfforwardprogress 扩展显示有关指定框架队列对象的向前进度的信息。
keywords:
- wdfkd wdfforwardprogress Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfforwardprogress
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0c33065789c670a4a1809eed0d24493008c397eb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838399"
---
# <a name="wdfkdwdfforwardprogress"></a>!wdfkd.wdfforwardprogress


**！ Wdfkd wdfforwardprogress** 扩展显示有关指定框架队列对象的向前进度的信息。

```dbgcmd
!wdfkd.wdfforwardprogress Handle
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span>*句柄*   
框架队列对象的句柄。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关如何 (KMDF) 驱动程序调试 Kernel-Mode Driver Framework 的详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

仅当指定的框架队列对象配置为支持向前进度时，此扩展才会成功。 如果此扩展与其他对象一起使用，将显示一条错误消息。

下面的示例演示了 **！ wdfkd. wdfforwardprogress** 扩展中的显示。

```dbgcmd
kd> !wdfkd.wdfforwardprogress 0x79af3250 

# Dumping forward progress fields for WDFQUEUE 0x79af3250
=================================================
    ForwardProgressReservedPolicy: UseExamine (0x2)

    Total reserved requests: 44 

    Number of available reserved requests in list: 41
            !WDFREQUEST 0x7bcaf4c0 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bc67eb0 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bccf678 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bb6ce40 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7be30a58 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x79af37d0 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bc7f428 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bbd40f0 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bd333a8 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bd241d8 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bd594e0 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bd80d10 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x78ea2d50 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x792020f0 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bc37258 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bbc1fb0 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bbc4fb0 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7be0cb80 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bc84890 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x78acbd18 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bcf1ad8 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bead540 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7922c0f0 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7a34a0f0 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x625195d0 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bc33640 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bba9f28 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bba44c8 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bb77cd8 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7a2b89a8 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7a41ab88 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bc7cc88 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bd37180 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bca40f0 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x64b4af20 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bd01a40 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7a25cfb0 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bba9330 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bd14a40 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7bcc0210 (Reserved) !IRP 0x00000000
            !WDFREQUEST 0x7a54eb00 (Reserved) !IRP 0x00000000

    Number of reserved requests in use: 3
            !WDFREQUEST 0x7bf0ab80 (Reserved) !IRP 0x8438f008
            !WDFREQUEST 0x7bc53ca8 (Reserved) !IRP 0x875f59f0
            !WDFREQUEST 0x7bced8b8 (Reserved) !IRP 0x85c25348

    Number of undispatched IRP's in list: 0

    EvtIoReservedResourcesAllocate: (0x9a3f1b70) mqueue!EvtIoAllocateResourcesForReservedRequest
    EvtIoExamineIrp: (0x9a3f19d0) mqueue!EvtIoWdmIrpForForwardProgress
```

 

 





