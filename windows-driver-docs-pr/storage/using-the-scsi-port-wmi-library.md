---
title: 使用 SCSI 端口 WMI 库
description: 使用 SCSI 端口 WMI 库
ms.assetid: cb55bbb3-39bb-491f-a6d2-50dceace4a86
keywords:
- WMI SRBs WDK 存储，SCSI 端口 WMI 库
- SCSI 端口 WMI 库 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d12fcbe3886c5e0d97cc55c7a776227bb3327b8
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191631"
---
# <a name="using-the-scsi-port-wmi-library"></a>使用 SCSI 端口 WMI 库


## <span id="ddk_using_the_scsi_port_wmi_library_kg"></span><span id="DDK_USING_THE_SCSI_PORT_WMI_LIBRARY_KG"></span>


作为 WMI 提供程序运行的存储微型端口驱动程序可以使用 SCSI 端口 WMI 库来简化处理 SCSI 请求块的任务 (包含 WMI 命令的 SRBs) 。 微型端口驱动程序的启动 i/o 例程 [**HwScsiStartIo**](/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))将 wmi SRB 中的相关信息传递到 SCSI 端口 wmi 库，以便通过调用 [**ScsiPortWmiDispatchFunction**](/windows-hardware/drivers/ddi/scsiwmi/nf-scsiwmi-scsiportwmidispatchfunction) 库的调度例程进行处理。 微型端口驱动程序会将以下数据传递到调度例程：

-   在 *WmiLibInfo* 参数中：一个 [**SCSI \_ WMILIB \_ 上下文**](/windows-hardware/drivers/ddi/scsiwmi/ns-scsiwmi-_scsiwmilib_context) 结构，其中包含指向微型端口驱动程序的回调例程的指针。

-   在 *WMISubFunction* 参数中： SRB 的 **WMISubFunction** 成员中的值。

-   在 *DeviceContext* 参数中：指向设备扩展的指针。

-   在 *RequestContext* 参数中： [**SCSIWMI \_ 请求 \_ 上下文**](/windows-hardware/drivers/ddi/scsiwmi/ns-scsiwmi-scsiwmi_request_context) 的请求上下文结构，SCSI 端口 WMI 库使用该上下文来记录信息，如返回的数据的状态和大小。

-   在 *数据路径* 参数中： SRB 的 **数据路径** 成员中的值。

-   在 *BufferSize* 参数中： SRB 的 **DataTransferLength** 成员中的值。

-   在 *Buffer* 参数中： SRB 的 **DataBuffer** 成员中的值。

初始化微型端口驱动程序时，它必须使用指向所需微型端口驱动程序回调例程的指针填充 [**SCSI \_ WMILIB \_ 上下文**](/windows-hardware/drivers/ddi/scsiwmi/ns-scsiwmi-_scsiwmilib_context) 结构，然后将该结构存储在微型端口驱动程序特定的存储区域中，如驱动程序扩展。 每个微型端口驱动程序回调例程对应次要 IRP 号，如 [端口驱动程序处理 WMI 请求的方式中所](how-the-port-driver-processes-wmi-requests.md)述。 有关如何设计微型端口驱动程序回调例程的信息，请参阅 [设计 WMI 微型端口驱动程序回调例程](designing-wmi-miniport-driver-callback-routines.md)

SCSI **GuidList** \_ WMILIB 上下文结构的 GuidList 成员 \_ 必须指向[**SCSIWMIGUIDREGINFO**](/windows-hardware/drivers/ddi/scsiwmi/ns-scsiwmi-scsiwmiguidreginfo)类型的元素数组，其中包含有关 guid 的信息，这些 guid 用于唯一标识 MOF 文件中定义的受支持 WMI 类。 下面的代码段演示了此类元素数组的定义：

```cpp
SCSIWMIGUIDREGINFO GuidList[] = 
{
  {
    &HBAStatisticsGUID,  // Guid
    3,  // number of instances of this class
    0  // flags
  },
  {
    &HBAAttributesGUID, // guid
    1,  // number of instances of this class
    0  // flags
  }
};
```

该数组包含有关两个 WMI 类（ **HBAStatistics** 和 **HBAAttributes**）的 guid 的信息。 Guid 的符号常量是从使用 WMI 工具套件定义两个类的 MOF 文件中获取的标头文件， (**mofcomp.exe** 和 **wmimofck** 工具 ") 。 有关如何使用这些工具的详细信息，请参阅 [编译驱动程序的 MOF 文件](../kernel/compiling-a-driver-s-mof-file.md) 和 [使用 wmimofck.exe](../kernel/using-wmimofck-exe.md)。

WMI 工具套件将后缀 "GUID" 连接到 WMI 类的名称，从而生成 GUID 的符号常数的名称。 例如，对于类 **HBAStatistics，** 该工具将创建一个名为 **HBAStatisticsGUID** 的符号常数，表示该类的 GUID。

 

