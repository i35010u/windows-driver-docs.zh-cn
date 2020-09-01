---
title: 使用 WMI 库注册块
description: 使用 WMI 库注册块
ms.assetid: 1f4b773d-ca24-47f5-87e8-84c98dad9267
keywords:
- WMI WDK 内核，用 WMI 注册
- 注册 WMI 数据提供程序
- 数据访问接口 WDK WMI
- 驱动程序注册 WDK WMI
- 事件块 WDK WMI
- 阻止 WDK WMI
- IRP_MN_REGINFO
- IRP_MN_REGINFO_EX
- 注册块
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d49da8fad88c258b152b0f4db6f187c604dd178f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187695"
---
# <a name="using-the-wmi-library-to-register-blocks"></a>使用 WMI 库注册块





驱动程序可以使用 WMI 库处理 [**irp \_ MN \_ REGINFO**](./irp-mn-reginfo.md) 和 [**irp \_ MN \_ REGINFO \_ EX**](./irp-mn-reginfo-ex.md) 请求，前提是它正在注册不使用动态实例名称的块，或使用基于 PDO 或驱动程序定义的基名称字符串的静态实例名称。 在这种情况下，驱动程序：

1.  使用指向驱动程序的设备对象的指针、指向[**WMILIB \_ 上下文**](/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)结构的指针和指向 IRP 的指针调用[**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

    **WMILIB \_ 上下文**结构指示用于注册 (**GuidCount**) 的块数，并指向一个[**WMIGUIDREGINFO**](/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmiguidreginfo)结构列表， (**GuidList**) 指定 GUID、实例数和与相应块相关的注册标志。 它还定义驱动程序的必需和可选 *DpWmiXxx* 回调例程的入口点。

2.  当 WMI 调用驱动程序的 [*DpWmiQueryReginfo*](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_reginfo_callback) 例程时，驱动程序将指定驱动程序的注册表路径、其 MOF 资源名称、与其所有块相关的注册标志，并指定 WMI 用来命名驱动程序数据块实例的信息，这些信息可能是指向传递给驱动程序的 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程的物理设备对象的指针，或者是作为静态实例名称基础的字符串。

在调用**WmiSystemControl**之前，驱动程序必须在**WMILIB \_ 上下文**结构中初始化其*DpWmiXxx*回调例程的入口点，但在 WMI 调用驱动程序的*GuidList*例程之前，**可以 \_ 将** **GuidCount**和**WMILIB**的初始化推迟。

 

