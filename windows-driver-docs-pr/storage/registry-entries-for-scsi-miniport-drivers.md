---
title: SCSI 微型端口驱动程序的注册表项
description: SCSI 微型端口驱动程序的注册表项
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
ms.openlocfilehash: 26ba97b6cb103097ea4d5d98232e6c53dc423bff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791279"
---
# <a name="registry-entries-for-scsi-miniport-drivers"></a>SCSI 微型端口驱动程序的注册表项


## <span id="ddk_registry_entries_for_scsi_miniport_drivers_kg"></span><span id="DDK_REGISTRY_ENTRIES_FOR_SCSI_MINIPORT_DRIVERS_KG"></span>


以下注册表项可用于配置端口驱动程序/SCSI 微型端口驱动程序对的行为。 有关即插即用 (PnP) 设备所需的 PnpInterface 注册表项的信息，请参阅 [即插即用 SCSI 微型端口驱动程序的注册表项](registry-entries-for-plug-and-play-scsi-miniport-drivers.md)。

-   **TimeoutValue**
    -   位置： HKLM \\ System \\ CurrentControlSet \\ Services \\ Disk \\ TimeoutValue
    -   值： 1-255 秒
    -   含义：由磁盘类驱动程序启动的 SRB 请求超时之前的时间（秒）。如果未设置此注册表值，则使用默认值10秒。 类驱动程序启动的请求的超时值因类驱动程序而异。

        **注意**  如果微型端口设置了值，则将优先使用该超时值。 超时选择逻辑如下所示：
        -   从 Windows 8 开始，如果微型端口设置的超时值 (在 HKLM .。。 \\服务 \\ &lt; 微型 &gt; \\ 参数 \\ IoTimeoutValue) ，此值由存储类驱动程序使用。
        -   否则，如果设置了磁盘全局超时注册表 (此密钥) 设置，则存储类驱动程序将接受此值。
        -   否则，存储类驱动程序将使用默认值10秒。

         

    -   操作系统版本：此功能在所有版本的 Windows 操作系统中可用。

<!-- -->

-   **TotalSenseDataBytes**
    -   位置： HKLM \\ 系统 \\ CurrentControlSet \\ 枚举 \\ &lt; 总线 &gt; \\ &lt; DeviceID &gt; \\ &lt; 设备 &gt; \\ DeviceParameters \\ ScsiPort \\ TotalSenseDataBytes
    -   值：对于 SCSI 端口，介于18到255之间。 Storport 始终使用255。
    -   含义：如果设置此值，此值将指定 SCSI 端口驱动程序为请求感知数据分配的缓冲区的大小（以字节为单位）。 如果未设置该值，则 SCSI 端口使用默认大小为18。 Storport 驱动程序始终允许255。 警告：在类驱动程序和端口驱动程序之间插入的筛选器驱动程序必须遵守此值，并且不尝试管理感知数据缓冲区的大小。
    -   操作系统版本：此功能在 Windows 2000 Server 及更高版本的操作系统中可用。
-   **MaximumSGList**
    -   Location： HKLM \\ System \\ CurrentControlSet \\ Services \\ &lt; ServiceName &gt; \\ PARAMETERS \\ Device \\ MaximumSGList，其中 &lt; ServiceName &gt; = INF 文件中的 **AddServices** 指令指定的微型端口驱动程序名称。
    -   值：介于16和255之间。
    -   含义：指示适配器支持的散点/集合列表元素的数目。
    -   操作系统版本：此功能在 Windows NT 4.0 SP4 和更高版本的操作系统中可用。
-   **BusType**
    -   Location： HKLM \\ System \\ CurrentControlSet \\ Services \\ &lt; ServiceName &gt; \\ PARAMETERS \\ BusType，其中 &lt; ServiceName &gt; = 通过 INF 文件中的 **AddServices** 指令指定的微型端口驱动程序名称。
    -   值：与 [**存储 \_ 总线 \_ 类型**](/previous-versions/windows/hardware/drivers/ff566356(v=vs.85)) 枚举器相同：
    -   含义：指示适配器连接到的总线类型。
    -   操作系统版本：此功能在 Windows 2000 和更高版本的操作系统中可用。
-   **CreateInitiatorLU**
    -   Location： &lt; servicename &gt; \\ 参数 \\ Device \\ CreateInitiatorLU，其中 &lt; ServiceName &gt; = 在 INF 文件中用 **AddServices** 指令指定的微型端口驱动程序名称。
    -   值：0或1。
    -   含义：值为1表示端口驱动程序将创建一个 "发起方逻辑单元"，以便更高级别的驱动程序可以将某些请求发送到端口驱动程序，即使没有实际的硬件设备连接到该适配器或连接的设备对系统不可见。 有时，需要配置设备的操作参数或更新其固件后，系统才会显示该设备。 在 Windows Server 2003 之前，除非端口驱动程序的设备堆栈中至少有一个逻辑单元，否则不能指示端口驱动程序更新设备的固件。 某些供应商尝试通过将所谓的 "伪 Lun" 添加到适配器的堆栈来更正此缺陷，但这会导致安装程序和磁盘管理出现问题，有时此类解决方案将导致 configuration manager 提示用户提供不存在的设备的驱动程序。 使用新的 "发起方逻辑单元" 功能，不再需要使用这些解决方法。 通过在注册表中将 **CreateInitiatorLU** 设置为1，可以将 IOCTLS 和 WMI 请求发送到端口驱动程序，无论该设备是否附加了对操作系统可见的设备。 "发起方逻辑单元" 功能的另一个用途是允许与光纤通道适配器进行通信，该适配器具有纯粹的管理功能，但没有附加的设备。
    -   操作系统版本：此功能在 Windows Server 2003 及更高版本的操作系统中可用。 此注册表值的值仅影响 SCSI 端口微型端口驱动程序的功能。 即使没有设备连接到适配器，还可以使用 Storport 微型端口驱动程序始终允许对适配器对象进行访问。

 

