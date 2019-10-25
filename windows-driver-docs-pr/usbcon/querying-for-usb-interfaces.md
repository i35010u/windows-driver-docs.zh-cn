---
Description: USB 客户端驱动程序可以获取对总线驱动程序接口的引用，并使用它来访问总线驱动程序例程，而不是使用 i/o 请求数据包（IRP）机制。
title: 查询总线驱动程序接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d2551f404da196f7d007d5d71649823e1489b1f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824206"
---
# <a name="querying-for-bus-driver-interfaces"></a>查询总线驱动程序接口


USB 客户端驱动程序可以获取对总线驱动程序接口的引用，并使用它来访问总线驱动程序例程，而不是使用 i/o 请求数据包（IRP）机制。




使用总线驱动程序接口可为客户端驱动程序提供以下几个优点：

-   它可以使用接口的服务而无需分配 IRP。

-   它可以在引发的 IRQL 处调用接口的例程。

在 Windows Vista USB 中，客户端驱动程序本身可以公开一个接口，以帮助[USB 公共类通用父驱动程序](usb-common-class-generic-parent-driver.md)为它所管理的设备定义界面集合。

若要获取总线驱动程序接口，客户端驱动程序必须将[**IRP\_MN\_QUERY\_interface**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)请求发送到总线驱动程序。 在客户端驱动程序中：

1.  在下一个堆栈位置创建类型为 IRP\_MN\_QUERY\_接口的 IRP。
    ```cpp
    irpstack = IoGetNextIrpStackLocation(irp);
    irpstack->MajorFunction= IRP_MJ_PNP;
    irpstack->MinorFunction= IRP_MN_QUERY_INTERFACE;
    ```

2.  为接口分配内存，并将堆栈点设置为新内存。 例如，若要为[**USB\_总线\_接口分配内存\_USBDI\_V0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbbusif/ns-usbbusif-_usb_bus_interface_usbdi_v0)接口：
    ```cpp
    irpstack->Parameters.QueryInterface.Interface = (USB_BUS_INTERFACE_USBDI_V0) newly allocated interface buffer;
    ```

3.  将**InterfaceSpecificData**设置为 NULL。
    ```cpp
    irpstack->Parameters.QueryInterface.InterfaceSpecificData = NULL;
    ```

4.  用适当的接口 GUID、接口的大小和接口版本初始化 IRP 堆栈。
    ```cpp
    irpstack->Parameters.QueryInterface.InterfaceType = &USB_BUS_INTERFACE_USBDI_GUID;
    irpstack->Parameters.QueryInterface.Size = sizeof(USB_BUS_INTERFACE_USBDI_V0);
    irpstack->Parameters.QueryInterface.Version = USB_BUSIF_USBDI_VERSION_0;
    ntStatus = IoCallDriver(PDO that the client passes URBs to, irp);
    ```

5.  调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) ，将查询接口 IRP 向下传递到堆栈。
    ```cpp
    ntStatus = IoCallDriver(PDO that the client passes URBs to, irp);
    ```

有关 USB 接口的详细信息，请参阅[适用于 Usb 客户端驱动程序的总线驱动程序接口例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#usbdi)。

## <a name="related-topics"></a>相关主题
[为 USB 设备开发 Windows 客户端驱动程序](usb-driver-development-guide.md)  



