---
title: 使用虚拟 HID 框架 (VHF) 编写 HID 源驱动程序
description: 了解如何编写将 HID 数据报告给操作系统的 HID 源驱动程序。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00ac2fb303fca184075ab487fb51eba894c82978
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97091192"
---
# <a name="write-a-hid-source-driver-by-using-virtual-hid-framework-vhf"></a>使用虚拟 HID 框架 (VHF) 编写 HID 源驱动程序

**摘要**

-   写入 Kernel-Mode Driver Framework (KMDF) HID 源驱动程序，该驱动程序将 HID 读取报告提交到操作系统。
-   将 VHF 驱动程序作为低级筛选器加载到虚拟 HID 设备堆栈中的 HID 源驱动程序。

**适用于**

-   Windows 10
-   HID 设备的驱动程序开发人员

**重要的 API**

-   [虚拟 HID 框架回调函数](/windows-hardware/drivers/ddi/_hid/#callback-functions)
-   [虚拟 HID 框架方法](/windows-hardware/drivers/ddi/_hid/#functions)
-   [虚拟 HID 框架结构](/windows-hardware/drivers/ddi/_hid/#functions)

了解如何编写将 HID 数据报告给操作系统的 HID 源驱动程序。

HID 输入设备（例如键盘、鼠标、笔、触摸或按钮）会将不同的报告发送给操作系统，以便它能够理解设备的用途并执行必要的操作。 报告采用 [hid 集合](opening-hid-collections.md) 和 [hid 用法](hid-usages.md)的形式。 设备将这些报告发送到各种传输，Windows 支持其中的某些传输，例如，通过 [I2C 上的 hid](hid-over-i2c-guide.md) 和 [hid over USB](hid-over-usb.md)。 在某些情况下，Windows 可能不支持传输，或者报表可能不会直接映射到实际硬件。 它可以是由其他软件组件为虚拟硬件（例如，对于非 GPIO 按钮或传感器）发送的 HID 格式的数据流。 例如，请考虑加速将数据视为游戏控制器，并将其无线发送到 PC。 在另一个示例中，计算机可以使用 UIBC 协议从 Miracast 设备接收远程输入。

在以前版本的 Windows 中，若要支持 (真正的硬件或软件) 的新传输，你必须编写一个 [HID 传输微型驱动程序](transport-minidrivers.md) ，并将其绑定到 Microsoft 提供的内置类驱动程序，Hidclass.sys。 类/微型驱动程序对提供了 HID 集合，例如顶级驱动程序和用户模式应用程序的 [顶层集合](top-level-collections.md) 。 在该模型中，面临的挑战是编写微型驱动程序，这可能是一项复杂的任务。

从 Windows 10 开始，新的虚拟 HID 框架 (VHF) 无需编写传输微型驱动程序。 相反，你可以使用 KMDF 或 WDM 编程接口编写一个 HID 源驱动程序。 此框架由 Microsoft 提供的用于公开您的驱动程序所使用的编程元素的静态库组成。 它还包括一个 Microsoft 提供的内置驱动程序，用于枚举一个或多个子设备并继续构建和管理虚拟 HID 树。

**注意**  在此版本中，VHF 仅在内核模式下支持 HID 源驱动程序。

本主题介绍框架、虚拟 HID 设备树和配置方案的体系结构。

## <a name="virtual-hid-device-tree"></a>虚拟 HID 设备树

在此图中，设备树显示了驱动程序及其关联的设备对象。

![虚拟 hid 设备树](images/vhf.png)

**(驱动程序的 HID 源驱动程序)**

HID 源驱动程序链接到 Vhfkm，并在其生成项目中包括 Vhf。 该驱动程序可以使用 [Windows 驱动模型](../kernel/writing-wdm-drivers.md) (WDM) 或 Kernel-Mode 驱动程序框架 (KMDF) （这是 [Windows 驱动程序框架 (WDF) ](../what-s-new-in-driver-development.md)的一部分）编写的。 驱动程序可以作为筛选器驱动程序或设备堆栈中的函数驱动程序加载。

**VHF 静态库 (vhfkm)**

静态库包含在 windows 10 (WDK) 的 Windows 驱动程序工具包中。 库公开了由 HID 源驱动程序使用的编程接口，如例程和回调函数。 当驱动程序调用函数时，静态库会将请求转发给处理请求的 VHF 驱动程序。

**VHF 驱动程序 ( # A0)**

Microsoft 提供的内置驱动程序。 此驱动程序必须作为下方筛选器驱动程序加载到 HID 源设备堆栈中的驱动程序下。 VHF 驱动程序会动态枚举子设备，并 (PDO) 为 HID 源驱动程序指定的一个或多个 HID 设备创建物理设备对象。 它还实现枚举的子设备的 HID 传输微型驱动程序功能。

**HID 类驱动程序对 ( # A0、Mshidkmdf.sys)**

Hidclass/Mshidkmdf 对枚举 [顶级集合 (的 TLC) ](top-level-collections.md) 类似于它枚举真实 HID 设备的集合的方式。 HID 客户端可以继续请求和使用 TLCs，就像实际的 HID 设备一样。 此驱动程序对作为函数驱动程序安装在设备堆栈中。

**注意**  在某些情况下，HID 客户端可能需要标识 HID 数据的源。 例如，系统具有内置传感器，并从同一类型的远程传感器接收数据。 系统可能需要选择一个传感器来更可靠。 为区分连接到系统的两个传感器，HID 客户端将查询 TLC 的容器 ID。 在这种情况下，HID 源驱动程序可以提供容器 ID，该 ID 通过 VHF 报告为虚拟 HID 设备的容器 ID。

**HID 客户端 (应用程序)**

查询并使用 HID 设备堆栈报告的 TLCs。

## <a name="header-and-library-requirements"></a>标头和库要求

此过程介绍如何编写简单的 HID 源驱动程序，用于向操作系统报告耳机式按钮。 在这种情况下，实现此代码的驱动程序可以是一个现有的 KMDF 音频驱动程序，该驱动程序已通过使用 VHF 修改为作为 HID 源报表耳机按钮。

1.  包括在 Windows 10 中包含的 Vhf。
2.  指向包含在 WDK 中的 vhfkm 的链接。
3.  创建您的设备要向操作系统报告的 HID 报告描述符。 在此示例中，HID 报表描述符描述了耳机按钮。 报表指定 HID 输入报告，大小为8位 (1 字节) 。 前三个位用于耳机中间、调高音量和调低音量按钮。 剩余的位未使用。

```cpp
UCHAR HeadSetReportDescriptor[] = {
    0x05, 0x01,         // USAGE_PAGE (Generic Desktop Controls)
    0x09, 0x0D,         // USAGE (Portable Device Buttons)
    0xA1, 0x01,         // COLLECTION (Application)
    0x85, 0x01,         //   REPORT_ID (1)
    0x05, 0x09,         //   USAGE_PAGE (Button Page)
    0x09, 0x01,         //   USAGE (Button 1 - HeadSet : middle button)
    0x09, 0x02,         //   USAGE (Button 2 - HeadSet : volume up button)
    0x09, 0x03,         //   USAGE (Button 3 - HeadSet : volume down button)
    0x15, 0x00,         //   LOGICAL_MINIMUM (0)
    0x25, 0x01,         //   LOGICAL_MAXIMUM (1)
    0x75, 0x01,         //   REPORT_SIZE (1)
    0x95, 0x03,         //   REPORT_COUNT (3)
    0x81, 0x02,         //   INPUT (Data,Var,Abs)
    0x95, 0x05,         //   REPORT_COUNT (5)
    0x81, 0x03,         //   INPUT (Cnst,Var,Abs)
    0xC0,               // END_COLLECTION
};
```

## <a name="create-a-virtual-hid-device"></a>创建虚拟 HID 设备

调用 [**VHF \_ config \_ INIT**](/windows-hardware/drivers/ddi/vhf/nf-vhf-vhf_config_init)宏，然后调用 [**VhfCreate**](/windows-hardware/drivers/ddi/vhf/nf-vhf-vhfcreate)方法，初始化 [**VHF \_ 配置**](/windows-hardware/drivers/ddi/vhf/ns-vhf-_vhf_config)结构。 驱动程序必须 \_ 在 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)调用之后（通常是在驱动程序的 [*EVTDRIVERDEVICEADD*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数中）在被动级别调用 VhfCreate。

在 [**VhfCreate**](/windows-hardware/drivers/ddi/vhf/nf-vhf-vhfcreate) 调用中，驱动程序可以指定某些配置选项，如必须异步处理的操作，或者)  (供应商/产品 id 设置设备信息。

例如，应用程序请求 TLC。 当 HID 类驱动程序对接收该请求时，对将确定请求的类型，并创建相应的 [HID 微型驱动程序 IOCTL](/windows-hardware/drivers/ddi/_hid/#hid-minidriver-ioctls) 请求，并将其转发给 VHF。 获取 IOCTL 请求后，VHF 可以处理该请求，依赖于 HID 源驱动程序来处理该请求，或完成状态为 "不支持" 的请求 \_ \_ 。

VHF 处理以下 IOCTLs：

-   [**IOCTL \_ HID \_ 获取 \_ 字符串**](/windows-hardware/drivers/ddi/hidport/ni-hidport-ioctl_hid_get_string)
-   [**IOCTL \_ HID \_ 获取 \_ 设备 \_ 属性**](/windows-hardware/drivers/ddi/hidport/ni-hidport-ioctl_hid_get_device_attributes)
-   [**IOCTL \_ HID \_ 获取 \_ 设备 \_ 描述符**](/windows-hardware/drivers/ddi/hidport/ni-hidport-ioctl_hid_get_device_descriptor)
-   [**IOCTL \_ HID \_ 获取 \_ 报告 \_ 描述符**](/windows-hardware/drivers/ddi/hidport/ni-hidport-ioctl_hid_get_report_descriptor)

如果请求为 **GetFeature**、 **SetFeature**、 **WRITEREPORT** 或 **GetInputReport**，并且 HID 源驱动程序注册了相应的回调函数，则 VHF 将调用回调函数。 在该函数中，HID 源驱动程序可以获取或设置 HID 虚拟设备的 HID 数据。 如果驱动程序未注册回调，则 VHF 完成状态为 "不支持" 的请求 \_ \_ 。

VHF 为这些 IOCTLs 调用 HID 源驱动程序实现的事件回调函数：

-   [**IOCTL \_ HID \_ 读取 \_ 报告**](/windows-hardware/drivers/ddi/hidport/ni-hidport-ioctl_hid_read_report)

    如果驱动程序要在提交缓冲区以获取 HID 输入报告时处理缓冲策略，则它必须实现 [*EvtVhfReadyForNextReadReport*](/windows-hardware/drivers/ddi/vhf/nc-vhf-evt_vhf_ready_for_next_read_report) ，并在 **EvtVhfAsyncOperationGetInputReport** 成员中指定一个指针。 有关详细信息，请参阅 [提交 HID 输入报告](#submit-the-hid-input-report)。

-   [**IOCTL \_HID \_ 获取 \_ 功能**](/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_get_feature)或 [ **IOCTL \_ HID \_ 集 \_ 功能**](/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_set_feature)

    如果驱动程序要以异步方式获取或设置 HID 功能报表，则驱动程序必须实现 [*EvtVhfAsyncOperation*](/windows-hardware/drivers/ddi/vhf/nc-vhf-evt_vhf_async_operation)函数，并在 [**VHF \_ CONFIG**](/windows-hardware/drivers/ddi/vhf/ns-vhf-_vhf_config)的 **EvtVhfAsyncOperationGetFeature** 或 **EvtVhfAsyncOperationSetFeature** 成员中指定指向 get 或 set 实现函数的指针。

-   [**IOCTL \_ HID \_ 获取 \_ 输入 \_ 报告**](/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_get_input_report)

    如果驱动程序要以异步方式获取 HID 输入报告，驱动程序必须实现 [*EvtVhfAsyncOperation*](/windows-hardware/drivers/ddi/vhf/nc-vhf-evt_vhf_async_operation)函数，并在 [**VHF \_ CONFIG**](/windows-hardware/drivers/ddi/vhf/ns-vhf-_vhf_config)的 **EvtVhfAsyncOperationGetInputReport** 成员中指定指向函数的指针。

-   [**IOCTL \_ HID \_ 写入 \_ 报告**](/windows-hardware/drivers/ddi/hidport/ni-hidport-ioctl_hid_write_report)

    如果驱动程序要以异步方式写入 HID 输入报告，驱动程序必须实现 [*EvtVhfAsyncOperation*](/windows-hardware/drivers/ddi/vhf/nc-vhf-evt_vhf_async_operation)函数，并在 [**VHF \_ CONFIG**](/windows-hardware/drivers/ddi/vhf/ns-vhf-_vhf_config)的 **EvtVhfAsyncOperationWriteReport** 成员中指定指向函数的指针。

对于任何其他 [HID 微型驱动程序 IOCTL](/windows-hardware/drivers/ddi/index)，VHF 完成请求，状态 \_ 不 \_ 受支持。

虚拟 HID 设备通过调用 [**VhfDelete**](/windows-hardware/drivers/ddi/vhf/nf-vhf-vhfdelete)来删除。 如果驱动程序为虚拟 HID 设备分配了资源，则需要 [*EvtVhfCleanup*](/windows-hardware/drivers/ddi/vhf/nc-vhf-evt_vhf_cleanup) 回调。 驱动程序必须实现 *EvtVhfCleanup* 函数，并在 [**VHF \_ CONFIG**](/windows-hardware/drivers/ddi/vhf/ns-vhf-_vhf_config)的 **EvtVhfCleanup** 成员中指定指向此函数的指针。 在 **VhfDelete** 调用完成之前调用 *EvtVhfCleanup* 。 有关详细信息，请参阅 [删除虚拟 HID 设备](#delete-the-virtual-hid-device)。

**注意**  异步操作完成后，驱动程序必须调用 [**VhfAsyncOperationComplete**](/windows-hardware/drivers/ddi/vhf/nf-vhf-vhfasyncoperationcomplete) 来设置操作的结果。 你可以从事件回调调用方法，或在稍后从回调返回后调用方法。

```cpp
NTSTATUS
VhfSourceCreateDevice(
_Inout_ PWDFDEVICE_INIT DeviceInit
)

{
    WDF_OBJECT_ATTRIBUTES   deviceAttributes;
    PDEVICE_CONTEXT deviceContext;
    VHF_CONFIG vhfConfig;
    WDFDEVICE device;
    NTSTATUS status;

    PAGED_CODE();

    WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&deviceAttributes, DEVICE_CONTEXT);
    deviceAttributes.EvtCleanupCallback = VhfSourceDeviceCleanup;

    status = WdfDeviceCreate(&DeviceInit, &deviceAttributes, &device);

    if (NT_SUCCESS(status))
    {
        deviceContext = DeviceGetContext(device);

        VHF_CONFIG_INIT(&vhfConfig,
            WdfDeviceWdmGetDeviceObject(device),
            sizeof(VhfHeadSetReportDescriptor),
            VhfHeadSetReportDescriptor);

        status = VhfCreate(&vhfConfig, &deviceContext->VhfHandle);

        if (!NT_SUCCESS(status)) {
            TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, "VhfCreate failed %!STATUS!", status);
            goto Error;
        }

        status = VhfStart(deviceContext->VhfHandle);
        if (!NT_SUCCESS(status)) {
            TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, "VhfStart failed %!STATUS!", status);
            goto Error;
        }

    }

Error:
    return status;
}
```

## <a name="submit-the-hid-input-report"></a>提交 HID 输入报告

通过调用 [**VhfReadReportSubmit**](/windows-hardware/drivers/ddi/vhf/nf-vhf-vhfreadreportsubmit)提交 HID 输入报告。

通常，HID 设备通过中断发送输入报告来发送有关状态更改的信息。 例如，在按钮的状态发生更改时，耳机设备可能会发送报表。 在这种情况下，将调用驱动程序的中断服务例程 (ISR) 。 在这种情况下，驱动程序可能会计划延迟的过程调用 (DPC) 处理输入报告，并将其提交到 VHF，这会将信息发送到操作系统。 默认情况下，VHF 会缓冲报表，并且 HID 源驱动程序可以在其传入时开始提交 HID 输入报告。 这样就不再需要 HID 源驱动程序来实现复杂的同步。

HID 源驱动程序可以通过实现挂起报表的缓冲策略来提交输入报告。 若要避免重复的缓冲，HID 源驱动程序可以实现 [*EvtVhfReadyForNextReadReport*](/windows-hardware/drivers/ddi/vhf/nc-vhf-evt_vhf_ready_for_next_read_report) 回调函数并跟踪 VHF 是否调用了此回调。 如果先前调用了它，则 HID 源驱动程序可以调用 [**VhfReadReportSubmit**](/windows-hardware/drivers/ddi/vhf/nf-vhf-vhfreadreportsubmit) 来提交报告。 它必须等待 *EvtVhfReadyForNextReadReport* 调用，然后才能再次调用 **VhfReadReportSubmit** 。

```cpp
VOID
MY_SubmitReadReport(
    PMY_CONTEXT  Context,
    BUTTON_TYPE  ButtonType,
    BUTTON_STATE ButtonState
    )
{
    PDEVICE_CONTEXT deviceContext = (PDEVICE_CONTEXT)(Context);

    if (ButtonState == ButtonStateUp) {
        deviceContext->VhfHidReport.ReportBuffer[0] &= ~(0x01 << ButtonType);
    } else {
        deviceContext->VhfHidReport.ReportBuffer[0] |=  (0x01 << ButtonType);
    }

    status = VhfSubmitReadReport(deviceContext->VhfHandle, &deviceContext->VhfHidReport);

    if (!NT_SUCCESS(status)) {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE,"VhfSubmitReadReport failed %!STATUS!", status);
    }
}
```

## <a name="delete-the-virtual-hid-device"></a>删除虚拟 HID 设备

通过调用 [**VhfDelete**](/windows-hardware/drivers/ddi/vhf/nf-vhf-vhfdelete)删除虚拟 HID 设备。

通过指定 Wait 参数，可以同步或异步调用 [**VhfDelete**](/windows-hardware/drivers/ddi/vhf/nf-vhf-vhfdelete) 。 对于同步调用，必须在被动级别（例如 \_ ，从设备对象的 [*EvtCleanupCallback*](/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup) 中）调用方法。 删除虚拟 HID 设备后， **VhfDelete** 返回。 如果驱动程序以异步方式调用 **VhfDelete** ，则它会立即返回，并且 VHF 将在删除操作完成后调用 [*EvtVhfCleanup*](/windows-hardware/drivers/ddi/vhf/nc-vhf-evt_vhf_cleanup) 。 可在最大调度级别调用方法 \_ 。 在这种情况下，驱动程序必须已注册，并在以前调用 [**VhfCreate**](/windows-hardware/drivers/ddi/vhf/nf-vhf-vhfcreate)时实现了 *EvtVhfCleanup* 回调函数。 下面是 HID 源驱动程序要删除虚拟 HID 设备时的事件序列：

1.  HID 源驱动程序停止启动对 VHF 的调用。
2.  HID 源调用 [**VhfDelete**](/windows-hardware/drivers/ddi/vhf/nf-vhf-vhfdelete) ，并将 *WAIT* 设置为 FALSE。
3.  VHF 停止调用由 HID 源驱动程序实现的回调函数。
4.  VHF 开始将设备报告为 PnP 管理器丢失。 此时，VhfDelete 调用可能会返回。
5.  将设备报告为缺少设备时，如果 HID 源驱动程序已注册其实现，VHF 将调用 [*EvtVhfCleanup*](/windows-hardware/drivers/ddi/vhf/nc-vhf-evt_vhf_cleanup) 。
6.  [*EvtVhfCleanup*](/windows-hardware/drivers/ddi/vhf/nc-vhf-evt_vhf_cleanup)返回后，VHF 将执行其清理。

```cpp
VOID
VhfSourceDeviceCleanup(
_In_ WDFOBJECT DeviceObject
)
{
    PDEVICE_CONTEXT deviceContext;

    PAGED_CODE();

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DEVICE, "%!FUNC! Entry");

    deviceContext = DeviceGetContext(DeviceObject);

    if (deviceContext->VhfHandle != WDF_NO_HANDLE)
    {
        VhfDelete(deviceContext->VhfHandle, TRUE);
    }

}
```

## <a name="install-the-hid-source-driver"></a>安装 HID 源驱动程序

在安装 HID 源驱动程序的 INF 文件中，请确保使用 [**AddReg 指令**](../install/inf-addreg-directive.md)将 Vhf.sys 声明为降级到 HID 源驱动程序的筛选器驱动程序。

```cpp
[HIDVHF_Inst.NT.HW]
AddReg = HIDVHF_Inst.NT.AddReg

[HIDVHF_Inst.NT.AddReg]
HKR,,"LowerFilters",0x00010000,"vhf"
```

## <a name="related-topics"></a>相关主题
[人体学接口设备](https://developer.microsoft.com/windows/hardware)
