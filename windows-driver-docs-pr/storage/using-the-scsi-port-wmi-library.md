---
title: 使用 SCSI 端口 WMI 库
description: 使用 SCSI 端口 WMI 库
ms.assetid: cb55bbb3-39bb-491f-a6d2-50dceace4a86
keywords:
- WMI SRBs WDK 存储，SCSI 端口 WMI 库
- SCSI 端口 WMI 库 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 530e9ae66d20a5f212183be07d89d2543e788133
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845587"
---
# <a name="using-the-scsi-port-wmi-library"></a>使用 SCSI 端口 WMI 库


## <span id="ddk_using_the_scsi_port_wmi_library_kg"></span><span id="DDK_USING_THE_SCSI_PORT_WMI_LIBRARY_KG"></span>


作为 WMI 提供程序运行的存储微型端口驱动程序可以使用 SCSI 端口 WMI 库来简化处理包含 WMI 命令的 SCSI 请求块（SRBs）的任务。 微型端口驱动程序的启动 i/o 例程[**HwScsiStartIo**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))将 wmi SRB 中的相关信息传递到 SCSI 端口 wmi 库，以便通过调用[**ScsiPortWmiDispatchFunction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nf-scsiwmi-scsiportwmidispatchfunction)库的调度例程进行处理。 微型端口驱动程序会将以下数据传递到调度例程：

-   在*WmiLibInfo*参数中：一个[**SCSI\_WMILIB\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/ns-scsiwmi-_scsiwmilib_context)结构，其中包含指向微型端口驱动程序的回调例程的指针。

-   在*WMISubFunction*参数中： SRB 的**WMISubFunction**成员中的值。

-   在*DeviceContext*参数中：指向设备扩展的指针。

-   在*RequestContext*参数中： SCSIWMI 类型的请求上下文结构[ **\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/ns-scsiwmi-scsiwmi_request_context)SCSI 端口 WMI 库用来记录信息的\_上下文，如返回的数据的状态和大小。

-   在*数据路径*参数中： SRB 的**数据路径**成员中的值。

-   在*BufferSize*参数中： SRB 的**DataTransferLength**成员中的值。

-   在*Buffer*参数中： SRB 的**DataBuffer**成员中的值。

初始化微型端口驱动程序时，它必须使用指向所需微型端口驱动程序回调例程的指针填充[**SCSI\_WMILIB\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/ns-scsiwmi-_scsiwmilib_context)结构，然后将该结构存储在微型端口驱动程序特定的存储区域中，如驱动程序扩展。 每个微型端口驱动程序回调例程对应次要 IRP 号，如[端口驱动程序处理 WMI 请求的方式中所](how-the-port-driver-processes-wmi-requests.md)述。 有关如何设计微型端口驱动程序回调例程的信息，请参阅[设计 WMI 微型端口驱动程序回调例程](designing-wmi-miniport-driver-callback-routines.md)

SCSI\_WMILIB\_上下文结构的**GuidList**成员必须指向[**SCSIWMIGUIDREGINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/ns-scsiwmi-scsiwmiguidreginfo)类型的元素数组，其中包含有关 guid 的信息，这些 guid 用于唯一标识在MOF 文件。 下面的代码段演示了此类元素数组的定义：

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

该数组包含有关两个 WMI 类（ **HBAStatistics**和**HBAAttributes**）的 guid 的信息。 Guid 的符号常量来自于通过编译 MOF 文件生成的头文件，该文件使用 WMI 工具套件（ **mofcomp.exe**和**wmimofck**工具）定义这两个类。 有关如何使用这些工具的详细信息，请参阅[编译驱动程序的 MOF 文件](https://docs.microsoft.com/windows-hardware/drivers/kernel/compiling-a-driver-s-mof-file)和[使用 wmimofck](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-wmimofck-exe)。

WMI 工具套件将后缀 "GUID" 连接到 WMI 类的名称，从而生成 GUID 的符号常数的名称。 例如，对于类**HBAStatistics，** 该工具将创建一个名为**HBAStatisticsGUID**的符号常数，表示该类的 GUID。

 

 




