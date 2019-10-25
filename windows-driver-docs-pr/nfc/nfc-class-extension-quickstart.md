---
title: NFC CX 快速入门指南
author: EliotSeattle
description: 使用 NFC 类扩展编写 NFC 功能驱动程序的快速入门指南。
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
- CX
ms.author: eliotgra
ms.date: 12/10/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: low
ms.openlocfilehash: c335cf7386a33fddbe11316b5727938e12065191
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831892"
---
# <a name="nfc-cx-quick-start-guide"></a>NFC CX 快速入门指南

本指南演示如何使用 NFC 类扩展（NFC CX）驱动程序编写 NFC 功能驱动程序。

> [!NOTE]
> 在其实现中使用类扩展驱动程序的驱动程序称为 "客户端驱动程序"。 这就是类扩展驱动程序的客户端。

## <a name="prerequisites"></a>必备条件

* NFC 控制器的固件必须实现 NFC 论坛的[Nfc 控制器接口（NCI）](https://nfc-forum.org/our-work/specifications-and-application-documents/specifications/nfc-controller-interface-nci-specification/)协议。
* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_content=download+vs2017) （或更高版本）。
* [Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk)。
* [Windows 10 驱动程序工具包（WDK）](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)。

## <a name="client-driver-responsibilities"></a>客户端驱动程序责任

NFC CX 驱动程序负责处理发送到驱动程序的 i/o 请求，并创建相关的 NCI 命令包。 客户端驱动程序负责将这些 NCI 数据包发送到 NFC 控制器，并将 NCI 响应数据包发送回 NFC CX 驱动程序。

这取决于客户端驱动程序，确定如何将 NCI 数据包发送到 NFC 控制器。 这取决于所使用的硬件总线类型。 NFC 控制器使用的常见总线包括 I<sup>2</sup>C、SPI 和 USB。

## <a name="complete-project-code"></a>完成项目代码

GitHub 上提供了此示例代码的完整版本： [NFC CX 客户端驱动程序示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/nfc/NfcCxSample)。

## <a name="project-setup"></a>项目设置

1. 在 Visual Studio 中，创建一个新的 "用户模式驱动程序，空（UMDF V2）" 项目。

    在 "**文件**" 菜单上，指向 "**新建**"，然后单击 "**项目**"。 在**可视化C++** 节点的 " **Windows 驱动程序**" 下，单击 " **WDF**"，然后单击 "**用户模式驱动程序"，空（UMDF V2）**

    ![image](images/quick-start-new-project.png)

2. 打开 INF 文件。

   在**解决方案资源管理器**的 " **\<项目-名称 >** " 节点下的 "**驱动程序文件**" 文件夹中，双击 **\<项目名称 >** 。

3. 在 INF 文件中，使用以下步骤删除自定义设备类：

    1. 删除以下两部分：

        ```inf
        [ClassInstall32]
        AddReg=SampleClass_RegistryAdd

        [SampleClass_RegistryAdd]
        HKR,,,,%ClassName%
        HKR,,Icon,,"-10"
        ```

    2. 在 `[Strings]` 部分中，删除以下行。 

        ```inf
        ClassName="Samples" ; TODO: edit ClassName
        ```

4. 在 INF 文件中，将驱动程序的设备类设置为**邻近**：

    1. 将 `Class` 的值更改为 `Proximity`
    2. 将 `ClassGuid` 的值更改为 `{5630831C-06C9-4856-B327-F5D32586E060}`
        - 这是邻近感应设备类的 GUID。

    ```ini
    [Version]
    ...
    Class=Proximity
    ClassGuid={5630831C-06C9-4856-B327-F5D32586E060} ; Proximity class GUID
    ...
    ```

5. 在 INF 文件中，添加对 NFC 类扩展的引用。 这样做可确保在客户端驱动程序加载时 Windows 驱动程序框架（WDF）将加载 NFC CX 驱动程序。
  
    1. 找到 `<project-name>_Install` 部分。
    2. 添加 `UmdfExtensions=NfcCx0102`。

    ```ini
    [<project-name>_Install]
    ...
    UmdfExtensions=NfcCx0102
    ```

6. 在 "驱动程序生成设置" 中，链接到 NFC 类扩展。 这样做可确保 NFC CX API 在代码编译期间可用。

    1. 在**解决方案资源管理器**中，右键单击项目，然后单击 "**属性**"。 在 "**配置属性**" 的 "**驱动程序设置**" 下，单击 " **NFC**"。
    2. 确保**配置**设置为 `All Configurations`。
    3. 确保将**平台**设置为 `All Platforms`。
    4. 设置**要 `Yes`的 NFC 类扩展的链接**。

    ![image](images/quick-start-link-to-nfc-cx.png)

