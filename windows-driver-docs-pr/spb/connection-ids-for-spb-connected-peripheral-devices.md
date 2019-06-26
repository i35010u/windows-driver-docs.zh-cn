---
title: SPB 连接的外围设备的连接 ID
description: 驱动程序可以将 I/O 请求发送到简单的外围总线 （存储） 上的外围设备之前，该驱动程序必须打开到设备的逻辑连接。
ms.assetid: 234B5858-5930-40AD-BE4C-4A774A809D10
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0484928a4757737b3e78e50030be13e732e664e9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353269"
---
# <a name="connection-ids-for-spb-connected-peripheral-devices"></a>SPB 连接的外围设备的连接 ID


驱动程序可以外围设备向发送 I/O 请求之前[简单的外围总线](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))（存储），该驱动程序必须打开到设备的逻辑连接。 通过此连接，该驱动程序可以发送读取和写入请求来传输设备数据。 此外，驱动程序可以发送 I/O 控制 (IOCTL) 请求到设备来执行特定于存储的操作。




在系统启动时，插即用 (PnP) 管理器枚举即插即用设备和非 PnP 设备。 对于非 PnP 外围设备具有固定的连接到存储，即插即用管理器将查询硬件平台的 ACPI 固件来获取一系列介绍如何访问设备的连接参数。 这些连接参数标识的总线向其设备已连接，并包括其他信息，例如总线地址和总线时钟频率，在控制器与设备进行通信所需的存储控制器。

PnP 管理器将分配一个标识符，调用*连接 ID*— 对存储连接的外围设备连接参数。 PnP 管理器将此 ID 和连接参数一起调用的系统数据存储中存储*资源中心*。 （资源中心是 PnP 管理器将在其中存储有关与存储连接的外围设备的配置信息的内部数据存储。）连接 ID 包装这些参数，以便该驱动程序不需要显式提供它们。

与存储连接的外围设备的驱动程序作为驱动程序的已分配的硬件资源的一部分接收设备的连接 ID。 当外围设备的驱动程序调用系统函数，以打开到设备的连接时，驱动程序提供的连接 ID，该函数使用要从资源中心检索设备的连接参数。

驱动程序开发人员可以使用两个[用户模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/overview-of-the-umdf)(UMDF) 或[内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)(KMDF) 生成存储连接的外围设备的驱动程序。 UMDF 驱动程序将收到其资源 （其中包括连接 ID） 框架时调用的驱动程序[ **IPnpCallbackHardware2::OnPrepareHardware** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)方法。 KMDF 驱动程序将收到其硬件资源期间[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调。

若要启用 UMDF 外围设备驱动程序以接收其资源的列表中的连接 Id，请安装该驱动程序的 INF 文件必须包含以下指令中其 WDF 特定**DDInstall**部分：

**UmdfDirectHardwareAccess = AllowDirectHardwareAccess**有关此指令的详细信息，请参阅[INF 文件中指定 WDF 指令](https://docs.microsoft.com/windows-hardware/drivers/wdf/specifying-wdf-directives-in-inf-files)。 使用此指令的 INX 文件 （用来生成相应的 INF 文件） 的示例，请参阅[SpbAccelerometer](https://go.microsoft.com/fwlink/p/?LinkId=618052)驱动程序示例。

驱动程序收到作为资源的连接 ID 的 64 位整数，但该驱动程序必须将此 ID 合并到可用于从资源中心检索的连接参数的设备路径名称。 若要创建的设备路径名称，驱动程序调用**资源\_中心\_创建\_路径\_FROM\_ID** Reshub.h 标头文件中声明的函数。

若要打开存储连接的外围设备的逻辑连接，UMDF 驱动程序调用[ **IWDFRemoteTarget::OpenFileByName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremotetarget-openfilebyname)方法和 KMDF 驱动程序调用[ **WdfIoTargetOpen** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetopen)方法。 这两种方法要求的设备路径名称作为输入参数。

连接 Id 用于打开到已连接存储的外围设备的逻辑连接的 UMDF 和 KMDF 代码示例，请参阅以下主题：

[用户模式下存储外围设备驱动程序的硬件资源](https://docs.microsoft.com/windows-hardware/drivers/spb/hardware-resources-for-user-mode-spb-peripheral-drivers)
[内核模式存储外围设备驱动程序的硬件资源](https://docs.microsoft.com/windows-hardware/drivers/spb/hardware-resources-for-kernel-mode-spb-peripheral-drivers)用户模式应用程序无法打开存储连接到的逻辑连接外围设备，并且不能直接向这些设备发送 I/O 请求。

只有一个驱动程序可以保存打开的逻辑连接到与存储连接的外围设备一次。 由另一个驱动程序尝试打开到同一设备的第二个连接会失败。

 

 




