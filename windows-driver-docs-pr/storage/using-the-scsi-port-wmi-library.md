---
title: 使用 SCSI 端口 WMI 库
description: 使用 SCSI 端口 WMI 库
ms.assetid: cb55bbb3-39bb-491f-a6d2-50dceace4a86
keywords:
- WMI Srb WDK 存储，SCSI 端口 WMI 库
- SCSI 端口 WMI 库 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3e97a86daa24747a9ad08c4b641d8bf16157ca0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566285"
---
# <a name="using-the-scsi-port-wmi-library"></a>使用 SCSI 端口 WMI 库


## <span id="ddk_using_the_scsi_port_wmi_library_kg"></span><span id="DDK_USING_THE_SCSI_PORT_WMI_LIBRARY_KG"></span>


函数与 WMI 提供程序的存储微型端口驱动程序可以使用 SCSI 端口 WMI 库可以简化处理 SCSI 请求块 (Srb) 包含 WMI 命令的任务。 微型端口驱动程序的启动 I/O 例程[ **HwScsiStartIo**](https://msdn.microsoft.com/library/windows/hardware/ff557323)，相关信息中 WMI SRB 通过向传递 SCSI 端口 WMI 库处理在调用[ **ScsiPortWmiDispatchFunction** ](https://msdn.microsoft.com/library/windows/hardware/ff564766)库的调度例程。 微型端口驱动程序会将以下数据传递到调度例程：

-   在中*WmiLibInfo*参数： [ **SCSI\_WMILIB\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff565395)微型端口驱动程序的回调例程的指针的结构。

-   在中*WMISubFunction*参数： 中的值**WMISubFunction** SRB 的成员。

-   在中*DeviceContext*参数： 指向设备扩展。

-   在中*RequestContext*参数： 类型的请求上下文结构[ **SCSIWMI\_请求\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff564946)的 SCSI 端口 WMI库使用来记录的信息，如返回状态和数据的大小。

-   在中*数据路径*参数： 中的值**数据路径**SRB 的成员。

-   在中*BufferSize*参数： 中的值**DataTransferLength** SRB 的成员。

-   在中*缓冲区*参数： 中的值**DataBuffer** SRB 的成员。

初始化微型端口驱动程序时，它必须填写[ **SCSI\_WMILIB\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff565395)使用指向所需的微型端口驱动程序回调例程的指针的结构，然后微型端口驱动程序特定于存储区域，如驱动程序扩展插件中存储结构。 每个微型端口驱动程序回调例程对应于次 IRP 版本号中, 所述[如何端口驱动程序进程 WMI 请求](how-the-port-driver-processes-wmi-requests.md)。 有关如何设计微型端口驱动程序回调例程的信息，请参阅[设计 WMI 微型端口驱动程序回调例程](designing-wmi-miniport-driver-callback-routines.md)

**GuidList**成员的 SCSI\_WMILIB\_上下文结构必须指向类型的元素的数组[ **SCSIWMIGUIDREGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff564941) ，包含唯一地标识在 MOF 文件中定义的受支持的 WMI 类的 Guid 有关的信息。 下面的代码段说明了此类元素的数组的定义：

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

数组包含的两个 WMI 类，信息 Guid **HBAStatistics**并**HBAAttributes**。 Guid 的符号常量拍摄从编译 MOF 文件，用于定义两个类的 WMI 工具套件与生成的标头文件 ( **mofcomp**并**wmimofck**工具)。 有关如何使用这些工具的详细信息，请参阅[编译的驱动程序的 MOF 文件](https://msdn.microsoft.com/library/windows/hardware/ff542012)并[使用 wmimofck.exe](https://msdn.microsoft.com/library/windows/hardware/ff565588)。

WMI 工具套件生成通过串联 WMI 类的名称后缀"GUID"的 GUID 的符号常量的名称。 例如，对于类**HBAStatistics，** 该工具将创建名为符号常量**HBAStatisticsGUID** ，表示该类的 GUID。

 

 




