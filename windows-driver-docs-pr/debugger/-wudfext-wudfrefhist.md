---
title: wudfext.wudfrefhist
description: Wudfext.wudfrefhist 扩展显示 UMDF 对象的引用计数堆栈历史记录。
ms.assetid: 8999f525-c6ed-4341-be2c-b0debef23a4b
keywords:
- wudfext.wudfrefhist Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfrefhist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f3bc85de50ad2a6837d620e446c69b8a45c7f87b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564246"
---
# <a name="wudfextwudfrefhist"></a>!wudfext.wudfrefhist


**！ Wudfext.wudfrefhist**扩展显示 UMDF 对象的引用计数堆栈历史记录。

```dbgcmd
!wudfext.wudfrefhist ObjectAddress
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______ObjectAddress______"></span><span id="_______objectaddress______"></span><span id="_______OBJECTADDRESS______"></span> *ObjectAddress*   
指定要显示其引用计数堆栈历史记录的 UMDF 对象的地址。 请注意，这是对象本身，而不是该接口的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wudfext.dll

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[用户模式驱动程序框架调试](user-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

**！ Wudfext.wudfrefhist** UMDF 1.11 不支持命令。

*ObjectAddress*参数必须是 UMDF 对象，不能对接口 （这使用由许多其他 UMDF 扩展命令） 的地址的地址。 若要确定 UMDF 对象的地址，请使用[ **！ wudfext.wudfdumpobjects** ](-wudfext-wudfdumpobjects.md)命令，其中显示了 UMDF 对象地址和接口地址。 或者，如果您知道接口的地址，你可以将其用作参数的[ **！ wudfext.wudfobject** ](-wudfext-wudfobject.md)命令，用于显示对象地址 (显示符号的后面"Fx:")。

如果将引用计数跟踪选项 (**TrackRefCounts**) 已启用在 WDF 验证程序，你可以使用 **！ wudfext.wudfrefhist**以显示每个调用堆栈的递增或递减的对象引用计数。 可确定调用堆栈是否通过检查导致内存泄漏其**AddRef**和**发行**调用的引用的要添加并不会释放。

在任何时候，可以使用此命令，即使 UMDF 已不中断到调试器。

如果此命令不会显示所需的信息，请确保在调时相关数据，并再试一次。

下面是使用的示例 **！ wudfext.wudfrefhist**命令：

```dbgcmd
0:007> !wudfext.umdevstacks
...
      UMDriver Image Path: C:\Windows\System32\drivers\UMDF\WUDFOsrUsbFilter.dll
      Object Tracker Address: 0x0000003792ee9fc0
        Object   Tracking ON
        Refcount Tracking ON

0:007> !wudfext.wudfdumpobjects 0x0000003792ee9fc0
...
WdfTypeIoQueue   Object: 0x0000003792f05ce0, Interface: 0x0000003792f05d58

## 0:007> !wudfext.wudfrefhist 0x0000003792f05ce0
-----------------------------------------------------------------------
## 2  (++)
-----------------------------------------------------------------------
WUDFx!UfxObject::TrackRefCounts+0xb2
WUDFx!CWdfIoQueue::AddRef+0x17adc
WUDFx!CWdfIoQueue::CreateAndInitialize+0xeb
WUDFx!CWdfDevice::CreateIoQueue+0x1e7
WUDFOsrUsbFilter!CMyQueue::Initialize+0x48
WUDFOsrUsbFilter!CMyDevice::Configure+0x7d
WUDFOsrUsbFilter!CMyDriver::OnDeviceAdd+0xca
WUDFx!CWdfDriver::OnAddDevice+0x486
WUDFx!CWUDF::AddDevice+0x43
WUDFHost!CWudfDeviceStack::LoadDrivers+0x320
WUDFHost!CLpcNotification::Message+0x1340
WUDFPlatform!WdfLpcPort::ProcessMessage+0x140
WUDFPlatform!WdfLpcCommPort::ProcessMessage+0x92
WUDFPlatform!WdfLpc::RetrieveMessage+0x20c
```

 

 





