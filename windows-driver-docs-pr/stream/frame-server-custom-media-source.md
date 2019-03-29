---
title: Frame Server 自定义媒体源
description: 提供有关实现自定义媒体源帧服务器体系结构中的信息。
ms.date: 10/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 825540b9854f2431017c8ce86772ec7119f406b1
ms.sourcegitcommit: 68bfa1f69229b7ac29d0e98f049734f5bc566a30
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2019
ms.locfileid: "58187470"
---
# <a name="frame-server-custom-media-source"></a>Frame Server 自定义媒体源 

本主题提供信息上的帧服务器体系结构内的自定义媒体源的实现。 

## <a name="av-stream-and-custom-media-source-options"></a>AV Stream 和自定义媒体源选项

在决定如何提供视频捕获帧服务器体系结构中的流支持，有两个主要选项：AV Stream 和自定义媒体源。

AV Stream 模型是使用 AV Stream 微型端口驱动程序 （内核模式驱动程序） 的标准照相机驱动程序模型。 通常 AV Stream 驱动程序划分为两个主要类别：MIPI 基于驱动程序和 USB 视频类驱动程序。

自定义媒体源选项时，可能是完全自定义驱动程序模型 （专有） 或可能基于非传统相机源 （如文件或网络源）。

### <a name="av-stream-driver"></a>AV Stream 驱动程序

AV Stream 驱动程序方法的主要优势是即插即用和电源管理/设备管理已由 AV Stream 框架进行处理。

但是，它还意味着基础数据源必须使用内核模式驱动程序，以便与硬件的物理设备。 对于 UVC 设备，Windows UVC 1.5 类驱动程序已提供收件箱，因此设备只需实现其固件。

MIPI 基于设备的供应商需要实现自己的 AV Stream 微型端口驱动程序。

### <a name="custom-media-source"></a>自定义媒体源

为其设备驱动程序已经可用 （但不是 AV Stream 微型端口驱动程序） 的源或源使用非传统相机捕捉，AV Stream 驱动程序可能不可行。 例如，通过网络连接 IP 相机无法适应 AV Stream 驱动程序模型。

在这种情况下，使用帧服务器模型的自定义媒体源将是一种替代方法。

| 功能 | 自定义媒体源 | AV Stream 驱动程序 |
|---|---|---|
| PnP 和电源管理 | 必须由源和/或存根 （stub） 驱动程序实现 | AV Stream 框架提供的 |
| 用户模式下插件       | 不可用。 自定义媒体源整合了 OEM/IHV 特定的用户模式逻辑。 | DMFT、 平台 DMFT 和旧实现 MFT0 |
| 传感器组 | 支持 | 支持 |
| 照相机配置文件 V2 | 支持 | 支持 |
| 照相机配置文件 V1 | 不支持 | 支持 |

## <a name="custom-media-source-requirements"></a>自定义媒体源的要求

随着 Windows 照相机帧服务器 （称为帧服务器） 服务，这可以通过实现自定义媒体源。 这需要两个主要组件：

-   与用于注册/启用照相机设备接口的存根驱动程序的驱动程序包。

-   COM DLL，它承载自定义媒体源。

第一个要求是所需的两个用途：

-   通过受信任的进程 （驱动程序包需要经历 WHQL 认证） 进行安装以确保自定义媒体源的进行审核。

-   支持标准的即插即用枚举和发现"照相机"。

### <a name="security"></a>安全性

帧服务器的自定义媒体源按以下方式不同于一般的自定义媒体源在安全性方面：

-   作为本地服务 （不会与本地系统; 混淆运行帧 Server 自定义媒体源本地服务是非常低特权的帐户在 Windows 计算机上）。

-   帧 Server 自定义媒体源在会话 0 （系统服务会话） 中运行，并不能与用户桌面进行交互。

给定这些约束，帧 Server 自定义媒体源必须不尝试访问受保护的文件系统和注册表部分。 通常情况下，允许读取访问权限，但不是写访问权限。

### <a name="performance"></a>性能

帧服务器模型的一部分，将如何在帧服务器实例化自定义媒体源中有两种情况：

