---
title: wdfkd.wdfumdevstacks
description: Wdfkd.wdfumdevstacks 扩展隐式的过程中显示有关所有 UMDF 设备堆栈的信息。
ms.assetid: 05D09B0D-4ED8-4333-B4BC-5BE28C63312C
keywords:
- wdfkd.wdfumdevstacks Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfumdevstacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dc189f5294c8de6a1ce9d10ecff28ffdfe2ad1e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564268"
---
# <a name="wdfkdwdfumdevstacks"></a>!wdfkd.wdfumdevstacks


**！ Wdfkd.wdfumdevstacks**扩展插件都会显示有关所有 UMDF 设备堆栈中的信息[隐式过程](controlling-threads-and-processes.md)。

```dbgcmd
!wdfkd.wdfumdevstacks [Flags] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
可选。 指定要显示的信息的类型。 *标志*可以是以下位的任意组合。 默认值为 0x01。

<span id="Bit_0__0x01_"></span><span id="bit_0__0x01_"></span><span id="BIT_0__0X01_"></span>位 0 (0x01)  
显示有关每个设备堆栈的详细的信息。

<span id="Bit_7__0x80_"></span><span id="bit_7__0x80_"></span><span id="BIT_7__0X80_"></span>7 位 (0x80)  
显示内部框架有关的信息。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Wdfkd.dll

## <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架


UMDF 2

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息


有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

在内核模式调试会话中或在用户模式下调试会话附加到 UMDF 主机进程 (wudfhost.exe)，可以使用此命令。

此命令显示相同的信息作为用户模式命令[ **！ wudfext.umdevstacks**](-wudfext-umdevstacks.md)。

使用此命令之前，请使用[ **！ 过程**](-process.md)若要获取所有 UMDF 主机进程的列表。

```dbgcmd
0: kd> !process 0 0 wudfhost.exe
PROCESS ffffe00000c32900
    SessionId: 0  Cid: 079c    Peb: 7ff782537000  ParentCid: 037c
    DirBase: 607af000  ObjectTable: ffffc00009807940  HandleCount: <Data Not Accessible>
    Image: WUDFHost.exe
```

上面的输出显示是一个 UMDF 主机进程;也就是说，没有 wudfhost.exe 的一个实例。

接下来，使用[ **.process** ](-process--set-process-context-.md)到 wudfhost.exe 设置隐式的进程。

```dbgcmd
0: kd> .process /P ffffe00000c32900
Implicit process is now ffffe000`00c32900
.cache forcedecodeptes done
```

现在，使用 **！ wdfkd.wdfumdevstacks**隐式过程 (wudfhost.exe) 中显示的 UMDF 设备堆栈。

```dbgcmd
0: kd> !wdfkd.wdfumdevstacks
Number of device stacks: 1
  Device Stack: 0x000000a5a3ab5f70     Pdo Name: \Device\00000052
    Active: Yes
    Number of UM devices: 1
    Device 0
      Driver Config Registry Path: MyUmdf2Driver
      UMDriver Image Path: C:\WINDOWS\System32\drivers\UMDF\MyUmdf2Driver.dll
      FxDriver: 0xa5a3acaaa0
      FxDevice: 0xa5a3ac4fc0
      Open UM files (use !wdfumfile <addr> for details): <None>
      Device XFerMode: Deferred RW: Buffered CTL: Buffered
      DevStack XFerMode: Deferred RW: Buffered CTL: Buffered
```

上面的输出显示了隐式的过程中已有一个 UMDF 设备堆栈。 此外可以查看设备堆栈的一个设备对象 (数量的 UM 设备：1).

 

 





