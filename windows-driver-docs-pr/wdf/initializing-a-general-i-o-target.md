---
title: 初始化常规 I/O 目标
description: 初始化常规 I/O 目标
ms.assetid: c5d5b589-09a3-4f58-83bf-2876b37b0937
keywords:
- 一般 i/o 目标 WDK KMDF，初始化
- 初始化常规 i/o 目标 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89a38d455c34c10ca2dae2228212813ae75cf0e6
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89183921"
---
# <a name="initializing-a-general-io-target"></a>初始化常规 I/O 目标





当驱动程序调用 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)时，框架会为设备初始化驱动程序的本地 i/o 目标。 若要检索设备的本地 i/o 目标的句柄，驱动程序将调用 [**WdfDeviceGetIoTarget**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetiotarget)。

大多数驱动程序只向其本地 i/o 目标发送请求。

若要为设备初始化远程 i/o 目标，驱动程序必须：

1.  调用 [**WdfIoTargetCreate**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetcreate) 创建 i/o 目标对象。

2.  调用 [**WdfIoTargetOpen**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetopen) 打开 i/o 目标，以便驱动程序可以向其发送请求。

当驱动程序调用 [**WdfIoTargetOpen**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetopen)时，它通常通过提供表示 [对象名称](../kernel/object-names.md)的 Unicode 字符串来标识远程 i/o 目标。 此名称可以标识设备、文件或设备接口。 框架将 i/o 请求发送到支持对象名称的驱动程序堆栈的顶部。

很少情况下，驱动程序可以通过提供指向 Windows 驱动模型 (WDM) [**设备 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object) 结构的指针来识别远程 i/o 目标。 此指针标识调用驱动程序堆栈中的另一个驱动程序。 基于框架的驱动程序很少使用这种方法，因为它们极少具有对其他驱动程序 **设备 \_ 对象** 结构的访问权限。

下面的示例演示 Ndisedge 示例驱动程序如何使用上述技术来创建和打开远程 i/o 目标：

```cpp
status = WdfIoTargetCreate(Adapter->WdfDevice,
                        WDF_NO_OBJECT_ATTRIBUTES,
                        &Adapter->IoTarget);
    if (!NT_SUCCESS(status)) {
        DEBUGP(MP_ERROR, ("WdfIoTargetCreate failed 0x%x\n",
               status));
        return status;
    }

    WDF_IO_TARGET_OPEN_PARAMS_INIT_CREATE_BY_NAME(&openParams,
                                &fileName,
                                STANDARD_RIGHTS_ALL
                                );

    status = WdfIoTargetOpen(Adapter->IoTarget,
                        &openParams);
    if (!NT_SUCCESS(status)) {
        DEBUGP(MP_ERROR, ("WdfIoTargetOpen failed 0x%x\n", status));
        return status;
    }
```

 

