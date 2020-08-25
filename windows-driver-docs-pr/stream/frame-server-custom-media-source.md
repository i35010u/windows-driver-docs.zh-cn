---
title: Frame Server 自定义媒体源
description: 提供有关在框架服务器体系结构内实现自定义媒体源的信息。
ms.date: 08/25/2020
ms.localizationpriority: medium
ms.openlocfilehash: bc6e2cbc863558a64ce8c74ea8f308f27be6e430
ms.sourcegitcommit: d9a9925f790271f4ca2c8377d551d96e8d1e62c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88850213"
---
# <a name="frame-server-custom-media-source"></a>Frame Server 自定义媒体源

本主题提供有关在框架服务器体系结构中实现自定义媒体源的信息。

## <a name="av-stream-and-custom-media-source-options"></a>AV 流和自定义媒体源选项

在确定如何在框架服务器体系结构内提供视频捕获流支持时，有两个主要选项： AV 流和自定义媒体源。

AV 流模型是标准相机驱动程序型号，使用 AV 流微型端口驱动程序 (内核模式驱动程序) 。 AV 流驱动程序通常分为两个主要类别：基于 MIPI 的驱动程序和 USB 视频类驱动程序。

对于自定义媒体源选项，驱动程序模型可能是完全自定义的 (专有) 或基于非传统相机源 (如文件或网络源) 。

### <a name="av-stream-driver"></a>AV 流驱动程序

AV 流驱动程序方法的主要优点是： PnP 和电源管理/设备管理已由 AV 流框架处理。

但是，这也意味着基础源必须是具有内核模式驱动程序的物理设备，才能与硬件交互。 对于 UVC 设备，Windows UVC 1.5 类驱动程序已提供收件箱，因此设备只需实现其固件。

对于基于 MIPI 的设备，供应商需要实现其自己的 AV 流微型端口驱动程序。

### <a name="custom-media-source"></a>自定义媒体源

对于其设备驱动程序已 (但不是 AV 流微型端口驱动程序) 或使用非传统相机捕获的源的源，AV 流驱动程序可能不可行。 例如，通过网络连接的 IP 照相机无法适应 AV 流驱动程序模型。

在这种情况下，使用框架服务器模型的自定义媒体源将是一种替代方法。

| 功能 | 自定义媒体源 | AV 流驱动程序 |
|--|--|--|
| PnP 和电源管理 | 必须由源和/或存根驱动程序实现 | 由 AV 流框架提供 |
| 用户模式插件 | 不可用。 自定义媒体源包含 OEM/IHV 特定的用户模式逻辑。 | DMFT、Platform DMFT 和 MFT0 for legacy 实现 |
| 传感器组 | 支持 | 支持 |
| 照相机配置文件 V2 | 支持 | 支持 |
| 照相机配置文件 V1 | 不支持 | 支持 |

## <a name="custom-media-source-requirements"></a>自定义媒体源要求

随着 Windows 相机框架服务器的引入 (称为框架服务器) 服务，可通过自定义媒体源实现此目的。 这需要两个主要组件：

- 带有用作存根驱动程序的驱动程序包，旨在注册/启用照相机设备接口。

- 承载自定义媒体源的 COM DLL。

第一种要求需要有两个用途：

- 一个审核的过程，可确保自定义媒体源通过受信任的进程安装 (驱动程序包需要 WHQL 认证) 。

- 支持 "照相机" 标准 PnP 枚举和发现。

### <a name="security"></a>安全性

框架服务器的自定义媒体源在安全性方面不同于一般自定义媒体源，如下所示：

- 框架服务器自定义媒体源作为本地服务运行 (不会与本地系统混淆;在) 的 Windows 计算机上，本地服务是非常低的特权帐户。

- 框架服务器自定义媒体源在会话0中运行 (系统服务会话) 并且无法与用户桌面交互。

鉴于这些约束，框架服务器自定义媒体源不得尝试访问文件系统和注册表的受保护部分。 通常情况下，允许读取访问权限，但不允许写入访问权限。

### <a name="performance"></a>性能

作为框架服务器模型的一部分，框架服务器将如何对自定义媒体源进行实例化的情况有两种：

- 在生成/发布传感器的过程中。

- 在 "照相机" 激活期间