-   在传感器组生成/发布。

-   在"照相机"激活过程

传感器组生成通常是在设备安装和/或电源周期期间。 鉴于此，我们强烈建议自定义媒体源避免在创建期间及其任何重大处理，并将推迟到任何此类活动[IMFMediaSource::Start](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasource-start)函数。 传感器组生成不会尝试启动自定义媒体源，只是查询的各种可用的流媒体类型和源/流属性信息。

## <a name="stub-driver"></a>存根 （stub） 驱动程序

有两个驱动程序包和存根 （stub） 驱动程序的最低要求。

可以使用 WDF （UMDF 或 KMDF） 或 WDM 驱动程序模型编写的存根 （stub） 驱动程序。

驱动程序要求如下：

-   注册下的你"照相机"（自定义媒体源） 设备接口[KSCATEGORY_VIDEO_CAMERA](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-video-camera)类别，因此可以枚举。

> [!NOTE]
> 若要允许枚举的 DirectShow 的旧应用程序，您的驱动程序将需要还注册下[KSCATEGORY_VIDEO](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-video)并[KSCATEGORY_CAPTURE](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-capture)。

-   添加设备接口节点下的注册表项 (使用**AddReg**驱动程序 INF 中指令**DDInstall.Interface**部分) 的声明您的自定义媒体源 COM 可可以共同创建的 CLSID对象。 必须使用以下注册表值名称添加此：**CustomCaptureSourceClsid**。

这允许要发现的应用程序的"照相机"源，并激活时，通知将帧服务器服务截获激活调用并重新将其路由到共同创建自定义媒体源。

### <a name="sample-inf"></a>示例 INF

下面的示例显示了自定义媒体源存根 （stub） 驱动程序的典型 INF:

