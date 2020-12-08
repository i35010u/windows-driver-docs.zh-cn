---
title: 移动宽带设备固件更新
description: 本主题通过 Windows 更新 (WU) ，为移动宽带 (MB) 模块制造商提供支持固件升级设备的指南。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45008fe38b0d505a87bc21efc702e368be345d92
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818877"
---
# <a name="mobile-broadband-device-firmware-update"></a>移动宽带设备固件更新


本主题通过 Windows 更新 (WU) ，为移动宽带 (MB) 模块制造商提供支持固件升级设备的指南。 设备必须符合 usb [NCM Mobile 宽带接口模型， (MBIM) v2.0 1.0 规范](https://go.microsoft.com/fwlink/p/?linkid=320791) 由 Usb 设备工作组发布。

本主题中的信息适用于：

-   Windows 8

## <a name="device-requirements"></a>设备要求


若要使用 Windows 更新支持移动宽带上的固件更新，模块或设备制造商需要满足以下要求：

-   与 INF 文件和固件有效负载一起打包的、由模块或设备制造商开发) 基于用户模式驱动程序框架的 UMDF (。 本文档的后面部分提供了示例 INF 文件和详细信息
-   用于实现以下功能的设备固件：
    -   固件 ID 设备服务 (FID) 。 有关详细信息，请参阅 **FID 设备服务**。
    -   支持固件更新设备服务的固件。 这是设备制造商特定的设备服务，提供 UMDF 驱动程序调入和执行/下载固件负载并启动固件更新过程的能力。

**操作概述**

下图显示了所涉及的三个组件之间的高级设计和交互： MBIM 设备、Windows 8 操作系统和 IHV 提供的固件升级驱动程序。

![显示组件如何交互的图像。 下一段将对此进行介绍。](images/mbdevicefirmwareupdate.png)

-   当 WWAN 服务检测到新的 MB 设备的到达时，它将检查设备是否支持固件 ID (FID) 设备服务。 如果存在，它将检索定义为 GUID 的 FID。 **下面** 描述了 IHV 需要设备上的支持的固件设备服务规范。
-   WWAN 服务 (Windows OS) 将使用上面获得的 FID 作为设备硬件 Id 生成 "软设备节点"。这在上图中称为 "软开发节点"。 创建开发节点将启动 PnP 子系统 (Windows OS) 以查找最匹配的驱动程序。 在 Windows 8 中，PnP 系统将首先尝试从本地存储安装驱动程序（如果有），并且并行操作系统将尝试从 WU 获取更匹配的驱动程序。 如果无法使用更好的匹配驱动程序来消除 "找不到驱动程序" 问题，则将使用收件箱 NULL 驱动程序作为默认值。
-   根据 FID 匹配，将 IHV WU 包拉出到计算机并安装。 此 FID 应表示唯一的固件 SKU (唯一，此处是通过组合设备 VID/PID/REV 和 o) 来定义的。 WU 包包含 IHV 创作的 UMDF 驱动程序和固件负载。
-   在软开发节点上加载 IHV UMDF 后，它负责控制固件更新流。 应注意的是，软开发节点的生命时间与 MBIM 设备的物理状态相关。 UMDF 驱动程序应执行以下步骤来执行固件更新
    -   在固件更新过程中，设备可以多次重新启动，但会导致 UMDF 驱动程序被卸载/重装
    -   整个固件升级过程（包括重新启动）的发生时间不应超过60秒。
    -   固件更新完成并且设备已还原到 MBIM 模式后，应通知 Windows。 这是通过清除前面设置的 DEVPKEY \_ 设备 PostInstallInProgress 属性来完成的 \_ 。 **https://msdn.microsoft.com/library/windows/hardware/hh451399(v=vs.85).aspx** 介绍如何在 dev 节点上设置属性。 可以使用 DEVPROP 类型 EMPTY 清除先前设置的 \_ 属性 \_ 。
    -   在 OnPrepareHardware UMDF 回调过程中，UMDF 驱动程序应检查设备上的固件是否需要更新。 为此，可将设备上的固件版本与通过 Windows 更新中的固件版本进行比较。 稍后将在有关固件二进制放置位置的文档中提供其他指导。 如果需要固件更新，UMDF 驱动程序应：
        -   按中所述计划工作项 **https://msdn.microsoft.com/library/windows/hardware/hh463997(v=VS.85).aspx** 。 实际固件升级发生在工作项的上下文中。
        -   成功计划工作项后，请通知 Windows 有关开始固件更新的信息。 这是通过 \_ \_ 在 OnPrepareHardware UMDF 回调的上下文中设置软开发节点上的 DEVPKEY Device PostInstallInProgress 属性来完成的。
        -   固件更新过程中不会阻止 OnPrepareHardware 回调。 OnPrepareHardware 回调应最多在一秒钟或两秒钟内完成。

**WU 包的示例 INF 文件**

本部分提供属于 WU 包的示例 INF。 INF 文件中需要注意的要点如下：

-   固件二进制文件与 UMDF 驱动程序无关。
-   固件二进制文件位于众所周知的预定义位置，如下所示，文件名发生冲突。 二进制文件不能是包含 PE/COFF 标头的可执行文件。
-   `%windir%\Firmware\<IHVCompanyName>\<UniqueBinaryName>.bin`
-   UMDF 驱动程序知道此预定义的已知位置。
-   下面的示例 INF 模板包含需要由 IHV 填充的突出显示项。

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

**固件标识设备服务 (FID 设备服务)**

当由 CID \_ MBIM 设备服务进行查询时，符合 MBIM 的设备将实现并报告以下设备服务 \_ \_ 。 现有的已知服务在第10.1 节的 NCM MBIM 规范中定义。 Microsoft Corporation 扩展此项以定义以下服务。

服务名称 = **Microsoft 固件 ID**

UUID = **UUID \_ MSFWID UUID**

值 = **e9f7dea2-feaf-4009-93ce-90a3694103b6**

具体而言，为 UUID MSFWID 设备服务定义了以下 CID \_ ：

CID = **CID \_ MBIM \_ MSFWID \_ FIRMWAREID**

命令代码 = **1**

Query = **Yes**

Set = **否**

事件 = **否**

设置 InformationBuffer 负载 = **N/A**

查询 InformationBuffer 负载 = **暂缺**

完成 InformationBuffer 负载 = **UUID**

**CID \_ MBIM \_ MSFWID \_ FIRMWAREID**

此命令返回设备的 o 或 IHV 分配的固件 ID。 UUID 根据 MBIM 规范中的准则进行编码。

查询 = **\_ 未使用 MBIM 命令消息上的 InformationBuffer \_ 。在 InformationBuffer MBIM \_ 命令 \_ 完成后返回了 UUID。**

Set = **不受支持**

主动事件 = **不受支持**

**用于 UMDF 驱动程序的行为的代码段**

如前文所述，UMDF 驱动程序应在启动时向 Windows 指明 Windows 并完成固件升级。 本部分提供的代码段显示了驱动程序应如何通知 Windows 这些事件。

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

 

 





