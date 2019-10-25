---
title: SPB 连接的外围设备的连接 ID
description: 驱动程序在简单的外围总线（SPB）上向外围设备发送 i/o 请求之前，驱动程序必须打开与设备的逻辑连接。
ms.assetid: 234B5858-5930-40AD-BE4C-4A774A809D10
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b69c56f4ecd1ee5c7561e4b0830e6257037516c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842757"
---
# <a name="connection-ids-for-spb-connected-peripheral-devices"></a>SPB 连接的外围设备的连接 ID


驱动程序在[简单的外围总线](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))（SPB）上向外围设备发送 i/o 请求之前，驱动程序必须打开与设备的逻辑连接。 通过此连接，驱动程序可以发送读写请求，以便将数据传入和传出设备。 此外，驱动程序可以将 i/o 控制（IOCTL）请求发送到设备，以执行特定于 SPB 的操作。




系统启动时，即插即用（PnP）管理器会枚举 PnP 设备和非 PnP 设备。 对于具有与 SPB 的固定连接的非 PnP 外围设备，PnP 管理器会查询硬件平台的 ACPI 固件，以获取描述如何访问设备的一组连接参数。 这些连接参数标识设备连接到的总线的 SPB 控制器，并包含控制器与设备通信所需的其他信息（如总线地址和总线时钟频率）。

PnP 管理器将标识符（称为*连接 ID*）分配给连接到 SPB 的外围设备的连接参数。 PnP 管理器将此 ID 和连接参数一起存储在名为*资源中心*的系统数据存储中。 （资源中心是一种内部数据存储，其中 PnP 管理器存储与 SPB 连接的外围设备有关的配置信息。）连接 ID 封装这些参数，以便驱动程序无需显式提供它们。

与 SPB 连接的外围设备的驱动程序将接收设备的连接 ID 作为驱动程序的已分配硬件资源的一部分。 当外围设备的驱动程序调用系统函数以打开与设备的连接时，驱动程序会提供连接 ID，该 ID 用于从资源中心检索设备的连接参数。

驱动程序开发人员可以使用[用户模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/overview-of-the-umdf)（UMDF）或[内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)（KMDF）来构建连接到 SPB 的外围设备的驱动程序。 当框架调用驱动程序的[**IPnpCallbackHardware2：： OnPrepareHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)方法时，UMDF 驱动程序将接收其资源（包括连接 ID）。 KMDF 驱动程序在[*EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调期间接收其硬件资源。

要使 UMDF 外设驱动程序能够在其资源列表中接收连接 Id，安装驱动程序的 INF 文件必须在其特定于 WDF 的**DDInstall**节中包含以下指令：

**UmdfDirectHardwareAccess = AllowDirectHardwareAccess**有关此指令的详细信息，请参阅[在 INF 文件中指定 WDF 指令](https://docs.microsoft.com/windows-hardware/drivers/wdf/specifying-wdf-directives-in-inf-files)。 有关使用此指令的 INX 文件（用于生成相应的 INF 文件）的示例，请参阅[SpbAccelerometer](https://go.microsoft.com/fwlink/p/?LinkId=618052)驱动程序示例。

驱动程序作为资源接收的连接 ID 是64位整数，但驱动程序必须将此 ID 合并为可用于从资源中心检索连接参数的设备路径名称。 若要创建设备路径名称，驱动程序将调用**资源\_中心\_通过\_ID**函数（在 Reshub 头文件中声明）创建\_路径\_。

若要打开与 SPB 连接的外围设备的逻辑连接，UMDF 驱动程序将调用[**IWDFRemoteTarget：： OpenFileByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-openfilebyname)方法，而 KMDF 驱动程序调用[**WdfIoTargetOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetopen)方法。 任一方法都需要设备路径名称作为输入参数。

有关使用连接 Id 打开与 SPB 连接的外围设备的逻辑连接的 UMDF 和 KMDF 代码示例，请参阅以下主题：

[用于用户模式 Spb 外围设备驱动程序的硬件资源](https://docs.microsoft.com/windows-hardware/drivers/spb/hardware-resources-for-user-mode-spb-peripheral-drivers)
[内核模式 spb 外围设备的硬件资源](https://docs.microsoft.com/windows-hardware/drivers/spb/hardware-resources-for-kernel-mode-spb-peripheral-drivers)用户模式应用程序无法打开到 SPB 连接的外围设备的逻辑连接，并且无法发送 i/o直接请求发送到这些设备。

一次只能有一个驱动程序可以对连接到 SPB 的外围设备保持开放的逻辑连接。 另一个驱动程序尝试打开与同一设备的第二个连接失败。

 

 




