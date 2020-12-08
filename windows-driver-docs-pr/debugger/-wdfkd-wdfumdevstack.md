---
title: wdfkd.wdfumdevstack
description: Wdfkd. wdfumdevstack 扩展在隐式进程中显示有关 UMDF 设备堆栈的详细信息。
keywords:
- wdfkd wdfumdevstack Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfumdevstack
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 37af4c5c6e0c0ee55e7b278bcaf1b69b75553249
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823635"
---
# <a name="wdfkdwdfumdevstack"></a>!wdfkd.wdfumdevstack


**！ Wdfkd wdfumdevstack** 扩展在 [隐式进程](controlling-threads-and-processes.md)中显示有关 UMDF 设备堆栈的详细信息。

```dbgcmd
!wdfkd.wdfumdevstack DevstackAddress [Flags] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______DevstackAddress______"></span><span id="_______devstackaddress______"></span><span id="_______DEVSTACKADDRESS______"></span>*DevstackAddress*   
指定要显示其相关信息的设备堆栈的地址。 可以使用！ wdfumdevstacks 获取隐式进程中的 UMDF 设备堆栈的地址 [**wdfkd。**](-wdfkd-wdfumdevstacks.md)

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
可选。 指定要显示的信息的类型。 *标志* 可以是以下位的任意组合。 默认值为0x01。

<span id="Bit_0__0x01_"></span><span id="bit_0__0x01_"></span><span id="BIT_0__0X01_"></span>位 0 (0x01)   
显示有关设备堆栈的详细信息。

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

此命令显示与用户模式命令 [**！ wudfext**](-wudfext-umdevstack.md)相同的信息。

下面是如何使用 **！ wdfumdevstack** 的示例。 首先，使用 [**！ wdfumdevstacks**](-wdfkd-wdfumdevstacks.md) 在隐式进程中显示 UMDF 设备堆栈。

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

前面的输出显示设备堆栈 (0x000000a5a3ab5f70) 的地址。 若要获取有关设备堆栈的详细信息，请将其地址传递给 **！ wdfumdevstack**。 在此示例中，我们将 *Flags* 参数设置为0x80，以包含有关框架的信息。

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

 

 