传感器组生成通常在设备安装和/或电源周期内完成。 考虑到这一点，我们强烈建议在创建自定义媒体源的过程中避免任何重要处理，并将任何此类活动推迟到 [IMFMediaSource：： Start](https://docs.microsoft.com/windows/win32/api/mfidl/nf-mfidl-imfmediasource-start) 函数。 传感器组生成将不会尝试启动自定义媒体源，只需查询各种可用的流/媒体类型和源/流属性信息。

## <a name="stub-driver"></a>存根驱动程序

驱动程序包和存根驱动程序至少有两个要求。

存根（stub）驱动程序可以使用 WDF (UMDF 或 KMDF) 或 WDM 驱动程序模型编写。

驱动程序要求如下：

- 将 "照相机" (" [KSCATEGORY_VIDEO_CAMERA](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-video-camera) " 类别下的自定义媒体源) 设备接口，以便可以对其进行枚举。

> [!NOTE]
> 若要允许传统的 DirectShow 应用程序进行枚举，驱动程序还需要在 [KSCATEGORY_VIDEO](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-video) 和 [KSCATEGORY_CAPTURE](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-capture)下进行注册。

- 在 "设备接口" 节点下添加一个注册表项， (在 "驱动程序 INF **DDInstall** " 部分中使用**AddReg**指令，) 声明自定义媒体源 COM 对象的共同 iopalisserverextension CLSID。 必须使用以下注册表值名称添加此项： **CustomCaptureSourceClsid**。

这允许应用程序发现 "照相机" 源，并通知框架服务器服务截获激活调用，并将其重新路由到 CoCreated 自定义媒体源。

### <a name="sample-inf"></a>示例 INF

下面的示例演示了自定义媒体源存根驱动程序的典型 INF：

```inf
;/*++
;
;Module Name:
; SimpleMediaSourceDriver.INF
;
;Abstract:
; INF file for installing the Usermode SimpleMediaSourceDriver Driver
;
;Installation Notes:
; Using Devcon: Type "devcon install SimpleMediaSourceDriver.inf root\SimpleMediaSource" to install
;
;--*/

[Version]
Signature="$WINDOWS NT$"
Class=Sample
ClassGuid={5EF7C2A5-FF8F-4C1F-81A7-43D3CBADDC98}
Provider=%ProviderString%
DriverVer=01/28/2016,0.10.1234
CatalogFile=SimpleMediaSourceDriver.cat

[DestinationDirs]
DefaultDestDir = 12

; ================= Class section =====================

[ClassInstall32]
Addreg=SimpleMediaSourceClassReg

[SimpleMediaSourceClassReg]

HKR,,,0,%ClassName%
HKR,,Icon,,-24

[SourceDisksNames]
1 = %DiskId1%,,,""

[SourceDisksFiles]
SimpleMediaSourceDriver.dll = 1,,
SimpleMediaSource.dll = 1,,

;*****************************************
; SimpleMFSource Install Section
;*****************************************

[Manufacturer]
%StdMfg%=Standard,NT$ARCH$

[Standard.NT$ARCH$]
%SimpleMediaSource.DeviceDesc%=SimpleMediaSource, root\SimpleMediaSource

;---------------- copy files

[SimpleMediaSource.NT]
CopyFiles=UMDriverCopy, CustomCaptureSourceCopy
AddReg = CustomCaptureSource.ComRegistration

[SimpleMediaSource.NT.Interfaces]
AddInterface = %KSCATEGORY_VIDEO_CAMERA%, %CustomCaptureSource.ReferenceString%, CustomCaptureSourceInterface
AddInterface = %KSCATEGORY_VIDEO%, %CustomCaptureSource.ReferenceString%, CustomCaptureSourceInterface
AddInterface = %KSCATEGORY_CAPTURE%, %CustomCaptureSource.ReferenceString%, CustomCaptureSourceInterface

[CustomCaptureSourceInterface]
AddReg = CustomCaptureSourceInterface.AddReg, CustomCaptureSource.ComRegistration

[CustomCaptureSourceInterface.AddReg]
HKR,,CLSID,,%ProxyVCap.CLSID%
HKR,,CustomCaptureSourceClsid,,%CustomCaptureSource.CLSID%
HKR,,FriendlyName,,%CustomCaptureSource.Desc%

[CustomCaptureSource.ComRegistration]
HKCR,CLSID\%CustomCaptureSource.CLSID%,,,%CustomCaptureSource.Desc%
HKCR,CLSID\%CustomCaptureSource.CLSID%\InprocServer32,,%REG_EXPAND_SZ%,%CustomCaptureSource.Location%
HKCR,CLSID\%CustomCaptureSource.CLSID%\InprocServer32,ThreadingModel,,Both

[UMDriverCopy]
SimpleMediaSourceDriver.dll,,,0x00004000 ; COPYFLG_IN_USE_RENAME

[CustomCaptureSourceCopy]
SimpleMediaSource.dll,,,0x00004000 ; COPYFLG_IN_USE_RENAME

[DestinationDirs]
UMDriverCopy=12,UMDF ; copy to driversMdf
CustomCaptureSourceCopy=11

;-------------- Service installation
[SimpleMediaSource.NT.Services]
AddService=WUDFRd,0x000001fa,WUDFRD_ServiceInstall

[WUDFRD_ServiceInstall]
DisplayName = %WudfRdDisplayName%
ServiceType = 1
StartType = 3
ErrorControl = 1
ServiceBinary = %12%\WUDFRd.sys

;-------------- WDF specific section -------------
[SimpleMediaSource.NT.Wdf]
UmdfService=SimpleMediaSource, SimpleMediaSource_Install
UmdfServiceOrder=SimpleMediaSource

[SimpleMediaSource_Install]
UmdfLibraryVersion=$UMDFVERSION$
ServiceBinary=%12%\UMDF\SimpleMediaSourceDriver.dll

[Strings]
ProviderString = "Microsoft Corporation"
StdMfg = "(Standard system devices)"
DiskId1 = "SimpleMediaSource Disk \#1"
SimpleMediaSource.DeviceDesc = "SimpleMediaSource Capture Source" ; what you will see under SimpleMediaSource dummy devices
ClassName = "SimpleMediaSource dummy devices" ; device type this driver will install as in device manager
WudfRdDisplayName="Windows Driver Foundation - User-mode Driver Framework Reflector"
KSCATEGORY_VIDEO_CAMERA = "{E5323777-F976-4f5b-9B55-B94699C46E44}"
KSCATEGORY_CAPTURE="{65E8773D-8F56-11D0-A3B9-00A0C9223196}"
KSCATEGORY_VIDEO="{6994AD05-93EF-11D0-A3CC-00A0C9223196}"
ProxyVCap.CLSID="{17CCA71B-ECD7-11D0-B908-00A0C9223196}"
CustomCaptureSource.Desc = "SimpleMediaSource Source"
CustomCaptureSource.ReferenceString = "CustomCameraSource"
CustomCaptureSource.CLSID = "{9812588D-5CE9-4E4C-ABC1-049138D10DCE}"
CustomCaptureSource.Location = "%SystemRoot%\System32\SimpleMediaSource.dll"
CustomCaptureSource.Binary = "SimpleMediaSource.dll"
REG_EXPAND_SZ = 0x00020000
```

上述自定义媒体源在 **KSCATEGORY \_ video**、 **KSCATEGORY \_ CAPTURE**和 **KSCATEGORY \_ 视频 \_ 相机** 下注册，以确保任何 UWP 和非 UWP 应用都可以发现 "相机" 以搜索标准 RGB 相机。

如果自定义媒体源还公开非 RGB 流 (IR、深度等) 则还可以选择在 [KSCATEGORY_SENSOR_CAMERA](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-sensor-camera)下进行注册。

> [!NOTE]
> 大多数基于 USB 的网络摄像头将公开 YUY2 和 MJPG 格式。 由于此行为，许多旧的 DirectShow 应用程序都是通过假设 YUY2/MJPG 可用而编写的。 若要确保与此类应用程序的兼容性，建议在自定义媒体源中提供 YUY2 介质类型（如果需要旧版应用兼容性）。

### <a name="stub-driver-implementation"></a>存根驱动程序实现

除 INF 外，驱动程序存根还必须注册并启用照相机设备接口。 这通常是在 **驱动程序 \_ 添加 \_ 设备** 操作过程中完成的。

请参阅针对基于 WDM 的驱动程序的 [DRIVER_ADD_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 回调函数和用于 UMDF/KMDF 驱动程序的 [WdfDriverCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate) 函数。

下面是用于处理此操作的 UMDF 驱动程序存根的代码段：

```cpp
NTSTATUS
DriverEntry(
    IN PDRIVER_OBJECT DriverObject,
    IN PUNICODE_STRING RegistryPath
    )
/*++

Routine Description:

    DriverEntry initializes the driver and is the first routine called by the
    system after the driver is loaded. DriverEntry specifies the other entry
    points in the function driver, such as EvtDevice and DriverUnload.

Parameters Description:

    DriverObject - represents the instance of the function driver that is loaded
    into memory. DriverEntry must initialize members of DriverObject before it
    returns to the caller. DriverObject is allocated by the system before the
    driver is loaded, and it is released by the system after the system unloads
    the function driver from memory.

RegistryPath - represents the driver specific path in the Registry.

    The function driver can use the path to store driver related data between
    reboots. The path does not store hardware instance specific data.

Return Value:

    STATUS_SUCCESS if successful,  
    STATUS_UNSUCCESSFUL otherwise.

--*/

{
    WDF_DRIVER_CONFIG config;
    NTSTATUS status;

    WDF_DRIVER_CONFIG_INIT(&config,
                    EchoEvtDeviceAdd
                    );

    status = WdfDriverCreate(DriverObject,
                            RegistryPath,
                            WDF_NO_OBJECT_ATTRIBUTES,
                            &config,
                            WDF_NO_HANDLE);

    if (!NT_SUCCESS(status)) {
        KdPrint(("Error: WdfDriverCreate failed 0x%x\n", status));
        return status;
    }

    // ...

    return status;
}

NTSTATUS
EchoEvtDeviceAdd(
    IN WDFDRIVER Driver,
    IN PWDFDEVICE_INIT DeviceInit
    )
/*++
Routine Description:

    EvtDeviceAdd is called by the framework in response to AddDevice
    call from the PnP manager. We create and initialize a device object to
    represent a new instance of the device.

Arguments:

    Driver - Handle to a framework driver object created in DriverEntry

    DeviceInit - Pointer to a framework-allocated WDFDEVICE_INIT structure.

Return Value:

    NTSTATUS

--*/
{
    NTSTATUS status;

    UNREFERENCED_PARAMETER(Driver);

    KdPrint(("Enter EchoEvtDeviceAdd\n"));

    status = EchoDeviceCreate(DeviceInit);

    return status;
}

NTSTATUS
EchoDeviceCreate(
    PWDFDEVICE_INIT DeviceInit  
/*++

Routine Description:

    Worker routine called to create a device and its software resources.

Arguments:

    DeviceInit - Pointer to an opaque init structure. Memory for this
                    structure will be freed by the framework when the WdfDeviceCreate
                    succeeds. Do not access the structure after that point.

Return Value:

    NTSTATUS

--*/  
{
    WDF_OBJECT_ATTRIBUTES deviceAttributes;
    PDEVICE_CONTEXT deviceContext;
    WDF_PNPPOWER_EVENT_CALLBACKS pnpPowerCallbacks;
    WDFDEVICE device;
    NTSTATUS status;
    UNICODE_STRING szReference;
    RtlInitUnicodeString(&szReference, L"CustomCameraSource");

    WDF_PNPPOWER_EVENT_CALLBACKS_INIT(&pnpPowerCallbacks);

    //
    // Register pnp/power callbacks so that we can start and stop the timer as the device
    // gets started and stopped.
    //
    pnpPowerCallbacks.EvtDeviceSelfManagedIoInit = EchoEvtDeviceSelfManagedIoStart;
    pnpPowerCallbacks.EvtDeviceSelfManagedIoSuspend = EchoEvtDeviceSelfManagedIoSuspend;

    #pragma prefast(suppress: 28024, "Function used for both Init and Restart Callbacks")
    pnpPowerCallbacks.EvtDeviceSelfManagedIoRestart = EchoEvtDeviceSelfManagedIoStart;

    //
    // Register the PnP and power callbacks. Power policy related callbacks will be registered
    // later in SoftwareInit.
    //
    WdfDeviceInitSetPnpPowerEventCallbacks(DeviceInit, &pnpPowerCallbacks);

    {
        WDF_FILEOBJECT_CONFIG cameraFileObjectConfig;
        WDF_OBJECT_ATTRIBUTES cameraFileObjectAttributes;

        WDF_OBJECT_ATTRIBUTES_INIT(&cameraFileObjectAttributes);

        cameraFileObjectAttributes.SynchronizationScope = WdfSynchronizationScopeNone;

        WDF_FILEOBJECT_CONFIG_INIT(
            &cameraFileObjectConfig,
            EvtCameraDeviceFileCreate,
            EvtCameraDeviceFileClose,
            WDF_NO_EVENT_CALLBACK);

        WdfDeviceInitSetFileObjectConfig(
            DeviceInit,
            &cameraFileObjectConfig,
            &cameraFileObjectAttributes);
    }

    WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&deviceAttributes, DEVICE_CONTEXT);

    status = WdfDeviceCreate(&DeviceInit, &deviceAttributes, &device);

    if (NT_SUCCESS(status)) {
        //
        // Get the device context and initialize it. WdfObjectGet_DEVICE_CONTEXT is an
        // inline function generated by WDF_DECLARE_CONTEXT_TYPE macro in the
        // device.h header file. This function will do the type checking and return
        // the device context. If you pass a wrong object handle
        // it will return NULL and assert if run under framework verifier mode.
        //
        deviceContext = WdfObjectGet_DEVICE_CONTEXT(device);
        deviceContext->PrivateDeviceData = 0;

        //
        // Create a device interface so that application can find and talk
        // to us.
        //
        status = WdfDeviceCreateDeviceInterface(
            device,
            &CAMERA_CATEGORY,
            &szReference // ReferenceString
            );

        if (NT_SUCCESS(status)) {
            //
            // Create a device interface so that application can find and talk
            // to us.
            //
            status = WdfDeviceCreateDeviceInterface(
            device,
            &CAPTURE_CATEGORY,
            &szReference // ReferenceString
            );
        }

        if (NT_SUCCESS(status)) {
            //
            // Create a device interface so that application can find and talk
            // to us.
            //
            status = WdfDeviceCreateDeviceInterface(
            device,
            &VIDEO_CATEGORY,
            &szReference // ReferenceString
            );
        }

        if (NT_SUCCESS(status)) {
            //
            // Initialize the I/O Package and any Queues
            //
            status = EchoQueueInitialize(device);
        }
    }

    return status;
}
```

### <a name="pnp-operation"></a>PnP 操作

就像任何其他物理相机一样，建议存根驱动程序至少管理在删除/连接基础源时启用和禁用设备的 PnP 操作。 例如，如果自定义媒体源使用网络源 (例如 IP 摄像机) ，则可能需要在该网络源不再可用时触发设备删除。

这可确保应用程序通过 PnP Api 侦听设备的添加/删除操作获取正确的通知。 并确保无法枚举不再可用的源。

有关 UMDF 和 KMDF 驱动程序，请参阅 [WdfDeviceSetDeviceState](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetdevicestate) 函数文档。

对于 WMD 驱动程序，请参阅 [IoSetDeviceInterfaceState](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate) 函数文档。

## <a name="custom-media-source-dll"></a>自定义媒体源 DLL

自定义媒体源是标准 inproc COM 服务器，必须实现以下接口：

- [IMFMediaEventGenerator](https://docs.microsoft.com/windows/win32/api/mfobjects/nn-mfobjects-imfmediaeventgenerator)

- [IMFMediaSource](https://docs.microsoft.com/windows/win32/api/mfidl/nn-mfidl-imfmediasource)

- [IMFMediaSourceEx](https://docs.microsoft.com/windows/win32/api/mfidl/nn-mfidl-imfmediasourceex)

- [IKsControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nn-ks-ikscontrol)

- [IMFGetService](https://docs.microsoft.com/windows/win32/api/mfidl/nn-mfidl-imfgetservice)

> [!NOTE]
> **IMFMediaSourceEx** 继承自 **IMFMediaSource** ， **IMFMediaSource** 继承自 **IMFMediaEventGenerator**。

自定义媒体源中每个受支持的流都必须支持以下接口：

- **IMFMediaEventGenerator**

- [IMFMediaStream](https://docs.microsoft.com/windows/win32/api/mfidl/nn-mfidl-imfmediastream)

- **IMFMediaStream2**

> [!NOTE]
> **IMFMediaStream2** 继承自 **IMFMediaStream** ， **IMFMediaStream** 继承自 **IMFMediaEventGenerator**。

请参阅 [编写自定义媒体源](https://docs.microsoft.com/windows/desktop/medfound/writing-a-custom-media-source) 文档，了解如何创建自定义媒体源。 本部分的其余部分将介绍在框架服务器框架内支持自定义媒体源所需的差异。

### <a name="imfgetservice"></a>IMFGetService

**IMFGetService** 是框架服务器自定义媒体源的必需接口。 如果你的自定义媒体源不需要公开任何其他服务接口， **IMFGetService**可能会返回**MF \_ E \_ 不受支持的 \_ 服务**。

下面的示例显示了不带支持服务接口的 **IMFGetService** 实现：

```cpp
_Use_decl_annotations_
IFACEMETHODIMP
SimpleMediaSource::GetService(
    _In_ REFGUID guidService,
    _In_ REFIID riid,
    _Out_ LPVOID * ppvObject
    )
{
    HRESULT hr = S_OK;
    auto lock = _critSec.Lock();

    RETURN_IF_FAILED (_CheckShutdownRequiresLock());

    if (!ppvObject)
    {
        return E_POINTER;
    }
    *ppvObject = NULL;

    // We have no supported service, just return
    // MF_E_UNSUPPORTED_SERVICE for all calls.

    return MF_E_UNSUPPORTED_SERVICE;
}
```

### <a name="imfmediaeventgenerator"></a>IMFMediaEventGenerator

如上所示，源和源中的各个流都必须支持其自己的 [IMFMediaEventGenerator](https://docs.microsoft.com/windows/win32/api/mfobjects/nn-mfobjects-imfmediaeventgenerator) 接口。 来自源的整个 MF 管道数据和控制流通过事件生成器通过事件生成器进行管理，该事件生成器将发送特定的 [IMFMediaEvent](https://docs.microsoft.com/windows/win32/api/mfobjects/nn-mfobjects-imfmediaevent)。

对于实现 IMFMediaEventGenerator，自定义媒体源必须使用 [MFCreateEventQueue](https://docs.microsoft.com/windows/win32/api/mfapi/nf-mfapi-mfcreateeventqueue) API 来创建 [IMFMediaEventQueue](https://docs.microsoft.com/windows/win32/api/mfobjects/nn-mfobjects-imfmediaeventqueue) ，并将 **IMFMediaEventGenerator** 的所有方法路由到 queue 对象：

**IMFMediaEventGenerator** 具有以下方法：

```cpp
// IMFMediaEventGenerator
IFACEMETHOD(BeginGetEvent)(_In_ IMFAsyncCallback *pCallback, _In_ IUnknown *punkState);
IFACEMETHOD(EndGetEvent)(_In_ IMFAsyncResult *pResult, _COM_Outptr_ IMFMediaEvent **ppEvent);
IFACEMETHOD(GetEvent)(DWORD dwFlags, _Out_ IMFMediaEvent **ppEvent);
IFACEMETHOD(QueueEvent)(MediaEventType met, REFGUID guidExtendedType, HRESULT hrStatus, _In_opt_ const PROPVARIANT *pvValue);
```

下面的代码演示 **IMFMediaEventGenerator** 接口的建议实现。 自定义媒体源实现将公开 **IMFMediaEventGenerator** 接口，该接口的方法将请求路由到在媒体源创建/初始化过程中创建的 **IMFMediaEventQueue** 对象。

在下面的代码中， ** \_ spEventQueue**对象是使用**MFCreateEventQueue**函数创建的**IMFMediaEventQueue** ：

```cpp
// IMFMediaEventGenerator methods
IFACEMETHODIMP
SimpleMediaSource::BeginGetEvent(
    _In_ IMFAsyncCallback *pCallback,
    _In_ IUnknown *punkState
    )
{
    HRESULT hr = S_OK;
    auto lock = _critSec.Lock();

    RETURN_IF_FAILED (_CheckShutdownRequiresLock());
    RETURN_IF_FAILED (_spEventQueue->BeginGetEvent(pCallback, punkState));

    return hr;
}

IFACEMETHODIMP
SimpleMediaSource::EndGetEvent(
    _In_ IMFAsyncResult *pResult,
    _COM_Outptr_ IMFMediaEvent **ppEvent
    )
{
    HRESULT hr = S_OK;
    auto lock = _critSec.Lock();

    RETURN_IF_FAILED (_CheckShutdownRequiresLock());
    RETURN_IF_FAILED (_spEventQueue->EndGetEvent(pResult, ppEvent));

    return hr;
}

IFACEMETHODIMP
SimpleMediaSource::GetEvent(
    DWORD dwFlags,
    _COM_Outptr_ IMFMediaEvent **ppEvent
    )
{
    // NOTE:
    // GetEvent can block indefinitely, so we do not hold the lock.
    // This requires some juggling with the event queue pointer.

    HRESULT hr = S_OK;

    ComPtr<IMFMediaEventQueue> spQueue;

    {
        auto lock = _critSec.Lock();

        RETURN_IF_FAILED (_CheckShutdownRequiresLock());
        spQueue = _spEventQueue;
    }

    // Now get the event.
    RETURN_IF_FAILED (_spEventQueue->GetEvent(dwFlags, ppEvent));

    return hr;
}

IFACEMETHODIMP
SimpleMediaSource::QueueEvent(
    MediaEventType eventType,
    REFGUID guidExtendedType,
    HRESULT hrStatus,
    _In_opt_ PROPVARIANT const *pvValue
    )
{
    HRESULT hr = S_OK;
    auto lock = _critSec.Lock();

    RETURN_IF_FAILED (_CheckShutdownRequiresLock());
    RETURN_IF_FAILED (_spEventQueue->QueueEventParamVar(eventType, guidExtendedType, hrStatus, pvValue));

    return hr;
}
```

### <a name="seeking-and-pausing"></a>查找和暂停

通过框架服务器框架支持的自定义媒体源不支持查找或暂停操作。 自定义媒体源不需要为这些操作提供支持，且不得发布 **MFSourceSeeked** 或 **MEStreamSeeked** 事件。

[IMFMediaSource：:P ause](https://docs.microsoft.com/windows/win32/api/mfidl/nf-mfidl-imfmediasource-pause) 应返回 **mf \_ e \_ 无效 \_ 状态 \_ 转换** (或 **mf \_ e \_ 关机** （如果源已关闭) ）。

### <a name="ikscontrol"></a>IKsControl

[IKsControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nn-ks-ikscontrol) 是所有相机相关控件的标准控制接口。 如果自定义媒体源实现了任何相机控制，则 **IKsControl** 接口就是管道路由控制 i/o 的方式。

有关详细信息，请参阅下面的控件集文档主题：

- [PROPSETID_VIDCAP_CAMERACONTROL](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-cameracontrol)

- [PROPSETID_VIDCAP_VIDEOPROCAMP](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videoprocamp)

- [KSPROPERTYSETID_ExtendedCameraControl](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropertysetid-extendedcameracontrol)

这些控件是可选的，如果不支持，建议返回的错误代码为 **" \_ HRESULT \_ (\_ \_ 找不到 \_) 设置 **"。

下面的代码是一个不受支持的控件的示例 **IKsControl** 实现：

```cpp
// IKsControl methods
_Use_decl_annotations_
IFACEMETHODIMP
SimpleMediaSource::KsProperty(
    _In_reads_bytes_(ulPropertyLength) PKSPROPERTY pProperty,
    _In_ ULONG ulPropertyLength,
    _Inout_updates_to_(ulDataLength, *pBytesReturned) LPVOID pPropertyData,
    _In_ ULONG ulDataLength,
    _Out_ ULONG* pBytesReturned
    )
{
    // ERROR_SET_NOT_FOUND is the standard error code returned
    // by the AV Stream driver framework when a miniport
    // driver does not register a handler for a KS operation.
    // We want to mimic the driver behavior here if we do not
    // support controls.
    return HRESULT_FROM_WIN32(ERROR_SET_NOT_FOUND);
}

_Use_decl_annotations_
IFACEMETHODIMP SimpleMediaSource::KsMethod(
    _In_reads_bytes_(ulMethodLength) PKSMETHOD pMethod,
    _In_ ULONG ulMethodLength,
    _Inout_updates_to_(ulDataLength, *pBytesReturned) LPVOID pMethodData,
    _In_ ULONG ulDataLength,
    _Out_ ULONG* pBytesReturned
    )
{
    return HRESULT_FROM_WIN32(ERROR_SET_NOT_FOUND);
}

_Use_decl_annotations_
IFACEMETHODIMP SimpleMediaSource::KsEvent(
    _In_reads_bytes_opt_(ulEventLength) PKSEVENT pEvent,
    _In_ ULONG ulEventLength,
    _Inout_updates_to_(ulDataLength, *pBytesReturned) LPVOID pEventData,
    _In_ ULONG ulDataLength,
    _Out_opt_ ULONG* pBytesReturned
    )
{
    return HRESULT_FROM_WIN32(ERROR_SET_NOT_FOUND);
}
```

### <a name="imfmediastream2"></a>IMFMediaStream2

如[编写自定义媒体源](https://docs.microsoft.com/windows/desktop/medfound/writing-a-custom-media-source)中所述，通过在[IMFMediaSource：： Start](https://docs.microsoft.com/windows/win32/api/mfidl/nf-mfidl-imfmediasource-start)方法完成过程中发布到源事件队列的[MENewStream](https://docs.microsoft.com/windows/desktop/medfound/menewstream)媒体事件，可在自定义媒体源中为帧工作提供**IMFMediaStream2**接口：

```cpp
IFACEMETHODIMP
SimpleMediaSource::Start(
    _In_ IMFPresentationDescriptor *pPresentationDescriptor,
    _In_opt_ const GUID *pguidTimeFormat,
    _In_ const PROPVARIANT *pvarStartPos
    )
{
    HRESULT hr = S_OK;
    auto lock = _critSec.Lock();
    DWORD count = 0;
    PROPVARIANT startTime;
    BOOL selected = false;
    ComPtr<IMFStreamDescriptor> streamDesc;
    DWORD streamIndex = 0;

    if (pPresentationDescriptor == nullptr || pvarStartPos == nullptr)
    {
        return E_INVALIDARG;
    }
    else if (pguidTimeFormat != nullptr && *pguidTimeFormat != GUID_NULL)
    {
        return MF_E_UNSUPPORTED_TIME_FORMAT;
    }

    RETURN_IF_FAILED (_CheckShutdownRequiresLock());

    if (_sourceState != SourceState::Stopped)
    {
        return MF_E_INVALID_STATE_TRANSITION;
    }

    _sourceState = SourceState::Started;

    // This checks the passed in PresentationDescriptor matches the member of streams we
    // have defined internally and that at least one stream is selected

    RETURN_IF_FAILED (_ValidatePresentationDescriptor(pPresentationDescriptor));
    RETURN_IF_FAILED (pPresentationDescriptor->GetStreamDescriptorCount(&count));
    RETURN_IF_FAILED (InitPropVariantFromInt64(MFGetSystemTime(), &startTime));

    // Send event that the source started. Include error code in case it failed.
    RETURN_IF_FAILED (_spEventQueue->QueueEventParamVar(MESourceStarted,
                                                            GUID_NULL,
                                                            hr,
                                                            &startTime));

    // We are hardcoding this to the first descriptor
    // since this sample is a single stream sample. For
    // multiple streams, we need to walk the list of streams
    // and for each selected stream, send the MEUpdatedStream
    // or MENewStream event along with the MEStreamStarted
    // event.
    RETURN_IF_FAILED (pPresentationDescriptor->GetStreamDescriptorByIndex(0,
                                                                            &selected,
                                                                            &streamDesc));

    RETURN_IF_FAILED (streamDesc->GetStreamIdentifier(&streamIndex));
    if (streamIndex >= NUM_STREAMS)
    {
        return MF_E_INVALIDSTREAMNUMBER;
    }

    if (selected)
    {
        ComPtr<IUnknown> spunkStream;
        MediaEventType met = (_wasStreamPreviouslySelected ? MEUpdatedStream : MENewStream);

        // Update our internal PresentationDescriptor
        RETURN_IF_FAILED (_spPresentationDescriptor->SelectStream(streamIndex));
        RETURN_IF_FAILED (_stream.Get()->SetStreamState(MF_STREAM_STATE_RUNNING));
        RETURN_IF_FAILED (_stream.As(&spunkStream));

        // Send the MEUpdatedStream/MENewStream to our source event
        // queue.

        RETURN_IF_FAILED (_spEventQueue->QueueEventParamUnk(met,
                                                                GUID_NULL,
                                                                S_OK,
                                                                spunkStream.Get()));

        // But for our stream started (MEStreamStarted), we post to our
        // stream event queue.
        RETURN_IF_FAILED (_stream.Get()->QueueEvent(MEStreamStarted,
                                                        GUID_NULL,
                                                        S_OK,
                                                        &startTime));
    }
    _wasStreamPreviouslySelected = selected;

    return hr;
}
```

必须为通过 [IMFPresentationDescriptor](https://docs.microsoft.com/windows/win32/api/mfidl/nn-mfidl-imfpresentationdescriptor)选择的每个流执行此操作。

对于包含视频流的自定义媒体源，不应发送 [MEEndOfStream](https://docs.microsoft.com/windows/desktop/medfound/meendofstream) 和 [MEEndOfPresentation](https://docs.microsoft.com/windows/desktop/medfound/meendofpresentation) 事件。

### <a name="stream-attributes"></a>流属性

所有自定义媒体源流都必须将 [MF_DEVICESTREAM_STREAM_CATEGORY](https://docs.microsoft.com/windows/desktop/medfound/mf-devicestream-stream-category) 设置为 **PINNAME \_ 视频 \_ 捕获**。 **PINNAME \_自 \_ ** 定义媒体源不支持视频预览。

> [!NOTE]
> **PINNAME \_** 虽然支持，但不建议使用映像。 使用 **PINNAME \_ 映像** 公开流需要自定义媒体源来支持所有照片触发器控件。 有关更多详细信息，请参阅下面的 [照片流控制](#photo-stream-controls) 部分。

[MF_DEVICESTREAM_STREAM_ID](https://docs.microsoft.com/windows/desktop/medfound/mf-devicestream-stream-id) 是所有流的必需属性。 它应该是从0开始的索引。 因此，第一个流的 ID 为0，第二个流的 id 为1，依此类推。

下面是流上建议的属性列表：

- [MF_DEVICESTREAM_ATTRIBUTE_FRAMESOURCE_TYPES](https://docs.microsoft.com/windows/desktop/medfound/mf-devicestream-attribute-framesource-types)

- [MF_DEVICESTREAM_FRAMESERVER_SHARED](https://docs.microsoft.com/windows/desktop/medfound/mf-devicestream-frameserver-shared)

#### <a name="mf_devicestream_attribute_framesource_types"></a>MF \_ DEVICESTREAM \_ 属性 \_ FRAMESOURCE \_ 类型

**MF \_DEVICESTREAM \_ 属性 \_ FRAMESOURCE \_ 类型** 是一个 UINT32 属性，它是流类型的 bitmasked 值。 它可以设置为以下任一 (，而这些类型是一个位掩码标志，则建议在所有可能的) 时不会混合源类型：

| 类型                         | Flag   | 描述                                      |
|------------------------------|--------|--------------------------------------------------|
| MFFrameSourceTypes \_ 颜色    | 0x0001 | 标准 RGB 颜色流                        |
| MFFrameSourceTypes \_ 红外 | 0x0002 | IR 流                                        |
| MFFrameSourceTypes \_ 深度    | 0x0004 | 深度流                                     |
| MFFrameSourceTypes \_ 图    | 0x0008 | 图像流 (非视频子类型，通常为 JPEG)  |
| \_自定义 MFFrameSourceTypes   | 0x0080 | 自定义流类型                               |

#### <a name="mf_devicestream_frameserver_shared"></a>MF \_ DEVICESTREAM \_ FRAMESERVER \_ SHARED

**MF \_DEVICESTREAM \_ FRAMESERVER \_ SHARED** 是一个 UINT32 属性，可将其设置为0或1。 如果设置为1，则它会将流标记为帧服务器 "可共享"。 这将允许应用程序在共享模式下打开流，即使其他应用程序使用它时也是如此。

如果未设置此属性，则框架服务器将允许共享第一个未标记的流 (如果自定义媒体源只有一个流，则会将该流标记为共享) 。

如果将此属性设置为0，则框架服务器将阻止来自共享应用的流。 如果自定义媒体源标记将此特性设置为0的所有流，则任何共享的应用程序都将无法初始化源。

### <a name="sample-allocation"></a>示例分配

所有媒体帧必须以 [IMFSample](https://docs.microsoft.com/windows/win32/api/mfobjects/nn-mfobjects-imfsample)的形式生成。 自定义媒体源必须使用 [MFCreateSample](https://docs.microsoft.com/windows/win32/api/mfapi/nf-mfapi-mfcreatesample) 函数来分配 IMFSample 的实例，并使用 [AddBuffer](https://docs.microsoft.com/windows/win32/api/mfobjects/nf-mfobjects-imfsample-addbuffer) 方法添加媒体缓冲区。

每个 **IMFSample** 都必须设置示例时间和采样持续时间。 所有示例时间戳都必须基于 QPC time (QueryPerformanceCounter) 。

建议在可能的情况下，自定义媒体源使用 [MFGetSystemTime](https://docs.microsoft.com/windows/win32/api/mfidl/nf-mfidl-mfgetsystemtime) 函数。 此函数是围绕 **QueryPerformanceCounter** 的包装器，将 QPC 刻度转换为100毫微秒。

自定义媒体源可以使用内部时钟，但必须根据当前 QPC 将所有时间戳关联到100毫微秒单位。

#### <a name="media-buffer"></a>媒体缓冲区

添加到 **IMFSample** 中的所有媒体缓冲区必须使用标准 MF 缓冲区分配函数。 自定义媒体源不得实现其自己的 [IMFMediaBuffer](https://docs.microsoft.com/windows/win32/api/mfobjects/nn-mfobjects-imfmediabuffer) 接口或尝试直接分配媒体缓冲区 (例如，new/Malloc/VirtualAlloc 等）不能用于帧数据) 。

使用以下任何 Api 来分配媒体帧：

- [MFCreateMemoryBuffer](https://docs.microsoft.com/windows/win32/api/mfapi/nf-mfapi-mfcreatememorybuffer)

- [MFCreateAlignedMemoryBuffer](https://docs.microsoft.com/windows/win32/api/mfapi/nf-mfapi-mfcreatealignedmemorybuffer)

- [MFCreate2DMediaBuffer](https://docs.microsoft.com/windows/win32/api/mfapi/nf-mfapi-mfcreate2dmediabuffer)

- [MFCreateDXGISurfaceBuffer](https://docs.microsoft.com/windows/win32/api/mfapi/nf-mfapi-mfcreatedxgisurfacebuffer)

**MFCreateMemoryBuffer** 和 **MFCreateAlignedMemoryBuffer** 应用于非步幅对齐媒体数据。 通常，这些是自定义子类型或压缩子类型 (例如 H264/HEVC/MJPG) 。

对于已知的未压缩媒体类型 (例如 YUY2、NV12 等) 使用系统内存时，建议使用 **MFCreate2DMediaBuffer**。

若要使用 DX surface (执行 GPU 加速操作（如渲染和/或编码) ），应使用 **MFCreateDXGISurfaceBuffer** 。

**MFCreateDXGISurfaceBuffer** 不会创建 DX 图面。 通过 [IMFMediaSourceEx：： SetD3DManager](https://docs.microsoft.com/windows/win32/api/mfidl/nf-mfidl-imfmediasourceex-setd3dmanager) 方法使用传入媒体源的 DXGI 管理器创建图面。

[IMFDXGIDeviceManager：： OpenDeviceHandle](https://docs.microsoft.com/windows/win32/api/mfobjects/nf-mfobjects-imfdxgidevicemanager-opendevicehandle)将提供与所选 D3D 设备关联的句柄。 然后，可以使用[IMFDXGIDeviceManager：： GetVideoService](https://docs.microsoft.com/windows/win32/api/mfobjects/nf-mfobjects-imfdxgidevicemanager-getvideoservice)方法获取[ID3D11Device](https://docs.microsoft.com/windows/win32/api/d3d11/nn-d3d11-id3d11device)接口。

无论使用哪种类型的缓冲区，都必须通过媒体流**IMFMediaEventGenerator**上的**MEMediaSample**事件向管道提供创建的**IMFSample** 。

尽管可以对自定义媒体源和**IMFMediaStream**的基础集合使用相同的**IMFMediaEventQueue** ，但应该注意的是，这样做会导致媒体源事件和流事件的序列化， (包括媒体流) 。 对于包含多个流的源，这并不是理想的做法。

以下代码段显示了媒体流的示例实现：

```cpp
IFACEMETHODIMP
    SimpleMediaStream::RequestSample(
    _In_ IUnknown *pToken
    )
{
    HRESULT hr = S_OK;
    auto lock = _critSec.Lock();
    ComPtr<IMFSample> sample;
    ComPtr<IMFMediaBuffer> outputBuffer;
    LONG pitch = IMAGE_ROW_SIZE_BYTES;
    BYTE *bufferStart = nullptr; // not used
    DWORD bufferLength = 0;
    BYTE *pbuf = nullptr;
    ComPtr<IMF2DBuffer2> buffer2D;

    RETURN_IF_FAILED (_CheckShutdownRequiresLock());
    RETURN_IF_FAILED (MFCreateSample(&sample));
    RETURN_IF_FAILED (MFCreate2DMediaBuffer(NUM_IMAGE_COLS,
                                            NUM_IMAGE_ROWS,
                                            D3DFMT_X8R8G8B8,
                                            false,
                                            &outputBuffer));
    RETURN_IF_FAILED (outputBuffer.As(&buffer2D));
    RETURN_IF_FAILED (buffer2D->Lock2DSize(MF2DBuffer_LockFlags_Write,
                                                &pbuf,
                                                &pitch,
                                                &bufferStart,
                                                &bufferLength));
    RETURN_IF_FAILED (WriteSampleData(pbuf, pitch, bufferLength));
    RETURN_IF_FAILED (buffer2D->Unlock2D());
    RETURN_IF_FAILED (sample->AddBuffer(outputBuffer.Get()));
    RETURN_IF_FAILED (sample->SetSampleTime(MFGetSystemTime()));
    RETURN_IF_FAILED (sample->SetSampleDuration(333333));
    if (pToken != nullptr)
    {
        RETURN_IF_FAILED (sample->SetUnknown(MFSampleExtension_Token, pToken));
    }
    RETURN_IF_FAILED (_spEventQueue->QueueEventParamUnk(MEMediaSample,
                                                            GUID_NULL,
                                                            S_OK,
                                                            sample.Get()));

    return hr;
}
```

## <a name="custom-media-source-extension-to-expose-imfactivate-available-in-windows-10-version-1809"></a>自定义媒体源扩展，用于公开 Windows 10 1809 版中提供的 IMFActivate () 

除了自定义媒体源必须支持的接口列表外，自定义媒体源操作在框架服务器体系结构中所强加的限制之一是，只能通过管道将一个 UMDF 驱动程序实例 "激活"。

例如，如果你有一个物理设备，除了它的非 AV 流驱动程序包外，还会安装一个 UMDF 存根驱动程序，并将多个这些物理设备附加到计算机，而 UMDF 驱动程序的每个实例都将获得唯一的符号链接名称，则自定义媒体源的激活路径将无法在创建时传达与自定义媒体源关联的符号链接名称。

自定义媒体源可能会在自定义媒体源的属性存储 (通过[IMFMediaSourceEx：： GetSourceAttributes](https://docs.microsoft.com/windows/win32/api/mfidl/nf-mfidl-imfmediasourceex-getsourceattributes)) 方法从自定义媒体源返回的属性存储中查找标准[MF_DEVSOURCE_ATTRIBUTE_SOURCE_TYPE_VIDCAP_SYMBOLIC_LINK](https://docs.microsoft.com/windows/desktop/medfound/mf-devsource-attribute-source-type-vidcap-symbolic-link)属性，同时调用[IMFMediaSource：： Start](https://docs.microsoft.com/windows/win32/api/mfidl/nf-mfidl-imfmediasource-start) 。

但是，这可能会导致启动延迟较高，因为这会将 HW 资源采集延迟为开始时间，而不是创建/初始化时间。

因此，在 Windows 10 版本1809中，自定义媒体源可以选择公开 [IMFActivate](https://docs.microsoft.com/windows/win32/api/mfobjects/nn-mfobjects-imfactivate) 接口。

> [!NOTE]
> **IMFActivate** 继承自 [IMFAttributes](https://docs.microsoft.com/windows/win32/api/mfobjects/nn-mfobjects-imfattributes)。

### <a name="imfactivate"></a>IMFActivate

如果自定义媒体源的 COM 服务器支持**IMFActivate**接口，则设备初始化信息将通过**IMFActivate**继承的**IMFAttributes**提供给 COM 服务器。 因此，在调用 [IMFActivate：： ActivateObject](https://docs.microsoft.com/windows/win32/api/mfobjects/nf-mfobjects-imfactivate-activateobject) 时， **IMFActivate** 的属性存储将包含 UMDF 存根驱动程序的符号链接名称，以及创建/初始化源时管道/应用程序提供的任何其他配置设置。

自定义媒体源应使用此方法调用来获取所需的任何硬件资源。

> [!NOTE]
> 如果硬件资源获取所用的时间超过200毫秒，则建议使用异步获取硬件资源。 激活自定义媒体源不应在硬件资源获取上阻止。 相反，应将 [IMFMediaSource：： Start](https://docs.microsoft.com/windows/win32/api/mfidl/nf-mfidl-imfmediasource-start) 操作序列化为硬件资源采集。

**IMFActivate**、 [DetachObject](https://docs.microsoft.com/windows/win32/api/mfobjects/nf-mfobjects-imfactivate-detachobject)和[ShutdownObject](https://docs.microsoft.com/windows/win32/api/mfobjects/nf-mfobjects-imfactivate-shutdownobject)公开的两个附加方法必须返回**E \_ NOTIMPL**。

自定义媒体源可以选择在与[IMFMediaSource](https://docs.microsoft.com/windows/win32/api/mfidl/nn-mfidl-imfmediasource)相同的 COM 对象中实现**IMFActivate**和**IMFAttributes**接口。 如果已完成此操作，建议使用[IMFMediaSourceEx：： GetSourceAttributes](https://docs.microsoft.com/windows/win32/api/mfidl/nf-mfidl-imfmediasourceex-getsourceattributes)返回与**IMFActivate**中的相同**IMFAttributes**接口。

如果自定义媒体源未实现具有相同对象的 **IMFActivate** 和 **IMFAttributes** ，则自定义媒体源必须将 **IMFActivate** 属性存储上设置的所有属性复制到自定义媒体源的源属性存储中。

## <a name="encoded-camera-stream"></a>编码相机流

自定义媒体源可能会 (HEVC 或 H264 基本流公开压缩媒体类型) 并且 OS 管道完全支持自定义媒体源上编码参数的源和配置， (编码参数通过 [ICodecAPI](https://docs.microsoft.com/windows/win32/api/strmif/nn-strmif-icodecapi)传递，后者路由为 [IKsControl：： KsProperty](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-ikscontrol-ksproperty) 调用) ：

```cpp
// IKsControl methods
_Use_decl_annotations_
IFACEMETHODIMP
SimpleMediaSource::KsProperty(
    _In_reads_bytes_(ulPropertyLength) PKSPROPERTY pProperty,
    _In_ ULONG ulPropertyLength,
    _Inout_updates_to_(ulDataLength, *pBytesReturned) LPVOID pPropertyData,
    _In_ ULONG ulDataLength,
    _Out_ ULONG* pBytesReturned
    );
```

传递给**IKsControl：： KSPROPERTY**方法的**KSPROPERTY**结构将包含以下信息：

```cpp
KSPROPERTY.Set = Encoder Property GUID
KSPROPERTY.Id = 0
KSPROPERTY.Flags = (KSPROPERTY_TYPE_SET or KSPROPERTY_TYPE_GET)
```

其中，编码器属性 GUID 是 [编解码器 API 属性](https://docs.microsoft.com/windows/desktop/DirectShow/codec-api-properties)中定义的可用属性列表。

编码器属性的有效负载将通过上面声明的**KsProperty**方法的*pPropertyData*字段传入。

### <a name="capture-engine-requirements"></a>捕获引擎要求

尽管帧服务器完全支持编码的源，但客户端捕获引擎 (**IMFCaptureEngine**) ， [MediaCapture](https://docs.microsoft.com/uwp/api/windows.media.capture.mediacapture) 对象使用该引擎会给出其他要求：

- 流必须全部编码 (HEVC 或 H264) 或此上下文 MJPG 中所有未压缩的 (被视为未压缩的) 。

- 必须至少有一个可用的未压缩流。

> [!NOTE]
> 除了本主题中所述的自定义媒体源要求之外，还需要满足这些要求。 但是，仅当客户端应用程序通过 **IMFCaptureEngine** 或 **MediaCapture** API 使用自定义媒体源时，才强制执行捕获引擎要求。

## <a name="camera-profiles-available-in-windows-10-version-1803-and-later"></a>在 Windows 10 版本1803及更高版本中，照相机配置文件 (可用) 

照相机配置文件支持适用于自定义媒体源。 建议的机制是通过 **MF \_ DEVICEMFT \_ SENSORPROFILE \_ COLLECTION** 属性（ ([IMFMediaSourceEx：： GetSourceAttributes](https://docs.microsoft.com/windows/win32/api/mfidl/nf-mfidl-imfmediasourceex-getsourceattributes)) 的源属性发布配置文件。

**MF \_ DEVICEMFT \_ SENSORPROFILE \_ COLLECTION**属性是[IMFSensorProfileCollection](https://docs.microsoft.com/windows/win32/api/mfidl/nn-mfidl-imfsensorprofilecollection)接口的**IUnknown** 。 可使用[MFCreateSensorProfileCollection](https://docs.microsoft.com/windows/win32/api/mfidl/nf-mfidl-mfcreatesensorprofilecollection)函数获取**IMFSensorProfileCollection** ：

```cpp
IFACEMETHODIMP
SimpleMediaSource::GetSourceAttributes(
    _COM_Outptr_ IMFAttributes** sourceAttributes
    )
{
    HRESULT hr = S_OK;
    auto lock = _critSec.Lock();

    if (nullptr == sourceAttributes)
    {
        return E_POINTER;
    }

    RETURN_IF_FAILED (_CheckShutdownRequiresLock());

    *sourceAttributes = nullptr;
    if (_spAttributes.Get() == nullptr)
    {
        ComPtr<IMFSensorProfileCollection> profileCollection;
        ComPtr<IMFSensorProfile> profile;

        // Create our source attribute store
        RETURN_IF_FAILED (MFCreateAttributes(_spAttributes.GetAddressOf(), 1));

        // Create an empty profile collection
        RETURN_IF_FAILED (MFCreateSensorProfileCollection(&profileCollection));

        // In this example since we have just one stream, we only have one
        // pin to add: Pin0

        // Legacy profile is mandatory. This is to ensure non-profile
        // aware applications can still function, but with degraded
        // feature sets.
        RETURN_IF_FAILED (MFCreateSensorProfile(KSCAMERAPROFILE_Legacy, 0, nullptr,
                                                profile.ReleaseAndGetAddressOf()));
        RETURN_IF_FAILED (profile->AddProfileFilter(0, L"((RES==;FRT<=30,1;SUT==))"));
        RETURN_IF_FAILED (profileCollection->AddProfile(profile.Get()));

        // High Frame Rate profile will only allow >=60fps
        RETURN_IF_FAILED (MFCreateSensorProfile(KSCAMERAPROFILE_HighFrameRate, 0, nullptr,
                                                profile.ReleaseAndGetAddressOf()));
        RETURN_IF_FAILED (profile->AddProfileFilter(0, L"((RES==;FRT>=60,1;SUT==))"));
        RETURN_IF_FAILED (profileCollection->AddProfile(profile.Get()));

        // See the profile collection to the attribute store of the IMFTransform
        RETURN_IF_FAILED (_spAttributes->SetUnknown(MF_DEVICEMFT_SENSORPROFILE_COLLECTION,
                                                        profileCollection.Get()));
    }

    return _spAttributes.CopyTo(sourceAttributes);
}
```

### <a name="face-authentication-profile"></a>人脸身份验证配置文件

如果自定义媒体源设计为支持 Windows Hello 面部识别，则建议发布面部身份验证配置文件。 人脸身份验证配置文件的要求如下：

- 人脸身份验证 DDI 控件在单个 IR 流上必须受支持。 有关详细信息，请参阅 [KSPROPERTY_CAMERACONTROL_EXTENDED_FACEAUTH_MODE](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-faceauth-mode)。

- IR 流必须至少为 340 x 340，15 fps。 格式必须为 L8、NV12 或用 L8 压缩标记的 MJPG。

- RGB 流必须至少为 480 x 480，每 7.5 fps (仅当强制执行 Multispectrum authentication) 时才需要。

- 人脸身份验证配置文件必须具有配置文件 ID： KSCAMERAPROFILE \_ FaceAuth \_ Mode，0。

建议人脸身份验证配置文件只为每个 IR 和 RGB 流公布一种媒体类型。

## <a name="photo-stream-controls"></a>照片流控件

如果通过将某个流的[MF \_ DEVICESTREAM \_ 流 \_ 类别](https://docs.microsoft.com/windows/desktop/medfound/mf-devicestream-stream-category) 标记为 **PINNAME \_ 映像**来公开独立照片流，则需要使用流类别为 **PINNAME \_ 视频 \_ 捕获** 的流 (例如，仅公开 **PINNAME \_ 映像** 的单个流不是有效的媒体源) 。

通过 **IKsControl**，必须支持 **PROPSETID \_ VIDCAP \_ VIDEOCONTROL** 属性集。 有关详细信息，请参阅 [视频控件属性](https://docs.microsoft.com/windows-hardware/drivers/stream/video-control-properties)。
