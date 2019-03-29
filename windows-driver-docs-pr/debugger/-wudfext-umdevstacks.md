---
title: wudfext.umdevstacks
description: Wudfext.umdevstacks 扩展显示当前的主机进程中的所有设备堆栈有关的信息。
ms.assetid: e69420fc-97b8-420f-b635-bee41fbf4586
keywords:
- wudfext.umdevstacks Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.umdevstacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 36d9a0b21a0966a740ceff55acac81017a4afa44
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564229"
---
# <a name="wudfextumdevstacks"></a>!wudfext.umdevstacks


**！ Wudfext.umdevstacks**扩展当前的主机进程中显示所有设备堆栈有关的信息。

```dbgcmd
!wudfext.umdevstacks [Flags] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
可选。 指定要显示的信息的类型。 *标志*可以是以下位的任意组合。 默认值为 0x01。

<span id="Bit_0__0x01_"></span><span id="bit_0__0x01_"></span><span id="BIT_0__0X01_"></span>位 0 (0x01)  
显示有关每个设备堆栈的详细的信息。

<span id="Bit_8__0x80_"></span><span id="bit_8__0x80_"></span><span id="BIT_8__0X80_"></span>8 位 (0x80)  
显示内部框架有关的信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wudfext.dll

 
### <a name="remarks"></a>备注
-------

**！ Wudfext.umdevstacks**扩展显示与每个设备堆栈关联的框架接口对象。 有关使用的输出详细信息 **！ wudfext.umdevstacks**，请参阅[ **！ wudfext.umdevstack**](-wudfext-umdevstack.md)。

**！ Wudfext.umdevstacks**输出包括名为"跟踪对象"和"引用计数跟踪"的两个字段。 这些指示是否跟踪选项的对象 (**TrackObjects**) 和跟踪选项的引用计数 (**TrackRefCounts**) 分别在 WDF 验证程序已启用。 如果已启用跟踪选项的对象，显示内容包括对象跟踪器地址;此地址可以传递给[ **！ wudfext.wudfdumpobjects** ](-wudfext-wudfdumpobjects.md)显示跟踪信息。

下面是举例 **！ wudfext.umdevstacks**显示：

```dbgcmd
0: kd> !umdevstacks 
Number of device stacks: 1
  Device Stack: 0x038c6f08    Pdo Name: \Device\USBPDO-11
    Number of UM devices: 1
    Device 0
      Driver Config Registry Path: WUDFOsrUsbFx2
      UMDriver Image Path: D:\Windows\system32\DRIVERS\UMDF\WUDFOsrUsbFx2.dll
      Fx Driver: IWDFDriver 0x3076ff0
      Fx Device: IWDFDevice 0x3082e70
        IDriverEntry: WUDFOsrUsbFx2!CMyDriver 0x0306eff8
      Open UM files (use !umfile <addr> for details): 
        0x04a8ef84
      Device XFerMode: CopyImmediately RW: Buffered CTL: Buffered
      Object Tracker Address: 0x03074fd8
        Object   Tracking ON
        Refcount Tracking OFF
    DevStack XFerMode: CopyImmediately RW: Buffered CTL: Buffered
```


### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[用户模式驱动程序框架调试](user-mode-driver-framework-debugging.md)。
 

 





