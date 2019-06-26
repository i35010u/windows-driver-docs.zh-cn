---
title: 初始化常规 I/O 目标
description: 初始化常规 I/O 目标
ms.assetid: c5d5b589-09a3-4f58-83bf-2876b37b0937
keywords:
- 常规 I/O 面向 WDK KMDF，初始化
- 初始化常规 I/O 面向 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b9d2e5485c2dd5fb9018bc754b78fd0edc6ff3e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380561"
---
# <a name="initializing-a-general-io-target"></a>初始化常规 I/O 目标





当驱动程序调用时，框架初始化设备驱动程序的本地 I/O 目标[ **WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)。 若要检索设备的本地 I/O 目标，驱动程序调用的句柄[ **WdfDeviceGetIoTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicegetiotarget)。

大多数驱动程序将请求发送到其本地 I/O 目标仅。

若要初始化设备的远程 I/O 目标，该驱动程序必须：

1.  调用[ **WdfIoTargetCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetcreate)创建 I/O 目标对象。

2.  调用[ **WdfIoTargetOpen** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetopen)若要打开的 I/O 目标，以便该驱动程序可以向其发送请求。

当驱动程序调用[ **WdfIoTargetOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetopen)，它通常通过提供一个 Unicode 字符串，表示标识远程 I/O 目标[对象名称](https://docs.microsoft.com/windows-hardware/drivers/kernel/object-names)。 该名称可以标识设备、 文件或设备接口。 该框架将 I/O 请求发送到支持的对象名称的驱动程序堆栈的顶部。

很少，驱动程序可能会通过提供对 Windows 驱动程序模型 (WDM) 的指针标识远程 I/O 目标[**设备\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)结构。 此指针标识不同的驱动程序中调用的驱动程序堆栈。 基于框架的驱动程序很少使用此方法，因为它们很少能有权访问其他驱动程序**设备\_对象**结构。

下面的示例演示 Ndisedge 示例驱动程序如何使用上面的技术来创建并打开远程 I/O 目标：

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

 

 





