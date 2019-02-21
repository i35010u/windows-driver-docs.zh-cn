---
title: wdfkd.wdfumdevstack
description: Wdfkd.wdfumdevstack 扩展隐式的过程中显示有关 UMDF 设备堆栈的详细的信息。
ms.assetid: AB7F2585-B69B-4854-B8BC-438DDA735149
keywords:
- wdfkd.wdfumdevstack Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfumdevstack
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 96e5b85b11a9f4d85f2cfd5117e375406c9f0f0f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522043"
---
# <a name="wdfkdwdfumdevstack"></a>!wdfkd.wdfumdevstack


**！ Wdfkd.wdfumdevstack**扩展插件都会显示有关 UMDF 设备堆栈中的详细的信息[隐式过程](controlling-threads-and-processes.md)。

```dbgcmd
!wdfkd.wdfumdevstack DevstackAddress [Flags] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______DevstackAddress______"></span><span id="_______devstackaddress______"></span><span id="_______DEVSTACKADDRESS______"></span> *DevstackAddress*   
指定要显示有关的信息的设备堆栈的地址。 可以使用[ **！ wdfkd.wdfumdevstacks** ](-wdfkd-wdfumdevstacks.md)隐式的过程中获取的 UMDF 设备堆栈的地址。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
可选。 指定要显示的信息的类型。 *标志*可以是以下位的任意组合。 默认值为 0x01。

<span id="Bit_0__0x01_"></span><span id="bit_0__0x01_"></span><span id="BIT_0__0X01_"></span>位 0 (0x01)  
显示有关设备堆栈的详细的信息。

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

此命令显示相同的信息作为用户模式命令[ **！ wudfext.umdevstack**](-wudfext-umdevstack.md)。

下面是如何使用的示例 **！ wdfumdevstack**。 首先，使用[ **！ wdfumdevstacks** ](-wdfkd-wdfumdevstacks.md)隐式的过程中显示的 UMDF 设备堆栈。

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

上面的输出显示设备堆栈 (0x000000a5a3ab5f70) 的地址。 若要获取有关设备堆栈的详细的信息，请将传递到其地址 **！ wdfumdevstack**。 在此示例中，我们将设置*标志*0x80 以包括有关框架的信息的参数。

```dbgcmd
0: kd> !wdfkd.wdfumdevstack 0x000000a5a3ab5f70 0x80
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
      Internal Values:
        wudfhost!WudfDriverAndFxInfo 0x000000a5a3ac21b8
        IUMDFramework: 0x0000000000000000
        IFxMessageDispatch: 0x000000a5a3aba630
        FxDevice 0x000000a5a3ac4fc0
        Modules:
          Driver: wudfhost!CWudfModuleInfo 0x000000a5a3ac18f0
          Fx:     wudfhost!CWudfModuleInfo 0x000000a5a3aca7a0
          wudfx02000!FxDriver: 0x000000a5a3acaaa0
      DevStack XFerMode: Deferred RW: Buffered CTL: Buffered
```

 

 





