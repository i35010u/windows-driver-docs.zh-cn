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
ms.openlocfilehash: bd678e28751d6a5fa914ec02055f9ee95b1c3192
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838327"
---
# <a name="using-the-wmi-library-to-register-blocks"></a>使用 WMI 库注册块





驱动程序可以使用 WMI 库来处理[**IRP\_MN\_REGINFO**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)和[**irp\_MN\_REGINFO\_EX**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)请求，前提是注册不使用动态实例名称的块，或使用静态实例名称基于PDO 或驱动程序定义的基名称字符串。 在这种情况下，驱动程序：

1.  调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) ，其中包含指向驱动程序的设备对象的指针、指向[**WMILIB\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)的指针和指向 IRP 的指针

    **WMILIB\_上下文**结构指示要注册的块数（**GuidCount**），并指向指定 GUID、实例数和注册的[**WMIGUIDREGINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmiguidreginfo)结构（**GuidList**）的列表与相应块相关的标志。 它还定义驱动程序的必需和可选*DpWmiXxx*回调例程的入口点。

2.  当 WMI 调用驱动程序的[*DpWmiQueryReginfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_reginfo_callback)例程时，驱动程序将指定驱动程序的注册表路径、其 MOF 资源名称、与所有块相关的注册标志，并指定 WMI 用来命名驱动程序数据实例的信息块，它可能是指向传递给驱动程序的[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程的物理设备对象的指针，或者是要作为静态实例名称基础的字符串。

在调用**WmiSystemControl**之前，驱动程序必须在**WMILIB\_上下文**结构中初始化其*DpWmiXxx*回调例程的入口点，但可以在在 WMI 调用驱动程序的*DpWmiQueryReginfo*例程之前， **WMILIB\_的上下文**结构。

 

 




