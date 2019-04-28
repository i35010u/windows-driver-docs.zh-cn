---
title: wdfkd.wdffindobjects
description: Wdfkd.wdffindobjects 扩展搜索 WDF 对象内存。
ms.assetid: 8c0a4881-9417-481b-82f8-f3510af768a1
keywords:
- wdfkd.wdffindobjects Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdffindobjects
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3c23082fc3c233d19c429ec8bc6df3277aa23094
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341716"
---
# <a name="wdfkdwdffindobjects"></a>!wdfkd.wdffindobjects


**！ Wdfkd.wdffindobjects**扩展搜索 WDF 对象内存。

```dbgcmd
!wdfkd.wdffindobjects [StartAddress [Flags]]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
可选。 指定必须开始执行搜索的地址。 如果省略此属性，从何处最多将开始搜索最近 **！ wdfkd.wdffindobjects**搜索结束。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
可选。 指定要显示信息的种类。 *标志*可以是以下位的任意组合。 默认值为 0x0。 *标志*无法使用，除非*StartAddress*指定。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
显示详细输出。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
显示内部键入每个句柄的信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架

KMDF 1，UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

下面的示例演示的输出 **！ wdfkd.wdffindobjects**扩展。 第二个示例设置了 0x1 标志。

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

 

 