```INF
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

上面的自定义媒体源注册下**KSCATEGORY\_视频**， **KSCATEGORY\_捕获**，以及**KSCATEGORY\_视频\_照相机**以确保"照相机"是可发现的搜索标准的 RGB 照相机任何 UWP 和非 UWP 应用。

如果自定义媒体源还公开非 RGB 流 （红外线 （ir）、 深度和等等） 它可以选择性地还注册下[KSCATEGORY_SENSOR_CAMERA](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-sensor-camera)。

> [!NOTE]
> 大多数基于 USB 网络摄像机将公开 YUY2 和 MJPG 格式。 由于此行为，许多旧 DirectShow 应用程序在编写 YUY2/MJPG 是可用的假设。 若要确保与此类应用程序兼容性，建议，YUY2 媒体类型可从您的自定义媒体源如果需要旧应用程序兼容性。

### <a name="stub-driver-implementation"></a>存根 （stub） 驱动程序实现

除了 INF，驱动程序存根 （stub） 也必须注册并启用照相机设备接口。 这通常是期间**驱动程序\_添加\_设备**操作。

请参阅[DRIVER_ADD_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device) WDM 的回调函数基于驱动程序和[WdfDriverCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdrivercreate) UMDF/KMDF 驱动程序的函数。

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
    // later in SotwareInit.
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

### <a name="pnp-operation"></a>即插即用操作

就像任何其他物理照相机，建议您存根 （stub） 的驱动程序管理至少启用和禁用设备时的基础源是删除附加的即插即用操作。 例如，如果您的自定义媒体源使用网络源 （如 IP 照相机），你可能想要该网络源不再可用时触发设备删除。

这可确保，应用程序侦听的设备添加/删除通过即插即用的 Api 获取适当的通知。 并确保不再可用的源不能枚举。

UMDF 和 KMDF 驱动程序，请参阅[WdfDeviceSetDeviceState](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetdevicestate)函数文档。

WMD 驱动程序，请参阅[IoSetDeviceInterfaceState](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetdeviceinterfacestate)函数文档。

## <a name="custom-media-source-dll"></a>自定义媒体源 DLL

自定义媒体源是标准进程内 COM 服务器，它必须实现以下接口：

-   [IMFMediaEventGenerator](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfmediaeventgenerator)

-   [IMFMediaSource](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfmediasource)

-   [IMFMediaSourceEx](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfmediasourceex)

-   [IKsControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nn-ks-ikscontrol)

-   [IMFGetService](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfgetservice)

> [!NOTE]
> **IMFMediaSourceEx**继承自**IMFMediaSource**并**IMFMediaSource**继承**IMFMediaEventGenerator**。

自定义媒体源中的每个受支持的流必须支持以下接口：

-   **IMFMediaEventGenerator**

-   [IMFMediaStream](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfmediastream)

-   **IMFMediaStream2**

> [!NOTE]
> **IMFMediaStream2**继承自**IMFMediaStream**并**IMFMediaStream**继承**IMFMediaEventGenerator**。

请参阅[编写自定义媒体源](https://docs.microsoft.com/windows/desktop/medfound/writing-a-custom-media-source)文档介绍了如何创建自定义媒体源。 本部分的其余部分将介绍支持您自定义的媒体源帧服务器框架内所需的差异。

### <a name="imfgetservice"></a>IMFGetService

**IMFGetService**帧服务器自定义媒体源是必需的接口。 **IMFGetService**可能会返回**MF\_E\_不支持\_服务**如果您的自定义媒体源不需要公开任何其他服务的接口。

下面的示例演示**IMFGetService**和没有支持服务接口的实现：

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

如上所示，在源和源中的单个流必须支持其自己[IMFMediaEventGenerator](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfmediaeventgenerator)接口。 通过发送特定事件生成器通过进行管理的整个 MF 管道数据和控制流从源[IMFMediaEvent](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfmediaevent)。

为了实现 IMFMediaEventGenerator，必须使用自定义媒体源[MFCreateEventQueue](https://docs.microsoft.com/windows/desktop/api/mfapi/nf-mfapi-mfcreateeventqueue) API 来创建[IMFMediaEventQueue](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfmediaeventqueue) ，并将路由的所有方法**IMFMediaEventGenerator**对队列对象：

**IMFMediaEventGenerator**具有以下方法：

```cpp
// IMFMediaEventGenerator
IFACEMETHOD(BeginGetEvent)(_In_ IMFAsyncCallback *pCallback, _In_ IUnknown *punkState);
IFACEMETHOD(EndGetEvent)(_In_ IMFAsyncResult *pResult, _COM_Outptr_ IMFMediaEvent **ppEvent);
IFACEMETHOD(GetEvent)(DWORD dwFlags, _Out_ IMFMediaEvent **ppEvent);
IFACEMETHOD(QueueEvent)(MediaEventType met, REFGUID guidExtendedType, HRESULT hrStatus, _In_opt_ const PROPVARIANT *pvValue);
```

下面的代码演示的推荐的实现**IMFMediaEventGenerator**接口。 自定义媒体源实现都会公开**IMFMediaEventGenerator**接口，以及该接口的方法将为将请求路由**IMFMediaEventQueue**对象媒体源创建/初始化期间创建。

在下面的代码，  **\_spEventQueue**对象是**IMFMediaEventQueue**使用创建**MFCreateEventQueue**函数：

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

通过框架服务器框架支持的自定义媒体源不支持 Seek 或暂停操作。 您的自定义媒体源不需要为这些操作提供支持，并且必须发布**MFSourceSeeked**或**MEStreamSeeked**事件。

[IMFMediaSource::Pause](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasource-pause)应返回**MF\_E\_无效\_状态\_转换**(或**MF\_E\_关闭**如果源已关闭)。

### <a name="ikscontrol"></a>IKsControl

[IKsControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nn-ks-ikscontrol)是标准控件界面，用于所有照相机相关控件。 如果自定义媒体源实现任何照相机控件**IKsControl**接口是管道将控制 I/O 的路由。

有关详细信息，请参阅下列控件设置文档主题：

-   [PROPSETID_VIDCAP_CAMERACONTROL](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-cameracontrol)

-   [PROPSETID_VIDCAP_VIDEOPROCAMP](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videoprocamp)

-   [KSPROPERTYSETID_ExtendedCameraControl](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropertysetid-extendedcameracontrol)

控件是可选的如果不支持，是要返回的建议的错误代码**HRESULT\_FROM\_WIN32 (错误\_集\_NOT\_找到)**。

下面的代码是一个示例**IKsControl**没有受支持的控件的实现：

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

中所述[编写自定义媒体源](https://docs.microsoft.com/windows/desktop/medfound/writing-a-custom-media-source)，则**IMFMediaStream2**从自定义媒体源通过接口提供给帧工作[MENewStream](https://docs.microsoft.com/windows/desktop/medfound/menewstream)媒体事件的完成期间发送到源事件队列[IMFMediaSource::Start](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasource-start)方法：

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

此操作必须通过选择的每个流的执行[IMFPresentationDescriptor](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfpresentationdescriptor)。

为视频流使用自定义媒体源[MEEndOfStream](https://docs.microsoft.com/windows/desktop/medfound/meendofstream)并[MEEndOfPresentation](https://docs.microsoft.com/windows/desktop/medfound/meendofpresentation)不应发送事件。

### <a name="stream-attributes"></a>Stream 属性

自定义媒体源的所有流必须都具有[MF_DEVICESTREAM_STREAM_CATEGORY](https://docs.microsoft.com/windows/desktop/medfound/mf-devicestream-stream-category)设置为**PINNAME\_视频\_捕获**。 **PINNAME\_视频\_预览**自定义媒体源不支持。

> [!NOTE]
> **PINNAME\_图像**，而受支持，不建议。 公开与流**PINNAME\_映像**要求要支持所有照片触发器控件的自定义媒体源。 请参阅[照片 Stream 控件](#photo-stream-controls)部分获取更多详细信息。

[MF_DEVICESTREAM_STREAM_ID](https://docs.microsoft.com/windows/desktop/medfound/mf-devicestream-stream-id)是所有流的一个必需属性。 它应该是基于 0 的索引。 因此第一个流的 ID 为 0，第二个流的 ID 为 1，依此类推。

以下是建议的流属性的列表：

-   [MF_DEVICESTREAM_ATTRIBUTE_FRAMESOURCE_TYPES](https://docs.microsoft.com/windows/desktop/medfound/mf-devicestream-attribute-framesource-types)

-   [MF_DEVICESTREAM_FRAMESERVER_SHARED](https://docs.microsoft.com/windows/desktop/medfound/mf-devicestream-frameserver-shared)

#### <a name="mfdevicestreamattributeframesourcetypes"></a>MF\_DEVICESTREAM\_特性\_框架资源\_类型

**MF\_DEVICESTREAM\_特性\_框架资源\_类型**是一种 UINT32 属性，这是流类型的掩码值。 它可能被设置为以下任一 （尽管这些类型的位掩码标志，它是建议的源类型不能与混合如果可能）：

| 在任务栏的搜索框中键入                         | Flag   | 描述                                      |
|------------------------------|--------|--------------------------------------------------|
| MFFrameSourceTypes\_Color    | 0x0001 | 标准的 RGB 颜色流                        |
| MFFrameSourceTypes\_Infrared | 0x0002 | 红外线 （ir） 流                                        |
| MFFrameSourceTypes\_Depth    | 0x0004 | 深度流                                     |
| MFFrameSourceTypes\_Image    | 0x0008 | 图像流 （非视频子类型，通常 JPEG） |
| MFFrameSourceTypes\_Custom   | 0x0080 | 自定义流类型                               |

#### <a name="mfdevicestreamframeservershared"></a>MF\_DEVICESTREAM\_FRAMESERVER\_SHARED

**MF\_DEVICESTREAM\_FRAMESERVER\_共享**为 UINT32 属性都被设置为 0 或 1。 如果设置为 1，则会标记为"共享"帧服务器的流。 这将允许应用程序在共享模式下打开流，即使使用的另一个应用。

如果未设置此属性，帧服务器将允许第一个非标记流共享 (如果自定义媒体源具有只有一个流，该流将被标记为共享)。

如果此属性设置为 0，帧服务器将阻止从共享应用程序的流。 如果自定义媒体源标记的所有流使用此属性设置为 0，没有任何共享的应用程序将能够初始化源。

### <a name="sample-allocation"></a>示例分配

必须作为生成所有媒体帧[IMFSample](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfsample)。 必须使用自定义媒体源[MFCreateSample](https://docs.microsoft.com/windows/desktop/api/mfapi/nf-mfapi-mfcreatesample)函数以分配 IMFSample 和使用的实例[AddBuffer](https://docs.microsoft.com/windows/desktop/api/mfobjects/nf-mfobjects-imfsample-addbuffer)方法中添加媒体缓冲区。

每个**IMFSample**必须具有的采样时间和设置的示例持续时间。 所有示例时间戳必须都基于 QPC 时间 (QueryPerformanceCounter)。

建议使用自定义媒体源[MFGetSystemTime](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-mfgetsystemtime)函数在可能的情况。 此函数是一个包装**QueryPerformanceCounter**并将 QPC 计时周期数转换为 100 纳秒为单位。

自定义媒体源可能会使用内部时钟，但所有时间戳必须关联到基于当前 QPC 的 100 纳秒为单位。

#### <a name="media-buffer"></a>媒体缓冲区

添加到的所有媒体缓冲区**IMFSample**必须使用标准 MF 缓冲区分配函数。 自定义媒体源必须实现其自己[IMFMediaBuffer](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfmediabuffer)接口或尝试直接分配媒体缓冲区 （例如，新/malloc/VirtualAlloc，以此类推，必须不用于帧数据）。

使用以下 Api 的任何分配媒体帧：

-   [MFCreateMemoryBuffer](https://docs.microsoft.com/windows/desktop/api/mfapi/nf-mfapi-mfcreatememorybuffer)

-   [MFCreateAlignedMemoryBuffer](https://docs.microsoft.com/windows/desktop/api/mfapi/nf-mfapi-mfcreatealignedmemorybuffer)

-   [MFCreate2DMediaBuffer](https://docs.microsoft.com/windows/desktop/api/mfapi/nf-mfapi-mfcreate2dmediabuffer)

-   [MFCreateDXGISurfaceBuffer](https://docs.microsoft.com/windows/desktop/api/mfapi/nf-mfapi-mfcreatedxgisurfacebuffer)

**MFCreateMemoryBuffer**并**MFCreateAlignedMemoryBuffer**应该用于非 stride 对齐的媒体数据。 这些通常是自定义子类型或压缩子类型 （如 H264/HEVC/MJPG)。

已知未压缩的媒体类型 （例如 YUY2、 NV12，等） 使用的系统内存，建议使用**MFCreate2DMediaBuffer**。

（有关在 GPU 加速操作如呈现和/或编码），使用 DX 表面**MFCreateDXGISurfaceBuffer**应使用。

**MFCreateDXGISurfaceBuffer**不会创建 DX 图面。 使用传递到媒体源通过 DXGI 管理器创建在图面[IMFMediaSourceEx::SetD3DManager](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasourceex-setd3dmanager)方法。

[IMFDXGIDeviceManager::OpenDeviceHandle](https://docs.microsoft.com/windows/desktop/api/mfobjects/nf-mfobjects-imfdxgidevicemanager-opendevicehandle)将提供与所选的 D3D 设备关联的句柄。 [ID3D11Device](https://docs.microsoft.com/windows/desktop/api/d3d11/nn-d3d11-id3d11device)接口可以然后使用获取[IMFDXGIDeviceManager::GetVideoService](https://docs.microsoft.com/windows/desktop/api/mfobjects/nf-mfobjects-imfdxgidevicemanager-getvideoservice)方法。

无论使用哪种类型的缓冲区， **IMFSample**创建必须提供给通过管道**MEMediaSample**上的事件**IMFMediaEventGenerator**的媒体流中。

虽然可以使用同一**IMFMediaEventQueue**自定义媒体源和基础集合**IMFMediaStream**，应注意的是，这样做将导致序列化媒体源的事件和流的事件 （其中包括媒体流）。 对于具有多个流的源，这是不可取。

下面的代码截图显示了媒体流的示例实现：

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

## <a name="custom-media-source-extension-to-expose-imfactivate-available-in-windows-10-version-1809"></a>自定义媒体源扩展公开 IMFActivate （适用于 Windows 10，版本 1809年）

除了上述列表中的自定义媒体源必须支持的接口，由框架服务器体系结构中的自定义媒体源操作施加的限制之一是，只能有一个实例的"激活"UMDF 驱动程序通过管道。

例如，如果有安装除了其 AV Stream 驱动程序包的 UMDF 存根 （stub） 驱动程序的物理设备并将多个这些物理设备连接到计算机，UMDF 驱动程序的每个实例时将获得唯一的符号链接名称自定义媒体源的激活路径不会在创建时与自定义媒体源相关联的符号链接名称通信的方式。

自定义媒体源的标准可能看起来[MF_DEVSOURCE_ATTRIBUTE_SOURCE_TYPE_VIDCAP_SYMBOLIC_LINK](https://docs.microsoft.com/windows/desktop/medfound/mf-devsource-attribute-source-type-vidcap-symbolic-link)中自定义媒体源的属性存储 （属性存储从通过自定义媒体源返回的属性[IMFMediaSourceEx::GetSourceAttributes](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasourceex-getsourceattributes)方法) 时[IMFMediaSource::Start](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasource-start)调用。

但是，这可能会导致延迟更高版本启动因为这将在硬件资源获取启动时间，而不是创建/初始化时间延迟。

因此，在 Windows 10，版本 1809，自定义媒体源可能会选择公开[IMFActivate](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfactivate)接口。

> [!NOTE] 
> **IMFActivate**继承自[IMFAttributes](https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfattributes)。

### <a name="imfactivate"></a>IMFActivate

自定义媒体源的 COM 服务器是否支持**IMFActivate**接口，设备初始化信息将提供给 COM 服务器通过**IMFAttributes** 由继承**IMFActivate**。 因此，在[IMFActivate::ActivateObject](https://docs.microsoft.com/windows/desktop/api/mfobjects/nf-mfobjects-imfactivate-activateobject)调用时，该属性存储区**IMFActivate**将包含的符号链接名称 UMDF 存根 （stub） 驱动程序以及任何其他配置设置在源创建/初始化时提供的管道/应用程序。

自定义媒体源应使用此方法调用来获取其所需的任何硬件资源。

> [!NOTE]
> 如果硬件资源获取需要大于 200 毫秒，则建议以异步方式获取硬件资源。 自定义媒体源的激活不应阻塞硬件资源获取。 相反[IMFMediaSource::Start](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasource-start)应针对硬件资源获取序列化操作。

通过公开的两个附加方法**IMFActivate**， [DetachObject](https://docs.microsoft.com/windows/desktop/api/mfobjects/nf-mfobjects-imfactivate-detachobject)并[ShutdownObject](https://docs.microsoft.com/windows/desktop/api/mfobjects/nf-mfobjects-imfactivate-shutdownobject)，必须返回**E\_NOTIMPL**.

自定义媒体源可能选择实施**IMFActivate**并**IMFAttributes**中相同的 COM 对象作为接口[IMFMediaSource](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfmediasource)。 如果此操作后，建议[IMFMediaSourceEx::GetSourceAttributes](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasourceex-getsourceattributes)返回相同**IMFAttributes**接口用作来自**IMFActivate**。

如果自定义媒体源不实现**IMFActivate**并**IMFAttributes**自定义媒体源必须使用相同的对象，将复制上设置的所有属性**IMFActivate**自定义媒体源的源属性存储到的属性存储。

## <a name="encoded-camera-stream"></a>编码的照相机 Stream

自定义媒体源可能会公开压缩的媒体类型 （HEVC 或 H264 基本流） 和 OS 管道完全支持的源和编码的参数的配置，自定义媒体源上 (通过与编码的参数进行沟通[ICodecAPI](https://docs.microsoft.com/previous-versions/windows/desktop/api/strmif/nn-strmif-icodecapi)，这作为路由[IKsControl::KsProperty](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nf-ksproxy-ikscontrol-ksproperty)调用):

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

**KSPROPERTY**结构传递到**IKsControl::KsProperty**方法将具有以下信息：

```cpp
KSPROPERTY.Set = Encoder Property GUID
KSPROPERTY.Id = 0
KSPROPERTY.Flags = (KSPROPERTY_TYPE_SET or KSPROPERTY_TYPE_GET)
```

其中编码器属性 GUID 是中定义的可用属性的列表[编解码器 API 属性](https://docs.microsoft.com/windows/desktop/DirectShow/codec-api-properties)。

编码器属性的有效负载部分将通过传入*pPropertyData*字段**KsProperty**前面声明的方法。

### <a name="capture-engine-requirements"></a>捕获引擎要求

客户端时由框架服务器完全支持编码的源，端捕获引擎 (**IMFCaptureEngine**) 以供[Windows.Media.Capture.MediaCapture](https://docs.microsoft.com/uwp/api/windows.media.capture.mediacapture)对象施加其他要求：

-   Stream 必须是所有编码 （HEVC 或 H264） 或所有未压缩 (在此上下文中处理 MJPG 为未压缩)。

-   必须有至少一个未压缩的流。

> [!NOTE]
> 这些要求是除了本主题中所述的自定义媒体源要求。 但是，捕获引擎要求才会强制执行客户端应用程序使用通过自定义媒体源时**IMFCaptureEngine**或**Windows.Media.Capture.MediaCapture** API。

## <a name="camera-profiles-available-in-windows-10-version-1803-and-later"></a>照相机配置文件 （适用于 Windows 10，版本 1803年和更高版本）

照相机配置文件的支持是可用于自定义媒体源。 建议的机制是要发布到配置文件**MF\_DEVICEMFT\_SENSORPROFILE\_集合**关闭源属性的属性 ([IMFMediaSourceEx::GetSourceAttributes](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-imfmediasourceex-getsourceattributes))。

**MF\_DEVICEMFT\_SENSORPROFILE\_集合**属性是**IUnknown**的[IMFSensorProfileCollection](https://docs.microsoft.com/windows/desktop/api/mfidl/nn-mfidl-imfsensorprofilecollection)接口。 **IMFSensorProfileCollection**可以使用获取[MFCreateSensorProfileCollection](https://docs.microsoft.com/windows/desktop/api/mfidl/nf-mfidl-mfcreatesensorprofilecollection)函数：

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

如果自定义媒体源设计为支持 Windows Hello 面部识别，然后建议发布人脸身份验证配置文件。 人脸身份验证配置文件的要求如下：

-   人脸验证 DDI 控件必须支持在单个的红外线 （ir） 流上。 有关详细信息，请参阅[KSPROPERTY_CAMERACONTROL_EXTENDED_FACEAUTH_MODE](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-faceauth-mode)。

-   红外线 （ir） 流必须是至少 340 x 340 在 15 每秒帧数。 格式必须为 L8、 NV12 或 MJPG 标有 L8 压缩。

-   RGB 流必须是至少 480x480 在 7.5 每秒帧数 （这仅当需要强制进行 Multispectrum 身份验证）。

-   人脸身份验证配置文件必须具有的配置文件 ID:KSCAMERAPROFILE\_FaceAuth\_模式，0。

我们建议使用人脸身份验证配置文件仅为每个红外线 （ir） 和 RGB 流公告一种媒体类型。

## <a name="photo-stream-controls"></a>照片 Stream 控件

如果通过将一个流的标记来公开独立的照片流[MF\_DEVICESTREAM\_流\_类别](https://docs.microsoft.com/windows/desktop/medfound/mf-devicestream-stream-category)作为**PINNAME\_映像**，然后流类别为流**PINNAME\_视频\_捕获**是必需的 (例如，单个流公开只**PINNAME\_映像**不是有效的媒体源)。

通过**IKsControl**，则**PROPSETID\_VIDCAP\_VIDEOCONTROL**必须支持属性集。 有关详细信息，请参阅[视频控件属性](https://docs.microsoft.com/windows-hardware/drivers/stream/video-control-properties)。
