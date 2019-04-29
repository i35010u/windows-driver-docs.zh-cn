---
title: 移动宽带设备固件更新
description: 本主题为想要支持设备固件升级通过 Windows Update (WU) 的移动宽带 (MB) 模块制造商提供指南。
ms.assetid: EBB95A11-14EF-4BF5-BE90-DB99624554CD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82939a3021ab3d670e8365b8f99f5533e2f39ced
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386245"
---
# <a name="mobile-broadband-device-firmware-update"></a>移动宽带设备固件更新


本主题为想要支持设备固件升级通过 Windows Update (WU) 的移动宽带 (MB) 模块制造商提供指南。 设备必须符合[USB NCM 移动宽带接口模型 (MBIM) V1.0 规范](https://go.microsoft.com/fwlink/p/?linkid=320791)USB 发布-如果设备使用组。

本主题中的信息适用于：

-   Windows 8

## <a name="device-requirements"></a>设备要求


若要在移动宽带使用 Windows Update 上支持固件更新，模块或设备制造商需要符合以下要求：

-   UMDF （用户模式驱动程序框架） 基于由模块开发的驱动程序或设备制造商，与 INF 文件和固件有效负载一起打包。 本文档的稍后部分中提供了示例 INF 文件和详细信息
-   设备固件，以实现以下功能：
    -   固件 ID 设备服务 (FID)。 有关详细信息，请参阅**FID 设备服务**。
    -   固件，以支持固件更新设备服务。 这是一种设备制造商特定的设备服务，提供了 UMDF 驱动程序来调用和执行/下载固件有效负载并启动固件更新过程的功能。

**操作概述**

下图显示的高级别设计和所涉及的三个组件之间的交互：MBIM 设备，Windows 8 操作系统和 IHV 提供固件升级驱动程序。

![显示组件如何交互的图像。 下一段所述。](images/mbdevicefirmwareupdate.png)

-   当 WWAN 服务检测到新的 MB 设备的到达时，它将检查如果设备支持固件 ID (FID) 设备服务。 如果存在，它会检索 FID，后者被定义为 GUID。 IHV 需要在设备上支持的固件设备服务规范所述**如下**。
-   WWAN 服务 (Windows OS) 将生成"软设备节点"使用上面获取的设备硬件 id。 作为 FID这称为"软开发节点"上图中。 创建适用于开发人员的节点将开始启动即插即用的子系统 (Windows OS) 若要查找最匹配的驱动程序。 在 Windows 8 中，即插即用系统将首先尝试从本地存储区安装驱动程序，如果可用，并在并行操作系统将尝试从 WU 获取更好地匹配的驱动程序。 收件箱 NULL 驱动程序将使用用作默认值，如果更好地匹配驱动程序不是可用于消除"找不到驱动程序"的问题。
-   IHV WU 包，基于 FID 匹配项，将向下拉取到计算机并安装。 应 FID 表示唯一固件 SKU （此处唯一性由组合设备 VID/PID/REV m n O）。 WU 包将包含 IHV 创作 UMDF 驱动程序，以及固件有效负载。
-   一旦 IHV UMDF 软开发节点上加载它负责控制固件更新流。 应注意软开发节点的生存时间与实际 MBIM 设备状态。 UMDF 驱动程序应执行以下步骤执行固件更新
    -   它是可以接受的设备在固件更新过程中，重新启动多次，但会导致 UMDF 驱动程序，才能卸载/重新加载
    -   整个固件升级过程，包括重新启动，应不超过 60 秒后发生。
    -   固件更新已完成并且设备已恢复为 MBIM 模式后，Windows 应收到通知。 这是通过清除以前设置 DEVPKEY\_设备\_PostInstallInProgress 属性。 **https://msdn.microsoft.com/library/windows/hardware/hh451399(v=vs.85).aspx** 介绍如何开发节点上设置属性。 以前的设置属性时可以使用 DEVPROP 清除\_类型\_为空。
    -   OnPrepareHardware UMDF 回调期间 UMDF 驱动程序应检查在设备上的固件是否需要更新。 这是通过比较针对传入后通过 Windows Update 设备上的固件版本。 更高版本中对放置位置的固件二进制文档提供了更多指导。 如果需要固件更新，则应 UMDF 驱动程序：
        -   计划工作项，如中所述**https://msdn.microsoft.com/library/windows/hardware/hh463997(v=VS.85).aspx**。 在工作项的上下文中进行实际固件升级。
        -   已成功计划工作项，完成后通知固件更新的启动 Windows。 可以通过设置 DEVPKEY\_设备\_PostInstallInProgress OnPrepareHardware UMDF 回调的上下文中的软开发节点的属性。
        -   不进行固件更新正在进行时阻止 OnPrepareHardware 回调至关重要。 应最完成在第二个或两个 OnPrepareHardware 回调。

**WU 包的示例 INF 文件**

本部分提供了属于 WU 包示例 INF。 请注意 INF 文件中的关键点是：

-   固件二进制文件是独立的 UMDF 驱动程序。
-   固件二进制文件的已知预定义的位置，如下所示文件名冲突。 二进制文件不能是为包含 PE/COFF 标头的可执行文件。
-   `%windir%\Firmware\<IHVCompanyName>\<UniqueBinaryName>.bin`
-   UMDF 驱动程序已知道此预定义的已知位置。
-   以下示例 INF 模板已突出显示需要由 IHV 填充的项。

```cpp
[Version]
Signature       = "$WINDOWS NT$"
Class           = Firmware
ClassGuid       = {f2e7dd72-6468-4e36-b6f1-6488f42c1b52}
Provider        = %Provider%
DriverVer       = 06/21/2006,6.2.8303.0
CatalogFile     = MBFWDriver.cat
PnpLockdown     = 1

[Manufacturer]
%Mfg%           = Firmware,NTx86

[Firmware.NTx86]
%DeviceDesc%    = Firmware_Install,MBFW\{FirmwareID}    ; From Device Service
;eg.%DeviceDesc%=Firmware_Install,MBFW\{2B13DD42-649C-3442-9E08-D85B26D7825C}

[Firmware_Install.NT]
CopyFiles       = FirmwareDriver_CopyFiles,FirmwareImage_CopyFiles

[Firmware_Install.NT.Services]
AddService      = WUDFRd,0x000001fa,WUDFRD_ServiceInstall

[WUDFRD_ServiceInstall]
DisplayName     = %WudfRdDisplayName%
ServiceType     = 1
StartType       = 3
ErrorControl    = 1
ServiceBinary   = %12%\WUDFRd.sys
LoadOrderGroup  = Base

[Firmware_Install.NT.CoInstallers]
CopyFiles       = WudfCoInstaller_CopyFiles

[WudfCoInstaller_AddReg]
HKR,,CoInstallers32,0x00010000,"WUDFCoinstaller.dll"

[Firmware_Install.NT.Wdf]
UmdfService      = MBIHVFirmwareDriver,MBIHVFirmwareDriver_Install
UmdfServiceOrder = MBIHVFirmwareDriver


[MBIHVFirmwareDriver_Install]
UmdfLibraryVersion  = 1.11
ServiceBinary       = %12%\UMDF\MBFWDriver.dll
DriverCLSID         = {<DriverClassGuid>} ; From UMDF driver

[FirmwareImage_CopyFiles]
MBIHVFirmware-XYZ-1.0.bin   ; Firmware Image

[FirmwareDriver_CopyFiles]
MBFWDriver.dll          ; UMDF driver for SoftDevNode

[DestinationDirs]
FirmwareImage_CopyFiles  = 10,Firmware\MBIHV ; %SystemRoot%\Firmware\MBIHV
FirmwareDriver_CopyFiles = 12,UMDF     ;%SystemRoot%\System32\drivers\UMDF

[SourceDisksFiles]
MBIHVFirmware-XYZ-1.0.bin = 1

[SourceDisksNames]
1 = %DiskName%

; ================== Generic ==================================

[Strings]
Provider        = "MBIHV"
Mfg             = "MBIHV"
DeviceDesc      = "MBIHV Mobile Broadband Firmware Device"
DiskName        = "Firmware Driver Installation Media"
```

**固件标识设备服务 （FID 设备服务）**

MBIM 兼容设备会实现并报告以下设备服务 CID 进行查询时\_MBIM\_设备\_服务。 在部分 10.1 NCM MBIM 规范中定义现有的已知服务。 Microsoft Corporation 扩展，以便定义以下服务。

服务名称 = **Microsoft 固件 ID**

UUID = **UUID\_MSFWID UUID**

Value = **e9f7dea2-feaf-4009-93ce-90a3694103b6**

具体而言，以下 CID 定义的 UUID\_MSFWID 设备服务：

CID = **CID\_MBIM\_MSFWID\_FIRMWAREID**

命令代码 = **1**

查询 =**是**

设置 =**否**

事件 =**否**

设置 InformationBuffer 负载 = **n/A**

查询 InformationBuffer 负载 = **n/A**

完成 InformationBuffer 负载 = **UUID**

**CID\_MBIM\_MSFWID\_FIRMWAREID**

该命令返回的 MNO 或 IHV 分配设备的固件 ID。 UUID 被编码的基于 MBIM 规范中的准则。

查询 = **InformationBuffer 上 MBIM\_命令\_未使用的消息。UUID 返回 InformationBuffer MBIM\_命令\_完成。**

设置 =**不受支持**

未经请求的事件 =**不受支持**

**UMDF 驱动程序的行为的代码片段**

如先前所述，它开始和完成固件升级时，应该向 Windows 指明 UMDF 驱动程序。 本部分提供的代码片段的显示驱动程序应如何通知这些事件的 Windows。

```cpp
/**
 * This is the IPnpCallbackHardware*:OnPrepareHardware handler 
 * in the UMDF driver. This is called every time the firmware 
 * update is device is started. Since this handler should be 
 * blocked from returning actual the firmware update process 
 * should be done in a workitem 
 */
HRESULT
CMyDevice::OnPrepareHardware(IWDFDevice* pDevice)
{
    HRESULT hr = S_OK;
    BOOL bFirmwareUpdateInProgress = FALSE;
    BOOL bFirmwareUpdateNeeded = FALSE;
    BOOL bFirmwareUpdateIsDone = FALSE;

    //
    // The snippets below demonstrates the steps for firmware 
    // update against a MB device that loads the updated firmware 
    // on device boot. So the firmware update driver needs to
    // send the new firmware down to the device and then tell 
    // the device to initiate a stop/start. Once the device has
    // reappeared, it would have automatically loaded the 
    // new firmware
    // 


    //
    // First, determine if firmware update is in progress. This 
    // can be based on some registry key that is saved when
    // firmware update is started
    //

    // Assuming this status is returned in bFirmwareUpdateInProgress
    if (bFirmwareUpdateInProgress)
    {
        //
        // If firmware update is in progress, check if its done. For
        // this it may be necessary to access the MB device. Note that 
        // if the MB device (& hence the Firmware update device) needs
        // multiple stop/starts to do the firmware update. In that case
        // it will be marked as done at the end of the process
        //

        // Assuming this status is returned in bFirmwareUpdateIsDone
        if (bFirmwareUpdateIsDone)
        {
            //
            // Signal the completion of the firmware update
            // process.
            //
            SignalFirmwareUpdateComplete(pDevice);
        }
        else
        {
            //
            // Take appropriate steps to get notified when
            // firmware update is done. Call SignalFirmwareUpdateComplete
            // when that notification is received
            //
        }
    }
    else
    {
        //
        // Determine if firmware update is needed. This can be 
        // based on checking state in the registry of the last
        // firmware version set on the device to the firmware
        // version associated with this driver
        //
        
        // Assuming this status is returned in bFirmwareUpdateNeeded
        if (bFirmwareUpdateNeeded)
        {
            // 
            // Create and queue a workitem to perform the firmware
            // update process. IWDFWorkItem can be used for this
            //
            
            // Assuming the creation/enquing status
            // is returned in hr
            
            if (SUCCEEDED(hr))
            {
                //
                // Work item queued. It will do the firmware update
                // Tell the OS that firmware update is in progress
                //
                SignalFirmwareUpdateInProgress(pDevice);
            }
        }
    }

    //
    // If we have a failure, we clear the firmware update
    // in progress state
    //
    if (FAILED(hr))
    {
        SignalFirmwareUpdateComplete(pDevice);
    }
    return S_OK;
}

/**
 * This function tells the OS that firmware update is in progress.
 * It should be called from the firmware update UMDF driver's 
 * IPnpCallbackHardware*:OnPrepareHardware handler after it has
 * successfully queued a workitem to perform the firmware update
 */
HRESULT
CMyDevice::SignalFirmwareUpdateInProgress(
    __in IWDFDevice* pDevice
    )
{
    HRESULT hr = S_OK;    
    IWDFUnifiedPropertyStoreFactory* spPropertyStoreFactory = NULL;
    IWDFUnifiedPropertyStore* spPropStore = NULL;
    WDF_PROPERTY_STORE_ROOT wdfPropRoot = { sizeof(WDF_PROPERTY_STORE_ROOT), WdfPropertyStoreRootClassHardwareKey };
    DEVPROP_BOOLEAN boolValue = DEVPROP_TRUE;
    
    do
    {
       
        hr = pDevice->QueryInterface(IID_PPV_ARGS(&spPropertyStoreFactory));
        if (FAILED(hr))
        {
            Trace(TRACE_LEVEL_ERROR, "Failed to query for property store factory. Error = 0x%x", hr);
            break;

        }
        
        hr = spPropertyStoreFactory->RetrieveUnifiedDevicePropertyStore(
            &wdfPropRoot,
            &spPropStore
            );
        if (FAILED(hr))
        {
            Trace(TRACE_LEVEL_ERROR, "Failed to query for device property store. Error = 0x%x", hr);
            break;
        }

        // Set the OS flag
        hr = spPropStore->SetPropertyData(
            reinterpret_cast<const DEVPROPKEY*>(&DEVPKEY_Device_PostInstallInProgress),
            0, // this property is language neutral
            0,
            DEVPROP_TYPE_BOOLEAN,
            sizeof(DEVPROP_BOOLEAN),
            &boolValue
            );
        if (FAILED(hr))
        {
            Trace(TRACE_LEVEL_ERROR, "Failed to set device property for PostInstallInProgress. Error = 0x%x", hr);
            break;
        }

        //
        // Save some state so that we know we are in the process
        // of firmware update
        //
    } while (FALSE);        

    if (spPropStore)
    {
        spPropStore->Release();
    }

    if (spPropertyStoreFactory)
    {
        spPropertyStoreFactory->Release();
    }

    return hr;
}


/**
 * This function tells the OS that firmware update is done
 * It should be called only after the full firmware update process
 * (including any MB device stop/start) has finished
 */
HRESULT
CMyDevice::SignalFirmwareUpdateComplete(
    __in IWDFDevice* pDevice
    )
{
    HRESULT hr = S_OK;    
    IWDFUnifiedPropertyStoreFactory* spPropertyStoreFactory = NULL;
    IWDFUnifiedPropertyStore* spPropStore = NULL;
    WDF_PROPERTY_STORE_ROOT wdfPropRoot = { sizeof(WDF_PROPERTY_STORE_ROOT), WdfPropertyStoreRootClassHardwareKey };
    
    do
    {
        hr = pDevice->QueryInterface(IID_PPV_ARGS(&spPropertyStoreFactory));
        if (FAILED(hr))
        {
            Trace(TRACE_LEVEL_ERROR, "Failed to query for property store factory. Error = 0x%x", hr);
            break;

        }

        hr = spPropertyStoreFactory->RetrieveUnifiedDevicePropertyStore(
            &wdfPropRoot,
            &spPropStore
            );
        if (FAILED(hr))
        {
            Trace(TRACE_LEVEL_ERROR, "Failed to query for device property store. Error = 0x%x", hr);
            break;
        }

        hr = spPropStore->SetPropertyData(
            reinterpret_cast<const DEVPROPKEY*>(&DEVPKEY_Device_PostInstallInProgress),
            0, // this property is language neutral
            0,
            DEVPROP_TYPE_BOOLEAN,
            0,
            NULL
            );
        if (FAILED(hr))
        {
            Trace(TRACE_LEVEL_ERROR, "Failed to clear device property for PostInstallInProgress. Error = 0x%x", hr);
            break;
        }

        //
        // Save some state so that we can do quick check on 
        // whether firmware update is needed or not
        //

    } while (FALSE);        

    if (spPropStore)
    {
        spPropStore->Release();
    }

    if (spPropertyStoreFactory)
    {
        spPropertyStoreFactory->Release();
    }

    return hr;
}
```

 

 





