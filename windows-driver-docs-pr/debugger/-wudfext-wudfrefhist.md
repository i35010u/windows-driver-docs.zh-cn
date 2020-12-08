---
title: wudfext.wudfrefhist
description: Wudfext. wudfrefhist 扩展显示 UMDF 对象的引用计数堆栈历史记录。
keywords:
- wudfext wudfrefhist Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfrefhist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b8817cffec9643dd18cc89978ce827d75a3ff1b3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824379"
---
# <a name="wudfextwudfrefhist"></a>!wudfext.wudfrefhist


**！ Wudfext wudfrefhist** 扩展显示 UMDF 对象的引用计数堆栈历史记录。

```dbgcmd
!wudfext.wudfrefhist ObjectAddress
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______ObjectAddress______"></span><span id="_______objectaddress______"></span><span id="_______OBJECTADDRESS______"></span>*ObjectAddress*   
指定要显示其引用计数堆栈历史记录的 UMDF 对象的地址。 请注意，这是对象本身的地址，而不是接口的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wudfext.dll

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [用户模式驱动程序框架调试](user-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

UMDF 1.11 不支持 **！ wudfext. wudfrefhist** 命令。

*ObjectAddress* 参数必须是 UMDF 对象的地址，而不能是接口的地址 (此接口由许多其他) 的 UMDF 扩展命令使用。 若要确定 UMDF 对象的地址，请使用 [**！ wudfext. wudfdumpobjects**](-wudfext-wudfdumpobjects.md) 命令，该命令显示 umdf 对象地址和接口地址。 或者，如果知道接口的地址，则可以将其用作 [**！ wudfobject**](-wudfext-wudfobject.md) 命令的参数，该命令显示 (符号 "Fx：" ) 后显示的对象地址。

如果已在 WDF 验证程序中启用了引用计数跟踪选项 (**TrackRefCounts**) ，则可以使用 **！ wudfext wudfrefhist** 显示每个调用堆栈，该堆栈递增或递减对象的引用计数。 您可以通过检查其 **AddRef** 和 **Release** 调用以查找正在添加但不释放的引用来确定调用堆栈是否导致内存泄露。

即使 UMDF 未在调试器中出现，也可以随时使用此命令。

如果此命令未显示所需的信息，请确保将相关数据分页，然后重试。

下面是使用 **！ wudfext. wudfrefhist** 命令的示例：

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

 

 





