---
title: SCSI 微型端口驱动程序的注册表项
description: SCSI 微型端口驱动程序的注册表项
ms.assetid: bff5c004-7115-4436-b233-9d1d89643b23
keywords:
- SCSI 微型端口驱动程序 WDK 存储，注册表项
- 注册表 WDK SCSI
- TimeoutValue
- TotalSenseDataBytes
- MaximumSGList
- BusType
- CreateInitiatorLU
- 伪 Lun WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b30b56531349992478273c63f2781844fcfa55e8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368958"
---
# <a name="registry-entries-for-scsi-miniport-drivers"></a>SCSI 微型端口驱动程序的注册表项


## <span id="ddk_registry_entries_for_scsi_miniport_drivers_kg"></span><span id="DDK_REGISTRY_ENTRIES_FOR_SCSI_MINIPORT_DRIVERS_KG"></span>


以下注册表项，可配置的端口驱动程序/SCSI 微型端口驱动程序对的行为。 所需的所有即插 (PnP) 设备的 PnpInterface 注册表项的相关信息，请参阅[即插即用和播放 SCSI 微型端口驱动程序的注册表项](registry-entries-for-plug-and-play-scsi-miniport-drivers.md)。

-   **TimeoutValue**
    -   位置:HKLM\\System\\CurrentControlSet\\Services\\Disk\\TimeoutValue
    -   值：1-255 秒
    -   含义：磁盘类驱动程序由启动 SRB 请求超时之前等待的秒为单位的时间。如果未设置此注册表值，使用默认值为 10 秒。 超时值的类驱动程序发起的请求而异的类驱动程序。

        **请注意**  微型端口设置一个值，如果将优先采用该超时时间。 超时选择逻辑如下所示：
        -   在 Windows 8 中，从开始，如果微型端口设置一个超时值 （以 HKLM... \\服务\\&lt;微型端口&gt;\\参数\\IoTimeoutValue)，此值由存储类驱动程序。
        -   否则，如果设置磁盘全局超时时间注册表 （此密钥），则此值被遵循存储类驱动程序。
        -   否则，默认值为 10 秒使用存储类驱动程序。

         

    -   操作系统版本：此功能现已推出的 Windows 操作系统的所有版本。

<!-- -->

-   **TotalSenseDataBytes**
    -   位置:HKLM\\System\\CurrentControlSet\\Enum\\&lt;Bus&gt;\\&lt; DeviceID&gt;\\&lt;Device&gt;\\DeviceParameters\\ScsiPort\\TotalSenseDataBytes
    -   值：介于 18 和 SCSI 端口的 255 之间。 Storport 始终使用 255。
    -   含义：如果设置了此值指定的以字节为单位的缓冲区的大小 SCSI 端口驱动程序分配的请求检测数据。 如果未设置值，SCSI 端口将使用默认大小为 18。 Storport 驱动程序始终允许 255。 警告： 在类驱动程序和端口驱动程序之间插入的筛选器驱动程序必须遵守此值，尝试进行管理的意义上的数据缓冲区大小。
    -   操作系统版本：此功能是 Windows 2000 Server 和更高版本操作系统中。
-   **MaximumSGList**
    -   位置:HKLM\\系统\\CurrentControlSet\\Services\\&lt;ServiceName&gt;\\参数\\设备\\MaximumSGList，其中&lt;ServiceName&gt; = 使用指定的微型端口驱动程序名称**AddServices**指令 INF 文件中。
    -   值：介于 16 和 255 之间。
    -   含义：指示适配器支持的分散/聚拢列表元素的数目。
    -   操作系统版本：此功能是在 Windows NT 4.0 SP4 和更高版本操作系统中可用。
-   **BusType**
    -   位置:HKLM\\系统\\CurrentControlSet\\Services\\&lt;ServiceName&gt;\\参数\\BusType，其中&lt;ServiceName&gt; = 使用指定的微型端口驱动程序名称**AddServices**指令 INF 文件中。
    -   值：与相同[**存储\_总线\_类型**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff566356(v=vs.85))枚举器：
    -   含义：指示适配器连接到的总线类型。
    -   操作系统版本：此功能是在 Windows 2000 和更高版本操作系统中可用。
-   **CreateInitiatorLU**
    -   位置:&lt;ServiceName&gt;\\参数\\设备\\CreateInitiatorLU，其中&lt;ServiceName&gt; = 使用指定的微型端口驱动程序名称**AddServices**指令 INF 文件中。
    -   值：0 或 1。
    -   含义：如果值为 1 指示端口驱动程序将创建的"发起程序逻辑单元，"，以便即使没有任何实际的硬件设备连接到该适配器或者已连接的设备不可见更高级别的驱动程序可以将某些请求发送到端口驱动程序到系统。 有时有必要配置设备的操作参数或更新其固件之后才会对系统可见。 之前 Windows Server 2003 中，这是不可能会指示端口驱动程序更新设备固件，除非端口驱动程序在其设备堆栈中有至少一个逻辑单元。 某些供应商尝试通过将所谓"伪-Lun"添加到适配器的堆栈，但这个创建的安装程序和磁盘管理、 问题解决这一缺陷，但此类解决方案有时会导致要提示用户输入的配置管理器不是存在设备驱动程序。 使用新的"发起程序逻辑单元"功能，就不再需要使用这些解决方法。 通过设置**CreateInitiatorLU** Ioctl 可以发送到注册表中的 1，并为端口驱动程序请求 WMI 其是否具有连接的设备对操作系统可见的。 "发起程序逻辑单元"功能的另一个用途是允许通信与光纤通道适配器具有完全管理功能和任何附加的设备。
    -   操作系统版本：此功能是在 Windows Server 2003 和更高版本操作系统中可用。 此注册表值的值仅影响 SCSI 端口微型端口驱动程序的功能。 Storport 微型端口驱动程序始终允许对适配器对象的访问，即使没有设备连接到的适配器。

 

 




