---
title: 使用虚拟 HID Framework (VHF) 编写的 HID 源驱动程序
description: 了解如何对操作系统编写的 HID 源驱动程序报告 HID 数据。
ms.assetid: 26964963-792F-4529-B4FC-110BF5C65B35
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92286f38db7ec35cd94b6f64f2ab7ac8fdd4a539
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524721"
---
# <a name="write-a-hid-source-driver-by-using-virtual-hid-framework-vhf"></a>使用虚拟 HID Framework (VHF) 编写的 HID 源驱动程序

**摘要**

-   编写将 HID 阅读的报告提交给操作系统的内核模式驱动程序框架 (KMDF) HID 源驱动程序。
-   为虚拟的 HID 设备堆栈中的 HID 源驱动程序到较低的筛选器中加载 VHF 驱动程序。

**适用于**

-   Windows 10
-   HID 设备的驱动程序开发人员

**重要的 Api**

-   [虚拟 HID Framework 回调函数](https://msdn.microsoft.com/library/windows/hardware/dn925049)
-   [虚拟 HID Framework 方法](https://msdn.microsoft.com/library/windows/hardware/dn925053)
-   [虚拟 HID 框架结构](https://msdn.microsoft.com/library/windows/hardware/dn925054)

了解如何对操作系统编写的 HID 源驱动程序报告 HID 数据。

Hid 标准的输入的设备，如-键盘、 鼠标、 笔、 触摸屏输入或按钮，将发送各种报告到操作系统，以便它可以了解设备的用途并采取必要措施。 报表是中的窗体[HID 集合](opening-hid-collections.md)并[HID 用法](hid-usages.md)。 设备通过各种不同的传输，其中一些如支持的 Windows，将发送这些报表[HID over I2C](hid-over-i2c-guide.md)并[通过 USB HID](hid-over-usb.md)。 在某些情况下，Windows，可能不支持传输或报表可能会不直接映射到的真实硬件。 它可以是 HID 格式，例如，对于非 GPIO 按钮或传感器的虚拟硬件另一个软件组件发送的数据的流。 例如，考虑为游戏控制器，以无线方式发送到电脑的方式运行的电话中的加速感应器数据。 在另一个示例中，计算机可以从支持 Miracast 的设备接收远程输入，通过使用 UIBC 协议。

在以前版本的 Windows 中，以支持新的传输 （的真实硬件或软件），您必须编写[HID 传输微型驱动程序](transport-minidrivers.md)并将其绑定到由 Microsoft 提供的内置类驱动程序，Hidclass.sys。 类/微型驱动程序对提供的 HID 集合，如[顶级集合](top-level-collections.md)别的驱动程序和用户模式应用程序。 在该模型中，这一难题编写微型驱动程序，可以是复杂的任务。

从 Windows 10 开始，新虚拟 HID Framework (VHF) 消除了需要写入传输微型驱动程序。 而是可以使用 KMDF 或 WDM 编程接口来编写 HID 源驱动程序。 该框架包括由 Microsoft 提供的静态库公开所使用的驱动程序的编程元素。 它还包括由 Microsoft 提供的现成驱动程序枚举一个或多个子设备并继续将构建和管理虚拟 HID 树。

**请注意**  VHF 在此版本中，支持仅在内核模式下的 HID 源驱动程序。

本主题介绍的体系结构框架、 虚拟 HID 设备树中，以及配置方案。

## <a name="virtual-hid-device-tree"></a>虚拟 HID 设备树

在此图中，设备树显示的驱动程序和其关联的设备对象。

![虚拟的 hid 的设备树](images/vhf.png)

**HID 的源驱动程序 （您的驱动程序）**

HID 源驱动程序链接到 Vhfkm.lib 和 Vhf.h 包括在其生成的项目。 该驱动程序可以编写通过使用[Windows 驱动程序模型](https://msdn.microsoft.com/library/windows/hardware/ff565698)(WDM) 或内核模式驱动程序框架 (KMDF) 的一部分[Windows 驱动程序框架 (WDF)](https://msdn.microsoft.com/library/windows/hardware/dn312126)。 为筛选器驱动程序或设备堆栈中的函数驱动程序可以加载驱动程序。

**VHF 静态库 (vhfkm.lib)**

静态库包含适用于 Windows 10 的 Windows Driver Kit (WDK) 中。 该库公开编程接口，如例程和 HID 源驱动程序使用的回调函数。 当您的驱动程序调用一个函数时，静态库将请求转发到 VHF 驱动程序处理请求。

**VHF 驱动程序 (Vhf.sys)**

Microsoft 提供的现成驱动程序。 此驱动程序必须为下面您 HID 源设备堆栈中的驱动程序的较低的筛选器驱动程序加载。 VHF 驱动程序动态枚举子设备，并创建一个或多个指定的 HID 源驱动程序的 HID 设备的物理设备对象 (PDO)。 它还实现枚举的子设备的 HID 传输微型驱动程序功能。

**HID 的类驱动程序对 （Hidclass.sys，Mshidkmdf.sys）**

Hidclass/Mshidkmdf 对枚举[顶级集合 (TLC)](top-level-collections.md)类似于它如何枚举真实的 HID 设备，这些集合。 HID 客户端可以继续请求和使用 TLCs 就像实际的 HID 设备一样。 此驱动程序对作为设备堆栈中的函数驱动程序安装。

**请注意**  HID 客户端可能需要在某些情况下，确定 HID 数据源。 例如，一个系统具有内置传感器，并从相同类型的远程传感器接收数据。 系统可能会想要选择一个传感器更可靠。 若要区分两个传感器连接到系统中，容器 ID 的 TLC HID 客户端查询。 在这种情况下，HID 源驱动程序可以提供容器 ID，它通过 VHF 报告为虚拟的 HID 设备的容器 ID。

**HID 客户端 （应用程序）**

查询并使用报告的 HID 设备堆栈 TLCs。

## <a name="header-and-library-requirements"></a>标头和库要求

此过程描述如何将简单的 HID 源驱动程序这些报表耳机按钮写入到操作系统。 在这种情况下，实现此代码的驱动程序可以是现有 KMDF 音频驱动程序的已修改为充当使用 VHF reporting 耳机按钮的 HID 源。

1.  包括 Vhf.h，包括在 Windows 10 的 WDK。
2.  链接到 vhfkm.lib，WDK 中包含。
3.  创建 HID 设备想要向操作系统报告的报告描述符。 在此示例中，HID 报表说明符所描述的耳机按钮。 报告指定 HID 输入报表，大小为 8 位 （1 个字节）。 前三个位是耳机中间、 卷向上和卷列表按钮。 剩余的位是未使用。

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

## <a name="create-a-virtual-hid-device"></a>创建一个虚拟的 HID 设备

初始化[ **VHF\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/dn925044)结构通过调用[ **VHF\_配置\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/dn925046)宏，然后调用[ **VhfCreate** ](https://msdn.microsoft.com/library/windows/hardware/dn925036)方法。 该驱动程序必须调用**VhfCreate**在被动\_级别后[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)调用，通常情况下，在驱动程序的[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调函数。

在中[ **VhfCreate** ](https://msdn.microsoft.com/library/windows/hardware/dn925036)调用时，该驱动程序可以指定某些配置选项，如必须是以异步方式处理或设置设备信息 （供应商/产品 Id） 的操作。

例如，应用程序请求 TLC。 HID 类驱动程序对接收该请求时，对确定请求的类型，并创建一个适当[HID 微型驱动程序 IOCTL](https://msdn.microsoft.com/library/windows/hardware/ff539926)请求并将其转发到 VHF。 后获取 IOCTL 请求，VHF 可以处理该请求、 依赖于 HID 源驱动程序来处理它，或完成状态为请求\_不\_受支持。

VHF 处理这些 Ioctl:

-   [**IOCTL\_HID\_GET\_STRING**](https://msdn.microsoft.com/library/windows/hardware/ff541167)
-   [**IOCTL\_HID\_GET\_DEVICE\_ATTRIBUTES**](https://msdn.microsoft.com/library/windows/hardware/ff541093)
-   [**IOCTL\_HID\_获取\_设备\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff541098)
-   [**IOCTL\_HID\_获取\_报表\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff541147)

该请求是否**GetFeature**， **SetFeature**， **WriteReport**，或者**GetInputReport**，并已注册的 HID 源驱动程序相应的回调函数，VHF 调用的回调函数。 在该函数的 HID 源驱动程序可以获取或设置 HID 虚拟设备的 HID 数据。 如果该驱动程序不会注册一个回调，VHF 完成状态为状态请求\_不\_受支持。

VHF 调用有这些 Ioctl HID 源驱动程序实现事件回调函数：

-   [**IOCTL\_HID\_读取\_报表**](https://msdn.microsoft.com/library/windows/hardware/ff541172)

    如果该驱动程序想要提交缓冲区获取 HID 输入报告时的句柄缓冲策略，它必须实现[ *EvtVhfReadyForNextReadReport* ](https://msdn.microsoft.com/library/windows/hardware/dn897135)并指定一个指针，在**EvtVhfAsyncOperationGetInputReport**成员。 有关详细信息，请参阅[提交 HID 输入报告](#submit)。

-   [**IOCTL\_HID\_获取\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff541103)或[ **IOCTL\_HID\_设置\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff541184)

    如果该驱动程序想要获取或设置 HID 功能报表以异步方式，该驱动程序必须实现[ *EvtVhfAsyncOperation* ](https://msdn.microsoft.com/library/windows/hardware/dn897133)函数和指定一个指向 get 或 set 实现函数**EvtVhfAsyncOperationGetFeature**或**EvtVhfAsyncOperationSetFeature**的成员[ **VHF\_配置**](https://msdn.microsoft.com/library/windows/hardware/dn925044).

-   [**IOCTL\_HID\_获取\_输入\_报表**](https://msdn.microsoft.com/library/windows/hardware/ff541128)

    如果该驱动程序想要以异步方式获取 HID 输入报表，该驱动程序必须实现[ *EvtVhfAsyncOperation* ](https://msdn.microsoft.com/library/windows/hardware/dn897133)函数，并指定到中的函数的指针**EvtVhfAsyncOperationGetInputReport**的成员[ **VHF\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/dn925044)。

-   [**IOCTL\_HID\_编写\_报表**](https://msdn.microsoft.com/library/windows/hardware/ff541221)

    如果该驱动程序想要以异步方式获取写入 HID 输入报表，该驱动程序必须实现[ *EvtVhfAsyncOperation* ](https://msdn.microsoft.com/library/windows/hardware/dn897133)函数，并指定到中的函数的指针**EvtVhfAsyncOperationWriteReport**的成员[ **VHF\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/dn925044)。

对于任何其他[HID 微型驱动程序 IOCTL](https://msdn.microsoft.com/library/windows/hardware/ff539926)，VHF 完成状态为请求\_不\_受支持。

通过调用删除虚拟的 HID 设备[ **VhfDelete**](https://msdn.microsoft.com/library/windows/hardware/dn925038)。 [ *EvtVhfCleanup* ](https://msdn.microsoft.com/library/windows/hardware/dn897134) callback 是必需的如果为虚拟的 HID 设备的驱动程序分配资源。 该驱动程序必须实现*EvtVhfCleanup*函数，并指定在该函数的指针**EvtVhfCleanup**的成员[ **VHF\_配置**](https://msdn.microsoft.com/library/windows/hardware/dn925044). *EvtVhfCleanup*之前调用**VhfDelete**调用完成。 有关详细信息，请参阅[删除虚拟 HID 设备](#delete-the-virtual-hid-device)。

**请注意**  驱动程序的异步操作完成后，必须调用[ **VhfAsyncOperationComplete** ](https://msdn.microsoft.com/library/windows/hardware/dn925060)设置操作的结果。 从事件回调或在以后从回调返回后，可以调用方法。

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

## <a name="submit-the-hid-input-report"></a>提交 HID 输入的报告

通过调用提交 HID 输入的报告[ **VhfReadReportSubmit**](https://msdn.microsoft.com/library/windows/hardware/dn925040)。

通常情况下，HID 设备发送的状态更改的信息发送输入的报告通过中断。 例如，耳机设备可能会发送报表，按钮的状态发生更改时。 在这种情况下，会调用驱动程序的中断服务例程 (ISR)。 在该例程中，该驱动程序可能会安排处理输入的报表，并将其提交给 VHF，将信息发送给系统的延迟的过程调用 (DPC)。 默认情况下，VHF 缓冲报表，HID 源驱动程序可以开始提交 HID 输入报表，因为它们进入。 这并不需要的 HID 源驱动程序来实现复杂的同步。

HID 源驱动程序可以通过实现挂起报告的缓冲策略提交输入的报表。 若要避免重复缓冲，HID 源驱动程序可以实现[ *EvtVhfReadyForNextReadReport* ](https://msdn.microsoft.com/library/windows/hardware/dn897135) VHF 是否调用此回调的回调函数，并保持跟踪。 如果以前调用的 HID 源驱动程序可以调用[ **VhfReadReportSubmit** ](https://msdn.microsoft.com/library/windows/hardware/dn925040)要提交报告。 它必须等待*EvtVhfReadyForNextReadReport*然后才能调用获取调用**VhfReadReportSubmit**试。

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

删除虚拟 HID 设备通过调用[ **VhfDelete**](https://msdn.microsoft.com/library/windows/hardware/dn925038)。

[**VhfDelete** ](https://msdn.microsoft.com/library/windows/hardware/dn925038)可以调用同步或异步指定 Wait 参数。 为同步调用，必须在调用方法在被动\_级别，例如从[ *EvtCleanupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540840)的设备对象。 **VhfDelete**虚拟 HID 设备中删除后返回。 如果该驱动程序调用**VhfDelete**异步，它会立即返回并调用 VHF [ *EvtVhfCleanup* ](https://msdn.microsoft.com/library/windows/hardware/dn897134)删除操作完成后。 该方法可以在最大调度调用\_级别。 在这种情况下，该驱动程序必须具有已注册并实现*EvtVhfCleanup*回调函数之前调用时[ **VhfCreate**](https://msdn.microsoft.com/library/windows/hardware/dn925036)。 下面是时 HID 源驱动程序想要删除虚拟 HID 设备的事件序列：

1.  HID 的源驱动程序将停止启动 VHF 调用。
2.  HID 的源调用[ **VhfDelete** ](https://msdn.microsoft.com/library/windows/hardware/dn925038)与*等待*设置为 FALSE。
3.  VHF 停止调用由 HID 源驱动程序实现的回调函数。
4.  VHF 开始报告该设备是缺少向即插即用管理器。 此时，可能会返回 VhfDelete 调用。
5.  当设备报告为丢失设备时，调用 VHF [ *EvtVhfCleanup* ](https://msdn.microsoft.com/library/windows/hardware/dn897134)如果 HID 源驱动程序已注册其实现。
6.  之后[ *EvtVhfCleanup* ](https://msdn.microsoft.com/library/windows/hardware/dn897134)返回 VHF 执行其清理。

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

## <a name="install-the-hid-source-driver"></a>安装的 HID 源驱动程序

在安装的 HID 源驱动程序的 INF 文件，请确保声明 Vhf.sys 作为较低的筛选器驱动程序到 HID 源驱动程序通过使用[ **AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)。

```cpp
[HIDVHF_Inst.NT.HW]
AddReg = HIDVHF_Inst.NT.AddReg

[HIDVHF_Inst.NT.AddReg]
HKR,,"LowerFilters",0x00010000,"vhf"
```

## <a name="related-topics"></a>相关主题
[人机接口设备](https://msdn.microsoft.com/library/windows/hardware/ff543301)

