---
title: wudfext.umdevstacks
description: Wudfext. umdevstacks 扩展显示当前主机进程中所有设备堆栈的相关信息。
keywords:
- wudfext umdevstacks Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.umdevstacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2a1112ecac8c3076c32aa2c203026b947ed8e992
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794105"
---
# <a name="wudfextumdevstacks"></a>!wudfext.umdevstacks


**！ Wudfext umdevstacks** 扩展显示当前主机进程中所有设备堆栈的相关信息。

```dbgcmd
!wudfext.umdevstacks [Flags] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
可选。 指定要显示的信息的类型。 *标志* 可以是以下位的任意组合。 默认值为0x01。

<span id="Bit_0__0x01_"></span><span id="bit_0__0x01_"></span><span id="BIT_0__0X01_"></span>位 0 (0x01)   
显示有关每个设备堆栈的详细信息。

<span id="Bit_8__0x80_"></span><span id="bit_8__0x80_"></span><span id="BIT_8__0X80_"></span>位 8 (0x80)   
显示有关内部框架的信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wudfext.dll

 
### <a name="remarks"></a>备注
-------

**！ Wudfext umdevstacks** 扩展显示与每个设备堆栈关联的框架接口对象。 有关使用 **！ wudfext. umdevstacks** 的输出的详细信息，请参阅 [**！ wudfext. umdevstack**](-wudfext-umdevstack.md)。

**！ Wudfext umdevstacks** 输出包含两个名为 "对象跟踪" 和 "引用计数跟踪" 的字段。 这表明对象跟踪选项 (**TrackObjects**) 和引用计数跟踪选项 (**TrackRefCounts**) 是否已在 WDF 验证程序中启用。 如果已启用对象跟踪选项，则显示内容将包括对象跟踪器地址;此地址可传递给 [**！ wudfext**](-wudfext-wudfdumpobjects.md) 以显示跟踪信息。

下面是 **！ umdevstacks** 显示的示例 wudfext：

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


### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [用户模式驱动程序框架调试](user-mode-driver-framework-debugging.md)。
 

 