7. 将名为 `Driver.cpp` 的文件添加到项目。

8. 在 `Driver.cpp`中创建 `DriverEntry` 例程。 这是驱动程序的入口点。 它的主要用途是初始化 WDF 并注册[`EvtDriverDeviceAdd`](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数。

    ```cpp
    #include <windows.h>
    #include <wdf.h>

    #include "Device.h" // created in Step 9

    // The entry point for the driver.
    extern "C" NTSTATUS DriverEntry(
        _In_ PDRIVER_OBJECT DriverObject,
        _In_ PUNICODE_STRING RegistryPath
        )
    {
        NTSTATUS status = STATUS_SUCCESS;

        // Specify `DeviceContext::AddDevice` as the 
        // `EvtDriverDeviceAdd` function for the driver.
        WDF_DRIVER_CONFIG driverConfig;
        WDF_DRIVER_CONFIG_INIT(&driverConfig, DeviceContext::AddDevice);

        // Initialize WDF.
        status = WdfDriverCreate(
            DriverObject,
            RegistryPath,
            WDF_NO_OBJECT_ATTRIBUTES,
            &driverConfig,
            WDF_NO_HANDLE);
        if (!NT_SUCCESS(status))
        {
            return status;
        }

        return STATUS_SUCCESS;
    }
    ```

9. 将名为 `Device.cpp` 和 `Device.h` 的两个文件添加到项目。

10. 在 `Device.h`中，定义 `DeviceContext` 类。

    ```cpp
    #pragma once

    #include <windows.h>
    #include <wdf.h>
    #include <NfcCx.h>

    // The class that will store the driver's custom state for
    // a device instance.
    class DeviceContext
    {
    public:
        // Implementation of `EvtDriverDeviceAdd`.
        static NTSTATUS AddDevice(
            _In_ WDFDRIVER Driver,
            _Inout_ PWDFDEVICE_INIT DeviceInit);

    private:
        // Implementation of `EvtDevicePrepareHardware`.
        static NTSTATUS PrepareHardware(
            _In_ WDFDEVICE Device,
            _In_ WDFCMRESLIST ResourcesRaw,
            _In_ WDFCMRESLIST ResourcesTranslated);

        // Implementation of `EvtDeviceReleaseHardware`.
        static NTSTATUS ReleaseHardware(
            _In_ WDFDEVICE Device,
            _In_ WDFCMRESLIST ResourcesTranslated);

        // Implementation of `EvtDeviceD0Entry`.
        static NTSTATUS D0Entry(
            _In_ WDFDEVICE Device,
            _In_ WDF_POWER_DEVICE_STATE PreviousState);

        // Implementation of `EvtDeviceD0Exit`.
        static NTSTATUS D0Exit(
            _In_ WDFDEVICE Device,
            _In_ WDF_POWER_DEVICE_STATE TargetState);

        // Implementation of `EvtNfcCxWriteNciPacket`.
        static void WriteNciPacket(
            _In_ WDFDEVICE Device,
            _In_ WDFREQUEST Request);
    };

    // Define the `DeviceGetContext` function.
    WDF_DECLARE_CONTEXT_TYPE_WITH_NAME(DeviceContext, DeviceGetContext);
    ```

11. 在 `Device.cpp`中，开始 `DeviceContext::AddDevice` 函数的定义。

    ```cpp
    #include "Device.h"

    NTSTATUS DeviceContext::AddDevice(
        _In_ WDFDRIVER Driver,
        _Inout_ PWDFDEVICE_INIT DeviceInit)
    {
        NTSTATUS status;

    ```

12. 设置 NFC CX 设备配置。 设备配置包括提供[`EvtNfcCxWriteNciPacket`](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nc-nfccx-evt_nfc_cx_write_nci_packet)回调函数。 此回调从 NFC CX 驱动程序接收来自客户端驱动程序应转发到 NFC 控制器的 NCI 数据包。

    ```cpp
        // Create the NfcCx config.
        NFC_CX_CLIENT_CONFIG nfcCxConfig;
        NFC_CX_CLIENT_CONFIG_INIT(&nfcCxConfig, NFC_CX_TRANSPORT_CUSTOM);
        nfcCxConfig.EvtNfcCxWriteNciPacket = WriteNciPacket;
        nfcCxConfig.DriverFlags = NFC_CX_DRIVER_ENABLE_EEPROM_WRITE_PROTECTION;

        // Set the NfcCx config.
        status = NfcCxDeviceInitConfig(DeviceInit, &nfcCxConfig);
        if (!NT_SUCCESS(status))
        {
            return status;
        }
    ```

13. 注册客户端驱动程序所需的[PnP 电源回调](https://docs.microsoft.com/windows-hardware/drivers/wdf/supporting-pnp-and-power-management-in-function-drivers)。

    典型的客户端驱动程序可能需要[`EvtDevicePrepareHardware`](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)、 [`EvtDeviceReleaseHardware`](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)、 [`EvtDeviceD0Entry`](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)和[`EvtDeviceD0Exit`](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)函数。 根据客户端驱动程序处理电源管理的方式，要求可能有所不同。

    ```cpp
        // Create the PnP power callbacks configuration.
        WDF_PNPPOWER_EVENT_CALLBACKS pnpCallbacks;
        WDF_PNPPOWER_EVENT_CALLBACKS_INIT(&pnpCallbacks);
        pnpCallbacks.EvtDevicePrepareHardware = PrepareHardware;
        pnpCallbacks.EvtDeviceReleaseHardware = ReleaseHardware;
        pnpCallbacks.EvtDeviceD0Entry = D0Entry;
        pnpCallbacks.EvtDeviceD0Exit = D0Exit;

        // Set the PnP power callbacks.
        WdfDeviceInitSetPnpPowerEventCallbacks(DeviceInit, &pnpCallbacks);
    ```

14. 调用[`WdfDeviceCreate`](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)函数以创建[`WDFDEVICE`](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/)对象。

    ```cpp
        // Create WDF object attributes for the WDFDEVICE object.
        WDF_OBJECT_ATTRIBUTES deviceAttributes;
        WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&deviceAttributes, DeviceContext);

        // Create the device.
        WDFDEVICE device;
        status = WdfDeviceCreate(&DeviceInit, &deviceAttributes, &device);
        if (!NT_SUCCESS(status))
        {
            return status;
        }
    ```

15. 调用[`NfcCxDeviceInitialize`](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxdeviceinitialize)函数。

    创建[`WDFDEVICE`](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/)对象后，应调用此函数以允许 NFC CX 驱动程序完成其设备实例的初始化。

    ```cpp
        // Let NFC CX finish initializing the device instance.
        status = NfcCxDeviceInitialize(device);
        if (!NT_SUCCESS(status))
        {
            return status;
        }
    ```

16. 调用[`NfcCxSetRfDiscoveryConfig`](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxsetrfdiscoveryconfig)以指定 nfc 控制器支持的 nfc 技术和协议。

    ```cpp
        // Create the RF config. (Enable everything.)
        NFC_CX_RF_DISCOVERY_CONFIG discoveryConfig;
        NFC_CX_RF_DISCOVERY_CONFIG_INIT(&discoveryConfig);
        discoveryConfig.PollConfig =
            NFC_CX_POLL_NFC_A | NFC_CX_POLL_NFC_B |
            NFC_CX_POLL_NFC_F_212 | NFC_CX_POLL_NFC_F_424 |
            NFC_CX_POLL_NFC_15693 | NFC_CX_POLL_NFC_ACTIVE |
            NFC_CX_POLL_NFC_A_KOVIO;
        discoveryConfig.NfcIPMode =
            NFC_CX_NFCIP_NFC_A | NFC_CX_NFCIP_NFC_F_212 |
            NFC_CX_NFCIP_NFC_F_424 | NFC_CX_NFCIP_NFC_ACTIVE |
            NFC_CX_NFCIP_NFC_ACTIVE_A | NFC_CX_NFCIP_NFC_ACTIVE_F_212 |
            NFC_CX_NFCIP_NFC_ACTIVE_F_424;
        discoveryConfig.NfcIPTgtMode =
            NFC_CX_NFCIP_TGT_NFC_A | NFC_CX_NFCIP_TGT_NFC_F |
            NFC_CX_NFCIP_TGT_NFC_ACTIVE_A | NFC_CX_NFCIP_TGT_NFC_ACTIVE_F;
        discoveryConfig.NfcCEMode =
            NFC_CX_CE_NFC_A | NFC_CX_CE_NFC_B |
            NFC_CX_CE_NFC_F;

        // Set the RF config.
        status = NfcCxSetRfDiscoveryConfig(device, &discoveryConfig);
        if (!NT_SUCCESS(status))
        {
            return status;
        }
    ```

17. 结束 `DeviceContext::AddDevice` 函数。

    ```cpp
        return STATUS_SUCCESS;
    }
    ```

18. 实现[`PrepareHardware`](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)和[`ReleaseHardware`](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)回调函数。

    这两个函数用于初始化和取消初始化分配给 NFC 控制器的设备实例的硬件资源。 其实现取决于设备连接到的总线类型（例如，I<sup>2</sup>C、SPI 和 USB）。

    ```cpp
    NTSTATUS DeviceContext::PrepareHardware(
        _In_ WDFDEVICE Device,
        _In_ WDFCMRESLIST ResourcesRaw,
        _In_ WDFCMRESLIST ResourcesTranslated)
    {
        // FIX ME: Initialize hardware resources.
        return STATUS_SUCCESS;
    }

    NTSTATUS DeviceContext::ReleaseHardware(
        _In_ WDFDEVICE Device,
        _In_ WDFCMRESLIST ResourcesTranslated)
    {
        // FIX ME: Uninitialize hardware resources.
        return STATUS_SUCCESS;
    }
    ```

19. 调用[`NfcCxHardwareEvent`](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxhardwareevent)函数与[`HostActionStart`](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/ne-nfccx-_nfc_cx_host_action) ，并[`HostActionStop`](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/ne-nfccx-_nfc_cx_host_action)在适当的时间启动和停止 NCI 状态机。

    某些驱动程序在[`D0Entry`](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)期间执行此操作，并[`D0Exit`](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit) PnP 电源回调。 但这可能会因客户端驱动程序处理电源管理的情况而有所不同。

    ```cpp
    // Device exiting low power state (or is booting up).
    NTSTATUS DeviceContext::D0Entry(
        _In_ WDFDEVICE Device,
        _In_ WDF_POWER_DEVICE_STATE PreviousState)
    {
        (void)PreviousState;

        NTSTATUS status;

        // Invoke the HostActionStart event, so that the NFC CX initializes
        // the NFC Controller.
        NFC_CX_HARDWARE_EVENT eventArgs = {};
        eventArgs.HostAction = HostActionStart;

        status = NfcCxHardwareEvent(Device, &eventArgs);
        if (!NT_SUCCESS(status))
        {
            return status;
        }

        return STATUS_SUCCESS;
    }

    // Device entering low power state.
    NTSTATUS DeviceContext::D0Exit(
        _In_ WDFDEVICE Device,
        _In_ WDF_POWER_DEVICE_STATE TargetState)
    {
        (void)TargetState;

        NTSTATUS status;

        // Trigger the HostActionStop event, so that the NFC CX
        // uninitializes the NFC Controller.
        NFC_CX_HARDWARE_EVENT eventArgs = {};
        eventArgs.HostAction = HostActionStop;

        status = NfcCxHardwareEvent(Device, &eventArgs);
        if (!NT_SUCCESS(status))
        {
            return status;
        }

        return STATUS_SUCCESS;
    }
    ```

20. 实现[`WriteNciPacket`](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nc-nfccx-evt_nfc_cx_write_nci_packet)函数。

    当存在要发送到 NFC 控制器的 NCI 数据包时，NFC CX 会调用此回调。

    ```cpp
    void DeviceContext::WriteNciPacket(
        _In_ WDFDEVICE Device,
        _In_ WDFREQUEST Request)
    {
        NTSTATUS status;

        // Get the NCI packet as a raw byte buffer.
        void* nciPacket;
        size_t nciPacketLength;
        status = WdfRequestRetrieveInputBuffer(Request, 0, &nciPacket, &nciPacketLength);
        if (!NT_SUCCESS(status))
        {
            WdfRequestComplete(Request, status);
            return;
        }

        // FIX ME: Use the NCI packet in some way.

        // FIX ME: Call `WdfRequestComplete` on `Request` with failure 
        // or success `NTSTATUS` code.
    };
    ```

21. 当 NFC 控制器具有应发送到 NFC CX 的 NCI 数据包时，调用[`NfcCxNciReadNotification`](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxncireadnotification)函数。 通常在硬件事件回调中完成此操作。

    例如：
    - [GPIO 中断](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-interrupts)事件回调。 （I<sup>2</sup>C 和 SPI）
    - [USB 连续读取器](https://docs.microsoft.com/windows-hardware/drivers/usbcon/how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-)回调。

## <a name="logging"></a>日志记录

请考虑将日志记录添加到客户端驱动程序，以便更轻松地进行调试。 [ETW 跟踪](https://docs.microsoft.com/windows-hardware/drivers/devtest/event-tracing-for-windows--etw-)和[WPP 跟踪](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)都是不错的选择。
