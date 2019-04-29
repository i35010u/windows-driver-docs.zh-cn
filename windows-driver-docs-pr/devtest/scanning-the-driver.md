---
title: 扫描驱动程序
description: 扫描驱动程序
ms.assetid: c36960b4-d97e-49b7-a7ad-e71b0820db8a
keywords:
- 静态驱动程序验证程序 WDK DriverEntry 例程会扫描
- StaticDV WDK DriverEntry 例程会扫描
- SDV WDK DriverEntry 例程会扫描
- 扫描 DriverEntry 例程 WDK Static Driver Verifier
- 驱动程序入口点 WDK Static Driver Verifier
- 入口点 WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9953e67c8242108d74aeeac2afc44be80ee3518a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340205"
---
# <a name="scanning-the-driver"></a>扫描驱动程序


驱动程序使用扫描 **/扫描**命令选项是可选的。 如果你不执行操作之前验证您的驱动程序进行扫描，SDV 扫描函数角色类型声明，并验证该驱动程序时创建的 Sdv map.h 文件。

此扫描期间 SDV 尝试检测它需要验证该驱动程序的驱动程序入口点。 它在 Sdv map.h，它在驱动程序源目录中创建的文件中记录扫描的结果。

但是，它是非常重要，在扫描步骤完成之后或验证，以确保 SDV 已检测到正确的入口点之后查看此文件。 如果入口点缺少或错误，请验证可能是不可靠的。 更重要的是，如果 SDV 无法检测到任何入口点，它无法验证该驱动程序。 

只需一次扫描的每个驱动程序。 此后，SDV 保留 Sdv map.h 文件进行验证的驱动程序。

### <a name="span-idexaminethesdvmaphfilespanspan-idexaminethesdvmaphfilespanexamine-the-sdv-maph-file"></a><span id="examine_the_sdv_map_h_file"></span><span id="EXAMINE_THE_SDV_MAP_H_FILE"></span>检查 Sdv map.h 文件

运行扫描命令或验证该驱动程序之后, 打开 Sdv map.h 文件并检查该文件。 Sdv map.h 是带格式的文本文件。 您可以阅读其任何文本编辑器，如记事本。

比较您的驱动程序与函数声明的角色类型的 Sdv map.h 文件的内容。 检查以查看驱动程序的回调或调度例程已正确识别的 Sdv map.h 文件的内容。

Sdv map.h 文件不需要列出所有驱动程序; 中的入口点只能 IRP 主要函数代码或分析中使用的函数角色类型的入口点。 不要添加任何 IRP 主要函数代码或函数的角色类型到该文件。

Sdv map.h 文件有关的详细信息，请参阅[Sdv map.h](sdv-map-h.md)。 格式中所述[Sdv map.h 文件的格式](format-of-the-sdv-map-h-file.md)。 可以在 Sdv map.h 文件中出现的错误进行了介绍[批准 Sdv map.h 文件](approving-the-sdv-map-h-file.md)。

下面的示例显示的 Sdv map.h 文件中的内容失效\_driver1，工具中的一个示例 WDM 驱动程序\\sdv\\示例\\失败\_驱动程序\\wdm 目录。

```
//Approved=false
//DriverAddDevice
#define fun_AddDevice DriverAddDevice
//DriverEntry
#define fun_DriverEntry DriverEntry
//DriverUnload
#define fun_DriverUnload DriverUnload
//CompletionRoutine
#define fun_IO_COMPLETION_ROUTINE_1 CompletionRoutine
//DpcForIsrRoutine
#define fun_IO_DPC_ROUTINE_1 DpcForIsrRoutine
//DispatchCreate
#define fun_IRP_MJ_CREATE DispatchCreate
//DispatchPnp
#define fun_IRP_MJ_PNP DispatchPnp
//DispatchPower
#define fun_IRP_MJ_POWER DispatchPower
//DispatchRead
#define fun_IRP_MJ_READ DispatchRead
//DispatchSystemControl
#define fun_IRP_MJ_SYSTEM_CONTROL DispatchSystemControl
//InterruptServiceRoutine
#define fun_KSERVICE_ROUTINE_1 InterruptServiceRoutine
```

### <a name="span-idcorrectthesdvmaphfilespanspan-idcorrectthesdvmaphfilespancorrect-the-sdv-maph-file"></a><span id="correct_the_sdv_map_h_file"></span><span id="CORRECT_THE_SDV_MAP_H_FILE"></span>更正 Sdv map.h 文件

验证驱动程序之前，请更正 Sdv map.h 文件中的任何错误。 SDV 将验证驱动程序，即使 Sdv map.h 文件不正确或不批准，但验证的结果可能不可靠。 例如，如果不使用相应的函数角色类型中声明的驱动程序调度或回调例程，驱动程序例程不会在 Sdv map.h 文件中。 因此，你可能会看因为 SDV 即使验证的一部分指定这些规则会考虑不适用时使用函数角色类型的规则在代码中发现缺陷。

若要更正的 Sdv map.h 文件，请确保您的驱动程序调度或回调例程通过使用相应的功能角色类型声明。 然后重新扫描该驱动程序，并验证它们出现在 Sdv map.h 文件...

### <a name="span-idapprovethesdvmaphfilespanspan-idapprovethesdvmaphfilespanapprove-the-sdv-maph-file"></a><span id="approve_the_sdv_map_h_file"></span><span id="APPROVE_THE_SDV_MAP_H_FILE"></span>审批 Sdv map.h 文件

确定 Sdv map.h 文件正确之后，您可以批准该文件。 如果不未对文件进行任何更改，您不需要批准它。

SDV 将验证驱动程序，即使未批准的 Sdv map.h 文件。

若要批准的 Sdv map.h 文件，该文件，在第一行更改：

```
//Approved=false
```

至：

```
//Approved=true
```

只需批准的 Sdv map.h 文件一次的每个驱动程序。 此后，SDV 保留已批准的 Sdv map.h 文件进行验证的驱动程序。 如果你想 SDV 来扫描你的源代码再次为函数角色类型声明，只需删除该文件。

下面的示例演示对于 KMDF 示例驱动程序，已批准的 Sdv map.h 文件失败\_Driver1。 SDV 使用 Sdv map.h 文件映射使用 SDV 验证所需的函数角色类型的驱动程序的声明的回调函数。

```
//Approved=true
//DriverEntry
#define fun_DriverEntry DriverEntry
//EvtDriverDeviceAdd
#define fun_WDF_DRIVER_DEVICE_ADD EvtDriverDeviceAdd
//EvtIoDeviceControl
#define fun_WDF_IO_QUEUE_IO_DEVICE_CONTROL EvtIoDeviceControl
//EvtIoInternalDeviceControl
#define fun_WDF_IO_QUEUE_IO_INTERNAL_DEVICE_CONTROL EvtIoInternalDeviceControl
//EvtIoRead
#define fun_WDF_IO_QUEUE_IO_READ EvtIoRead
//EvtRequestCancel
#define fun_WDF_REQUEST_CANCEL_1 EvtRequestCancel
```

 

 





