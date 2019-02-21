---
title: wudfext.wudfobject
description: Wudfext.wudfobject 扩展显示的 WDF 对象，其父级和子级关系有关的信息。
ms.assetid: cb9398fb-24f5-4692-9a08-543bf1317b19
keywords:
- wudfext.wudfobject Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfobject
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 10c5d683983efa900cb14cc5e0ac4f813357c59c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540954"
---
# <a name="wudfextwudfobject"></a>!wudfext.wudfobject


**！ Wudfext.wudfobject**扩展插件都会显示一个 WDF 对象，其父级和子级关系有关的信息。

```dbgcmd
!wudfext.wudfobject pWDFObject Flags TypeName
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______pWDFObject______"></span><span id="_______pwdfobject______"></span><span id="_______PWDFOBJECT______"></span> *pWDFObject*   
指定要显示有关的信息的 WDF 接口的地址。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
可选。 指定要显示的信息的类型。 *标志*可以是以下位的任意组合。 默认值为 0x01。

<span id="Bit_0__0x01_"></span><span id="bit_0__0x01_"></span><span id="BIT_0__0X01_"></span>位 0 (0x01)  
若要获取的父和子关系，将显示在对象层次结构的步骤以递归方式。

<span id="Bit_1__0x02_"></span><span id="bit_1__0x02_"></span><span id="BIT_1__0X02_"></span>位 1 (0x02)  
显示有关对象的摘要信息。

<span id="Bit_8__0x80_"></span><span id="bit_8__0x80_"></span><span id="BIT_8__0X80_"></span>8 位 (0x80)  
步骤以递归方式通过对象层次结构，并显示有关内部框架的详细信息。

<span id="_______TypeName______"></span><span id="_______typename______"></span><span id="_______TYPENAME______"></span> *TypeName*   
可选。 指定的接口类型 (例如， **IWDFDevice**)。 如果为值*TypeName*是提供，该扩展使用的值作为接口的类型。 如果星号 (\*) 作为提供*TypeName*，或者如果*TypeName*是省略，该扩展会尝试自动确定提供的接口的类型。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Wudfext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[用户模式驱动程序框架调试](user-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

可以使用 **！ wudfext.wudfobject**若要列出，例如，子对象的**IWDFDevice**对象，通常包括设备的队列。

此外可以使用 **！ wudfext.wudfobject**查找与特定设备，若要检查的状态 （例如，WDF 对象是否在过程中删除），一个 WDF 对象，或确定 WDF 相关联的 WDF 对象对象的当前引用计数。

**！ Wudfext.wudfobject**扩展还显示的回调函数和上下文对象与每个框架对象并尝试确定 framework 对象的类型相关联，驱动程序。 最后一种功能可能无法使用某些编译器。

以下是一些示例。 在第一个示例中， [ **！ wudfext.umdevstacks** ](-wudfext-umdevstack.md)设备对象的地址，此地址随后将传递到可让 0x03050E70 **！ wudfext.wudfobject**。 0x1 标志是包括在内，以显示该对象的所有子级。

```dbgcmd
0: kd> !umdevstacks 
Number of device stacks: 1
  Device Stack: 0x038f6f08    Pdo Name: \Device\USBPDO-11
    Number of UM devices: 1
    Device 0
      Driver Config Registry Path: WUDFOsrUsbFx2
      UMDriver Image Path: D:\Windows\system32\DRIVERS\UMDF\WUDFOsrUsbFx2.dll
      Fx Driver: IWDFDriver 0x3044ff0
      Fx Device: IWDFDevice 0x3050e70
        IDriverEntry: WUDFOsrUsbFx2!CMyDriver 0x0303eff8
      Open UM files (use !umfile <addr> for details): 
        0x049baf84
      Device XFerMode: CopyImmediately RW: Buffered CTL: Buffered
      Object Tracker Address: 0x00000000
        Object   Tracking OFF
        Refcount Tracking OFF
    DevStack XFerMode: CopyImmediately RW: Buffered CTL: Buffered

0: kd> !wudfobject 0x3050e70 1 
IWDFDevice 0x3050e70 Fx: 0x3050e30 [Ref 2]
  15 Children
    00: IWDFIoTarget 0x3056f90 Fx: 0x3056f50 [Ref 3]
        No Children
    01: <Internal>
    02: <Internal>
    03: <Internal>
    04: IWDFIoQueue 0x305ae98 Fx: 0x305ae58 [Ref 8]
        No Children
    05: IWDFIoQueue 0x305ee98 Fx: 0x305ee58 [Ref 2]
        No Children
    06: IWDFIoQueue 0x3060e98 Fx: 0x3060e58 [Ref 2]
        No Children
    07: IWDFIoTarget 0x3066f80 Fx: 0x3066f40 [Ref 2]
        1 Children
          00: IWDFUsbInterface 0x306efd8 Fx: 0x306ef98 [Ref 1]
              3 Children
                00: IWDFIoTarget 0x3074f70 Fx: 0x3074f30 [Ref 2]
                    2 Children
                      00: IWDFMemory 0x30a4ff0 Fx: 0x30a4fb0 [Ref 2]
                          No Children
                      01: IWDFMemory 0x30aaff0 Fx: 0x30aafb0 [Ref 2]
                          No Children
                01: IWDFIoTarget 0x3078f70 Fx: 0x3078f30 [Ref 1]
                    No Children
```

下面是举例 **！ wudfext.wudfobject**显示文件对象：

```dbgcmd
kd> !wudfobject 0xf5060 
IWDFFile 0xf5060 Fx: 0xf4fe8 [Ref 1]
  State: Created   Parent: 0xf2f80
  No Children
```

下面是举例 **！ wudfext.wudfobject**显示驱动程序对象：

```dbgcmd
kd> !wudfobject 0xf2db8 0x01 
IWDFDriver 0xf2db8 Fx: 0xf2d40 [Ref 2]
  Callback: (WUDFEchoDriver!CMyDriver, 0xf2c68)
  State: Created   Parent: 0
  1 Children:
    00: IWDFDevice 0xf2f80 Fx: 0xf2f08 [Ref 2]
        State: Created   Parent: 0xf2db8
        5 Children:
          00: IWDFIoTarget 0xf33c0 Fx: 0xf3348 [Ref 3]
              State: Created   Parent: 0xf2f80
              No Children
          01: IWDFIoQueue 0xf3500 Fx: 0xf3488 [Ref 3]
              State: Created   Parent: 0xf2f80
              No Children
          02: IWDFFile 0xf5060 Fx: 0xf4fe8 [Ref 1]
              State: Created   Parent: 0xf2f80
              No Children
          03: IWDFFile 0xf5100 Fx: 0xf5088 [Ref 101]
              State: Created   Parent: 0xf2f80
              No Children
          04: IWDFFile 0xf51a0 Fx: 0xf5128 [Ref 101]
              State: Created   Parent: 0xf2f80
              No Children
```

 

 





