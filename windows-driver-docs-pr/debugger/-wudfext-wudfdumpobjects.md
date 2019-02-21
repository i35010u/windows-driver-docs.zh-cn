---
title: wudfext.wudfdumpobjects
description: Wudfext.wudfdumpobjects 扩展显示未完成的 UMDF 对象。
ms.assetid: 2ede7f2e-124c-494d-9188-5a28617a0bdb
keywords:
- wudfext.wudfdumpobjects Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfdumpobjects
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3aab71a2c315c9e5bd798a8fe0c7978cb11f9615
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533833"
---
# <a name="wudfextwudfdumpobjects"></a>!wudfext.wudfdumpobjects


**！ Wudfext.wudfdumpobjects**扩展显示未完成的 UMDF 对象。

```dbgcmd
!wudfext.wudfdumpobjects ObjTrackerAddress
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______ObjTrackerAddress______"></span><span id="_______objtrackeraddress______"></span><span id="_______OBJTRACKERADDRESS______"></span> *ObjTrackerAddress*   
指定要跟踪泄漏的对象的地址。 当发生了泄漏时，此地址显示在调试器中的驱动程序停止消息。

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
<td align="left"><p><strong>使用 UMDF 1.7 和更高版本的 Windows XP</strong></p></td>
<td align="left"><p>Wudfext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[用户模式驱动程序框架调试](user-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

如果 UMDF 对象跟踪选项 (**TrackObjects**) 已启用在 WDF 验证程序，你可以使用 **！ wudfext.wudfdumpobjects**若要查看任何泄漏驱动程序卸载后保留的对象。

如果**TrackObjects**启用选项，当检测到泄漏时，将自动显示对象跟踪器的地址。 将此地址用作*ObjTrackerAddress*执行时 **！ wudfext.wudfdumpobjects**。

可以在任何时候，使用此扩展，即使 UMDF 已不中断到调试器。

如果 UMDF 为 1.9 版或更高版本，你可以使用[ **！ wudfext.umdevstack** ](-wudfext-umdevstack.md)或[ **！ wudfext.umdevstacks** ](-wudfext-umdevstacks.md)来确定的地址对象跟踪器。 然后可以将此地址传递给 **！ wudfext.wudfdumpobjects**。 下面是一个示例：

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

0: kd> !wudfdumpobjects 0x03074fd8 
WdfTypeDriver    Object: 0x03076fb0, Interface: 0x03076ff0
WdfTypeDevice   Object: 0x03082e30, Interface: 0x03082e70
WdfTypeIoTarget Object: 0x03088f50, Interface: 0x03088f90
WdfTypeIoQueue                Object: 0x0308ce58, Interface: 0x0308ce98
WdfTypeIoQueue                Object: 0x03090e58, Interface: 0x03090e98
WdfTypeIoQueue                Object: 0x03092e58, Interface: 0x03092e98
WdfTypeIoTarget Object: 0x03098f40, Interface: 0x03098f80
WdfTypeFile         Object: 0x0309cfa0, Interface: 0x0309cfe0
WdfTypeUsbInterface         Object: 0x030a0f98, Interface: 0x030a0fd8
WdfTypeRequest Object: 0x030a2ef8, Interface: 0x030a2f38
WdfTypeIoTarget Object: 0x030a6f30, Interface: 0x030a6f70
WdfTypeIoTarget Object: 0x030aaf30, Interface: 0x030aaf70
WdfTypeIoTarget Object: 0x030aef30, Interface: 0x030aef70
WdfTypeRequest Object: 0x030c6ef8, Interface: 0x030c6f38
WdfTypeRequest Object: 0x030ceef8, Interface: 0x030cef38
WdfTypeMemoryObject    Object: 0x030d6fb0, Interface: 0x030d6ff0
WdfTypeMemoryObject    Object: 0x030dcfb0, Interface: 0x030dcff0
WdfTypeFile         Object: 0x030e4fa8, Interface: 0x030e4fe8
WdfTypeFile         Object: 0x030e6fa8, Interface: 0x030e6fe8
WdfTypeFile         Object: 0x030e8fa8, Interface: 0x030e8fe8
WdfTypeRequest Object: 0x030eaef8, Interface: 0x030eaf38
WdfTypeMemoryObject    Object: 0x030ecfb0, Interface: 0x030ecff0
WdfTypeMemoryObject    Object: 0x030eefb0, Interface: 0x030eeff0
```

 

 





