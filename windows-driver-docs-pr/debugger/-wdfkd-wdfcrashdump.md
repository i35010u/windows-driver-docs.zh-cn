---
title: wdfkd.wdfcrashdump
description: 如果数据存在，wdfcrashdump 扩展将显示小型转储文件中的错误日志信息和其他故障转储信息。
keywords:
- wdfkd wdfcrashdump Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfcrashdump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d95629d88512115a517b4fa46b233cc0c3849283
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814641"
---
# <a name="wdfkdwdfcrashdump"></a>!wdfkd.wdfcrashdump


如果数据存在，则 **！ wdfkd wdfcrashdump** 扩展会显示小型转储文件中的错误日志信息和其他故障转储信息。

KMDF

```dbgcmd
!wdfkd.wdfcrashdump [InfoType]
```

UMDF

```dbgcmd
!wdfkd.wdfcrashdump [DriverName.dll][-d | -f | -m]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______InfoType______"></span><span id="_______infotype______"></span><span id="_______INFOTYPE______"></span>*InfoType*   
指定要显示的信息的类型。 *InfoType* 是可选的，可以是下列值之一：

<span id="log"></span><span id="LOG"></span>**日志**  
如果在崩溃转储文件中可用，则显示错误日志信息。 这是默认值。

<span id="loader"></span><span id="LOADER"></span>**引导**  
显示小型转储的动态绑定驱动程序。

<span id="drivername.dll"></span><span id="DRIVERNAME.DLL"></span>*DriverName*  
指定 UMDF 驱动程序的名称。 必须包含 .dll 文件后缀。 如果省略此可选参数，则输出将包含元数据、已加载的模块列表和可用日志。

<span id="-d"></span><span id="-D"></span>**-d.ddd...e**  
仅显示驱动程序日志。

<span id="-f"></span><span id="-F"></span>**-f**  
只显示框架日志。

<span id="-m"></span><span id="-M"></span>**-m**  
将框架和驱动程序日志合并为其记录的顺序。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF

UMDF 2.15

<a name="remarks"></a>备注
-------

此示例演示如何使用 **！ wdfkd** 来查看有关 KMDF 驱动程序的信息。 如果为 *InfoType* 指定 **加载程序**，则输出将在小型转储文件中包含动态绑定的驱动程序。

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

此示例演示如何使用 **！ wdfkd** 来查看有关 UMDF 驱动程序的信息。 如果你在没有参数的情况下发出 **！ wdfkd** ，则输出将包括导致崩溃的驱动程序，以及主机进程中失败的所有已加载驱动程序的列表。 你可以单击此列表中具有关联日志的驱动程序。

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

在上面的示例中，输出包括故障类型，即 WER 报告中的事件类型。 此处可以是 **WUDFVerifierFailure** 或 **WUDFUnhandledException**。 有关详细信息，请参阅 [在 WER 报表中访问 UMDF 元数据](../wdf/accessing-umdf-metadata-in-wer-reports.md)。 如果事件类型为 **WUDFVerifierFailure**，则 UMDF 的输出包含错误代码。

若要显示 [完整内存转储](complete-memory-dump.md)、 [内核内存转储](kernel-memory-dump.md)或 [实时内核模式目标](live-kernel-mode-targets.md)中框架的错误日志记录，你还可以尝试 [**！ wdfkd**](-wdfkd-wdflogdump.md) 扩展名。

**其他信息**

有关为驱动程序启用即时跟踪记录器的信息，请参阅 [使用即时 Trace 录像机 (IFR) 在 KMDF 和 UMDF 2 驱动程序中](../wdf/using-wpp-software-tracing-in-kmdf-and-umdf-2-drivers.md)。 有关调试 WDF 驱动程序的详细信息，请参阅 [调试 Wdf 驱动程序](./debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)。 有关 KMDF 调试的信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**!wdfkd.wdflogdump**](-wdfkd-wdflogdump.md)

[**!wdfkd.wdfsettraceprefix**](-wdfkd-wdfsettraceprefix.md)

