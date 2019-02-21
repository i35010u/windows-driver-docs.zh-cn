---
title: wdfkd.wdfcrashdump
description: Wdfkd.wdfcrashdump 扩展显示错误日志信息和其他故障转储信息从一个小型转储文件，如果数据存在。
ms.assetid: 419c76b1-e291-4503-8c59-aa46140e40b3
keywords:
- wdfkd.wdfcrashdump Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfcrashdump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5de525a7ffeee84d06f2a0073f86030d6d67f1fe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542793"
---
# <a name="wdfkdwdfcrashdump"></a>!wdfkd.wdfcrashdump


**！ Wdfkd.wdfcrashdump**扩展显示错误日志信息和其他故障转储信息从一个小型转储文件，如果数据存在。

KMDF

```dbgcmd
!wdfkd.wdfcrashdump [InfoType]
```

UMDF

```dbgcmd
!wdfkd.wdfcrashdump [DriverName.dll][-d | -f | -m]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______InfoType______"></span><span id="_______infotype______"></span><span id="_______INFOTYPE______"></span> *InfoType*   
指定要显示信息的种类。 *信息类型*是可选的可以是以下值之一：

<span id="log"></span><span id="LOG"></span>**log**  
如果崩溃转储文件中可用，则显示错误日志信息。 这是默认值。

<span id="loader"></span><span id="LOADER"></span>**loader**  
显示小型转储的动态绑定驱动程序。

<span id="drivername.dll"></span><span id="DRIVERNAME.DLL"></span>*DriverName*.dll  
指定 UMDF 驱动程序的名称。 必须包含.dll 文件后缀。 如果省略此可选参数，则输出将包括元数据、 加载的模块列表中和可用日志。

<span id="-d"></span><span id="-D"></span>**-d**  
显示仅的驱动程序日志。

<span id="-f"></span><span id="-F"></span>**-f**  
显示仅的框架日志。

<span id="-m"></span><span id="-M"></span>**-m**  
合并按照记录顺序的框架和驱动程序日志。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架

KMDF

UMDF 2.15

<a name="remarks"></a>备注
-------

此示例演示如何使用 **！ wdfkd.wdfcrashdump**若要查看有关 KMDF 驱动程序的信息。 如果指定**加载程序**有关*信息类型*，输出包括小型转储文件中动态绑定驱动程序。

```dbgcmd
0: kd> !wdfcrashdump loader 
Retrieving crashdump loader information...
## Local buffer 0x002B4D00, bufferSize 720
----------------------------------------------
  ImageName      Version    FxGlobals

  Wdf01000       v1.9(6902)
  msisadrv       v1.9(6913) 0x84deb260
  vdrvroot       v1.9(6913) 0x860e8260
  storflt        v1.5(6000) 0x861dfe90
  cdrom          v1.9(6913) 0x84dca008
  intelppm       v1.9(6913) 0x864704a8
  HDAudBus       v1.7(6001) 0x86101c98
  1394ohci       v1.7(6001) 0x8610d2e8
  CompositeBus   v1.9(6913) 0x86505b98
  ObjTestClassExt v1.9(6902) 0x865b7f00
  mqfilter       v1.9(6902) 0x865b8008
  mqueue         v1.9(6902) 0x865b6910
  umbus          v1.9(6913) 0x8618aea0
  monitor        v1.9(6913) 0x86aac1d8
  PEAUTH         v1.5(6000) 0x854e5350
----------------------------------------------
```

此示例演示如何使用 **！ wdfkd.wdfcrashdump**查看 UMDF 驱动程序的信息。 如果发出 **！ wdfkd.wdfcrashdump**不带任何参数，输出将包含失败的主机进程中导致崩溃和所有已加载的驱动程序列表的驱动程序。 您可以单击此列表中具有相关联的日志的驱动程序。

```dbgcmd
0:001> !wdfkd.wdfcrashdump
Opening minidump at location C:\temp\WudfHost_ext__1312.dmp

Faulting driver: wpptest.dll
Failure type: Unhandled Exception (WUDFUnhandledException)
Faulting thread ID: 2840

Listing all drivers loaded in this host process at the time of the failure:

  ServiceName
  wpptest 
  CoverageCx0102
  coverage
  WUDFVhidmini
  ToastMon
  WUDFOsrUsbFilter
```

在上面的示例中，输出包括失败类型，它是 WER 报表中的事件类型。 在这里，它可以是**WUDFVerifierFailure**或**WUDFUnhandledException**。 有关详细信息，请参阅[WER 报表中访问 UMDF 元数据](https://msdn.microsoft.com/library/windows/hardware/ff542975)。 对于 UMDF 输出包括错误代码，如果事件类型为**WUDFVerifierFailure**。

若要显示来自框架的错误日志记录[完全内存转储](complete-memory-dump.md)即[内核内存转储](kernel-memory-dump.md)，或[实时内核模式目标](live-kernel-mode-targets.md)，还可以尝试[**！ wdfkd.wdflogdump** ](-wdfkd-wdflogdump.md)扩展。

**其他信息**

有关启用您的驱动程序的即时跟踪记录器的信息，请参阅[使用即时跟踪记录器 (IFR) KMDF 和 UMDF 2 驱动程序中](https://msdn.microsoft.com/library/windows/hardware/dn940485)。 有关调试 WDF 驱动程序的详细信息，请参阅[调试 WDF 驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff540790)。 有关 KMDF 调试信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**!wdfkd.wdflogdump**](-wdfkd-wdflogdump.md)

[**!wdfkd.wdfsettraceprefix**](-wdfkd-wdfsettraceprefix.md)

 

 






