---
title: wdfkd.wdffindobjects
description: Wdfkd. wdffindobjects 扩展会搜索 WDF 对象的内存。
keywords:
- wdfkd wdffindobjects Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdffindobjects
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b27f46da11eb7c40c7d5f4a9c7e156d1253b54e0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834789"
---
# <a name="wdfkdwdffindobjects"></a>!wdfkd.wdffindobjects


**！ Wdfkd wdffindobjects** 扩展会搜索 WDF 对象的内存。

```dbgcmd
!wdfkd.wdffindobjects [StartAddress [Flags]]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span>*StartAddress*   
可选。 指定必须开始进行搜索的地址。 如果省略此条件，搜索将从最近的 **！ wdfkd** 搜索结束的位置开始。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
可选。 指定要显示的信息的类型。 *标志* 可以是以下位的任意组合。 默认值为0x0。 除非指定 *StartAddress* ，否则不能使用 *Flags* 。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
显示详细输出。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)   
显示每个句柄的内部类型信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1，UMDF 2

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

下面的示例显示 **！ wdfkd. wdffindobjects** 扩展的输出。 在第二个示例中设置了0x1 标志。

```dbgcmd
1: kd> !wdffindobjects 0xfffffa600211b668 
  Address             Value               Object
  ------------------  ------------------  ------------------
  0xfffffa600211b668  0x0000000000000008  
  0xfffffa600211b670  0xfffffa8002e7b1f0  !WDFREQUEST 0x0000057ffd184e08
  0xfffffa600211b678  0x0000000000000004  
  0xfffffa600211b680  0x0000000000000001  
  0xfffffa600211b688  0xfffffa8006aa3640  !WDFUSBPIPE 0x0000057ff955c9b8
  0xfffffa600211b690  0x0000000000000000  
  0xfffffa600211b698  0xfffff80001e61f78  
  0xfffffa600211b6a0  0x0000000000000010  
  0xfffffa600211b6a8  0x0000000000010286  
  0xfffffa600211b6b0  0xfffffa600211b6c0  
  0xfffffa600211b6b8  0x0000000000000000  
  0xfffffa600211b6c0  0xfffffa8006aa3640  !WDFUSBPIPE 0x0000057ff955c9b8
  0xfffffa600211b6c8  0x0000057ffd184e08  !WDFREQUEST 0x0000057ffd184e08
  0xfffffa600211b6d0  0x0000000000000000  
  0xfffffa600211b6d8  0x0000057ffc51ea18  !WDFMEMORY 0x0000057ffc51ea18
  0xfffffa600211b6e0  0x0000000000000000  

1: kd> !wdffindobjects 0xfffffa600211b668 1 
  Address             Value               Type    Object
  ------------------  ------------------  ------  ------------------
  0xfffffa600211b668  0x0000000000000008  
  0xfffffa600211b670  0xfffffa8002e7b1f0  Object  !WDFREQUEST 0x0000057ffd184e08
  0xfffffa600211b678  0x0000000000000004  
  0xfffffa600211b680  0x0000000000000001  
  0xfffffa600211b688  0xfffffa8006aa3640  Object  !WDFUSBPIPE 0x0000057ff955c9b8
  0xfffffa600211b690  0x0000000000000000  
  0xfffffa600211b698  0xfffff80001e61f78  
  0xfffffa600211b6a0  0x0000000000000010  
  0xfffffa600211b6a8  0x0000000000010286  
  0xfffffa600211b6b0  0xfffffa600211b6c0  
  0xfffffa600211b6b8  0x0000000000000000  
  0xfffffa600211b6c0  0xfffffa8006aa3640  Object  !WDFUSBPIPE 0x0000057ff955c9b8
  0xfffffa600211b6c8  0x0000057ffd184e08  Handle  !WDFREQUEST 0x0000057ffd184e08
  0xfffffa600211b6d0  0x0000000000000000  
  0xfffffa600211b6d8  0x0000057ffc51ea18  Handle  !WDFMEMORY 0x0000057ffc51ea18
  0xfffffa600211b6e0  0x0000000000000000  
```

 

 





