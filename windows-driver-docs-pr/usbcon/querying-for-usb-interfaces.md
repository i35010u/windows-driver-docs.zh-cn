---
Description: 而不是使用的 I/O 请求数据包 (IRP) 机制，USB 客户端驱动程序可以获取对总线驱动程序接口的引用，并使用它来访问总线驱动程序例程。
title: 查询总线驱动程序接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 906c726b2f0c2f56faef43a9dbd13bc435df805f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358362"
---
# <a name="querying-for-bus-driver-interfaces"></a>查询总线驱动程序接口


而不是使用的 I/O 请求数据包 (IRP) 机制，USB 客户端驱动程序可以获取对总线驱动程序接口的引用，并使用它来访问总线驱动程序例程。




使用总线驱动程序接口为客户端驱动程序提供多项优势：

-   无需分配 IRP，它可以使用接口的服务。

-   它可以在引发 IRQL 调用接口的例程。

在 Windows Vista USB、 客户端驱动程序可以自身公开接口以便帮助[USB 常见类通用父驱动程序](usb-common-class-generic-parent-driver.md)中定义它管理的设备的接口集合。

若要获取总线驱动程序接口，客户端驱动程序必须发送[ **IRP\_MN\_查询\_接口**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)总线驱动程序的请求。 在客户端驱动程序：

1.  创建类型 IRP 的 IRP\_MN\_查询\_接口中的下一步的堆栈位置。
    ```cpp
    irpstack = IoGetNextIrpStackLocation(irp);
    irpstack->MajorFunction= IRP_MJ_PNP;
    irpstack->MinorFunction= IRP_MN_QUERY_INTERFACE;
    ```

2.  接口分配内存并指向新的内存堆栈。 例如，若要分配的内存[ **USB\_总线\_接口\_USBDI\_V0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbbusif/ns-usbbusif-_usb_bus_interface_usbdi_v0)接口：
    ```cpp
    irpstack->Parameters.QueryInterface.Interface = (USB_BUS_INTERFACE_USBDI_V0) newly allocated interface buffer;
    ```

3.  设置**InterfaceSpecificData**为 NULL。
    ```cpp
    irpstack->Parameters.QueryInterface.InterfaceSpecificData = NULL;
    ```

4.  初始化具有适当的接口 GUID 的 IRP 堆栈、 接口、 大小和接口的版本。
    ```cpp
    irpstack->Parameters.QueryInterface.InterfaceType = &USB_BUS_INTERFACE_USBDI_GUID;
    irpstack->Parameters.QueryInterface.Size = sizeof(USB_BUS_INTERFACE_USBDI_V0);
    irpstack->Parameters.QueryInterface.Version = USB_BUSIF_USBDI_VERSION_0;
    ntStatus = IoCallDriver(PDO that the client passes URBs to, irp);
    ```

5.  调用[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)传递查询界面 IRP 堆栈。
    ```cpp
    ntStatus = IoCallDriver(PDO that the client passes URBs to, irp);
    ```

有关 USB 的详细信息的接口，请参阅[USB 客户端驱动程序的总线驱动程序接口例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#usbdi)。

## <a name="related-topics"></a>相关主题
[开发适用于 USB 设备的 Windows 客户端驱动程序](usb-driver-development-guide.md)  



