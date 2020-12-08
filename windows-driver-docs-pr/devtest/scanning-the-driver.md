---
title: 扫描驱动程序
description: 扫描驱动程序
keywords:
- 静态驱动程序验证程序 WDK，DriverEntry 例程扫描
- StaticDV WDK，DriverEntry 例程扫描
- SDV WDK，DriverEntry 例程扫描
- 扫描 DriverEntry 例程 WDK 静态驱动程序验证程序
- 驱动程序入口点 WDK 静态驱动程序验证程序
- 入口点 WDK 静态驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c43c42aecf36f93ec2e953ed2f9b41d666c5a75f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838329"
---
# <a name="scanning-the-driver"></a>扫描驱动程序


使用 **/scan** 命令选项扫描驱动程序是可选的。 如果在验证驱动程序之前未扫描，SDV 会扫描函数角色类型声明，并在验证驱动程序时创建 Sdv 文件。

在此扫描过程中，SDV 将尝试检测到需要验证驱动程序的驱动程序入口点。 它将扫描结果记录在 Sdv 中，它是在驱动程序的源目录中创建的文件。

但是，在扫描步骤或验证后查看此文件非常重要，以确保 SDV 检测到正确的入口点。 如果入口点丢失或错误，则验证可能不可靠。 更重要的是，如果 SDV 无法检测到任何入口点，它将无法验证该驱动程序。 

对于每个驱动程序，只需扫描一次。 此后，SDV 将保留驱动程序的 Sdv 文件，以便以后进行验证。

### <a name="span-idexamine_the_sdv_map_h_filespanspan-idexamine_the_sdv_map_h_filespanexamine-the-sdv-maph-file"></a><span id="examine_the_sdv_map_h_file"></span><span id="EXAMINE_THE_SDV_MAP_H_FILE"></span>检查 Sdv-map .h 文件

运行扫描命令或验证驱动程序后，打开 Sdv 文件并检查文件。 Sdv 是格式化的文本文件。 可以在任何文本编辑器（例如记事本）中读取它。

将 Sdv 文件的内容与你的驱动程序的已声明函数角色类型进行比较。 检查 Sdv 文件的内容，以查看是否已正确确定驱动程序的回调或调度例程。

不需要 Sdv 文件来列出驱动程序中的所有入口点;只有 IRP 主要功能代码的入口点或分析中使用的函数角色类型。 不要将任何 IRP 主要函数代码或函数角色类型添加到该文件。

有关 Sdv 文件的详细信息，请参阅 [Sdv](sdv-map-h.md)。 格式在 [Sdv 文件的格式](format-of-the-sdv-map-h-file.md)中进行了描述。 Sdv 文件中可能会出现的错误在 [批准 Sdv 文件](approving-the-sdv-map-h-file.md)中进行了介绍。

下面的示例显示 Sdv-map .h 文件的内容，该文件来自 Fail \_ driver1，这是 tools \\ Sdv \\ samples fail driver \\ \_ \\ WDM 目录中的一个示例 WDM 驱动程序。

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

### <a name="span-idcorrect_the_sdv_map_h_filespanspan-idcorrect_the_sdv_map_h_filespancorrect-the-sdv-maph-file"></a><span id="correct_the_sdv_map_h_file"></span><span id="CORRECT_THE_SDV_MAP_H_FILE"></span>更正 Sdv 文件

在验证驱动程序之前，请更正 Sdv 文件中的任何错误。 即使 Sdv 文件不正确或未批准，SDV 也将验证驱动程序，但验证的结果可能不可靠。 例如，如果未使用相应的函数角色类型声明驱动程序的调度或回调例程，则驱动程序例程将不会出现在 Sdv 文件中。 因此，你可能会遗漏在代码中查找缺陷，因为 SDV 将使用函数角色类型的规则视为不适用（即使你在验证过程中指定了这些规则）。

若要更正 Sdv-map .h 文件，请确保您的驱动程序的调度或回调例程是使用适当的函数角色类型声明的。 然后，重新扫描驱动程序，并验证它们是否显示在 Sdv 文件中。

### <a name="span-idapprove_the_sdv_map_h_filespanspan-idapprove_the_sdv_map_h_filespanapprove-the-sdv-maph-file"></a><span id="approve_the_sdv_map_h_file"></span><span id="APPROVE_THE_SDV_MAP_H_FILE"></span>批准 Sdv 文件

确定 Sdv 文件正确后，可以批准该文件。 如果未对文件进行任何更改，则无需批准。

即使未批准 Sdv 文件，SDV 仍将验证驱动程序。

若要批准 Sdv 文件，请在文件的第一行更改：

```
//Approved=false
```

to:

```
//Approved=true
```

对于每个驱动程序，只需批准 Sdv 文件一次。 此后，SDV 将为驱动程序保留批准的 Sdv 文件以供将来验证。 如果希望 SDV 再次扫描源代码以获取函数角色类型声明，只需删除该文件。

下面的示例显示了 KMDF 示例驱动程序的已批准 Sdv-map 文件，Driver1 失败 \_ 。 SDV 使用 Sdv 文件来映射驱动程序的已声明回调函数，该函数的函数角色类型 SDV 需验证。

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

 

 





