---
title: wdfkd.wdfumdevstacks
description: Wdfkd. wdfumdevstacks 扩展显示有关隐式进程中所有 UMDF 设备堆栈的信息。
keywords:
- wdfkd wdfumdevstacks Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfumdevstacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a74e456fa38a5b0f3ccda2f3d3c19bda8ce12ae9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823633"
---
# <a name="wdfkdwdfumdevstacks"></a>!wdfkd.wdfumdevstacks


**！ Wdfkd wdfumdevstacks** 扩展显示有关 [隐式进程](controlling-threads-and-processes.md)中的所有 UMDF 设备堆栈的信息。

```dbgcmd
!wdfkd.wdfumdevstacks [Flags] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
可选。 指定要显示的信息的类型。 *标志* 可以是以下位的任意组合。 默认值为0x01。

<span id="Bit_0__0x01_"></span><span id="bit_0__0x01_"></span><span id="BIT_0__0X01_"></span>位 0 (0x01)   
显示有关每个设备堆栈的详细信息。

<span id="Bit_7__0x80_"></span><span id="bit_7__0x80_"></span><span id="BIT_7__0X80_"></span>第7位 (0x80)   
显示有关内部框架的信息。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Wdfkd.dll

## <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作


UMDF 2

## <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息


有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

可以在内核模式调试会话中或在附加到 UMDF 主机进程 ( # A0) 的用户模式调试会话中使用此命令。

此命令显示与用户模式命令 [**！ wudfext**](-wudfext-umdevstacks.md)相同的信息。

使用此命令之前，请使用 [**！进程**](-process.md) 获取所有 UMDF 主机进程的列表。

```dbgcmd
0: kd> !process 0 0 wudfhost.exe
PROCESS ffffe00000c32900
    SessionId: 0  Cid: 079c    Peb: 7ff782537000  ParentCid: 037c
    DirBase: 607af000  ObjectTable: ffffc00009807940  HandleCount: <Data Not Accessible>
    Image: WUDFHost.exe
```

前面的输出显示有一个 UMDF 主机进程;也就是说，wudfhost.exe 有一个实例。

接下来，使用 [**. 进程**](-process--set-process-context-.md) 将隐式进程设置为 wudfhost.exe。

```dbgcmd
0: kd> .process /P ffffe00000c32900
Implicit process is now ffffe000`00c32900
.cache forcedecodeptes done
```

现在，请使用 **！ wdfkd** 在隐式进程 ( # A0) 中显示 UMDF 设备堆栈。

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

前面的输出显示隐式进程中有一个 UMDF 设备堆栈。 你还可以看到设备堆栈有一个设备对象 (UM 设备的数量： 1) 。

 

 





