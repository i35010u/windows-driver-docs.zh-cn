---
title: 安装生物识别驱动程序
description: 安装生物识别驱动程序
ms.assetid: f1ae7346-c55b-484e-a94a-b4e22f5fafed
keywords:
- 生物识别驱动程序 WDK，安装
- 安装生物识别驱动程序 WDK 生物识别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afbeb83c9de5d926bd509e9c434798e46d344069
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364702"
---
# <a name="installing-a-biometric-driver"></a>安装生物识别驱动程序


供应商可以提供要安装 WBDI 驱动程序的 INF 文件。

下面是有关生物识别设备安装指南的列表。 本主题中的代码示例摘自的 WudfBioUsbSample.inx 文件[WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver):

-   WBDI 驱动程序应指定一个类的"生物识别"。 设置 ClassGuid 等于相对应的值为 GUID\_DEVCLASS\_Devguid.h 中的生物识别：

    ```cpp
    [Version]
    Signature="$Windows NT$"
    Class=Biometric
    ClassGuid={53D29EF7-377C-4D14-864B-EB3A85769359}
    ```

-   在你。硬件部分中，提供 AddReg 指令来指定三个部分，包含要添加到注册表项：

    ```cpp
    [Biometric_Install.NT.hw]
    AddReg=Biometric_Device_AddReg
    AddReg=DriverPlugInAddReg, DatabaseAddReg
    ```

-   提供命名的部分中引用。硬件部分。 \[生物识别\_设备\_AddReg\]部分设置生物识别设备，包括独占标志和系统唤醒/设备空闲状态的值。 要被识别 Windows 生物识别框架，基于 UMDF WBDI 驱动程序必须将"独占"值设置为 1。 前两行\[生物识别\_设备\_AddReg\]节中指定访问控制列表 (ACL) 权限，以便该设备只能打开由管理员或本地系统帐户。 当指定这些 ACL 权限时，第三方应用程序不能打开设备并 WinBio 服务未运行时捕获指纹数据。 例如：

    ```cpp
    [Biometric_Device_AddReg]
    HKR,,"DeviceCharacteristics",0x10001,0x0100     ; Use same security checks on relative opens
    HKR,,"Security",,"D:P(A;;GA;;;BA)(A;;GA;;;SY)"  ; Allow generic-all access to Built-in administrators and Local system
    HKR,,"LowerFilters",0x00010008,"WinUsb" ; FLG_ADDREG_TYPE_MULTI_SZ | FLG_ADDREG_APPEND
    HKR,,"Exclusive",0x10001,1
    HKR,,"SystemWakeEnabled",0x00010001,1
    HKR,,"DeviceIdleEnabled",0x00010001,1
    HKR,,"UserSetDeviceIdleEnabled",0x00010001,1
    HKR,,"DefaultIdleState",0x00010001,1
    HKR,,"DefaultIdleTimeout",0x00010001,5000
    ```

    向旧版 (非 WBDI) 生物识别堆栈公开功能的 WBDI 驱动程序应排他值设置为零。 如果此值设置为零，Windows 生物识别框架不会尝试控制设备和设备未通过 WBF 公开。

    供应商可以有单独的驱动程序二进制文件，可以使用旧堆栈和 WBF，但不能同时运行这两个。 如果设备可以打开使用独占访问权，将仅运行 WBF。

-   第二个名为的部分包含插件适配器注册表的值。 此示例使用由 Microsoft 提供的传感器适配器和存储适配器。 本部分还支持 Windows 登录名通过 SystemSensor 值设置：

    ```cpp
    [DriverPlugInAddReg]
    HKR,WinBio\Configurations,DefaultConfiguration,,"0"
    HKR,WinBio\Configurations\0,SensorMode,0x10001,1                                ; Basic - 1, Advanced - 2
    HKR,WinBio\Configurations\0,SystemSensor,0x10001,1                              ; UAC/Winlogon - 1
    HKR,WinBio\Configurations\0,SensorAdapterBinary,,"WinBioSensorAdapter.DLL"      ; Windows built-in WBDI sensor adapter.
    HKR,WinBio\Configurations\0,EngineAdapterBinary,,"EngineAdapter.DLL"            ; Vendor engine
    HKR,WinBio\Configurations\0,StorageAdapterBinary,,"WinBioStorageAdapter.DLL"    ; Windows built-in storage adapter
    HKR,WinBio\Configurations\0,DatabaseId,,"6E9D4C5A-55B4-4c52-90B7-DDDC75CA4D50"  ; Unique database GUID
    ```

-   最后，第三个区域设置的数据库服务的以下注册表值。 标识 GUID 必须是唯一的特定格式的每个供应商数据库。 例如，在此示例中的代码示例，更改为自己唯一的 GUID INF 文件中的 6E9D4C5A-55B4-4c52-90B7-DDDC75CA4D50。

    ```cpp
    [DatabaseAddReg]
    HKLM,System\CurrentControlSet\Services\WbioSrvc\Databases\{6E9D4C5A-55B4-4c52-90B7-DDDC75CA4D50},BiometricType,0x00010001,0x00000008
    HKLM,System\CurrentControlSet\Services\WbioSrvc\Databases\{6E9D4C5A-55B4-4c52-90B7-DDDC75CA4D50},Attributes,0x00010001,0x00000001
    HKLM,System\CurrentControlSet\Services\WbioSrvc\Databases\{6E9D4C5A-55B4-4c52-90B7-DDDC75CA4D50},Format,,"00000000-0000-0000-0000-000000000000"
    HKLM,System\CurrentControlSet\Services\WbioSrvc\Databases\{6E9D4C5A-55B4-4c52-90B7-DDDC75CA4D50},InitialSize,0x00010001,0x00000020
    HKLM,System\CurrentControlSet\Services\WbioSrvc\Databases\{6E9D4C5A-55B4-4c52-90B7-DDDC75CA4D50},AutoCreate,0x00010001,0x00000001
    HKLM,System\CurrentControlSet\Services\WbioSrvc\Databases\{6E9D4C5A-55B4-4c52-90B7-DDDC75CA4D50},AutoName,0x00010001,0x00000001
    HKLM,System\CurrentControlSet\Services\WbioSrvc\Databases\{6E9D4C5A-55B4-4c52-90B7-DDDC75CA4D50},FilePath,,""
    HKLM,System\CurrentControlSet\Services\WbioSrvc\Databases\{6E9D4C5A-55B4-4c52-90B7-DDDC75CA4D50},ConnectionString,,""
    ```

-   若要区分 WBDI 和旧驱动程序，供应商必须设置特征评分驱动程序 INX 文件中。 中未设置特征评分[WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)示例。 有关设置特征评分的详细信息，请参阅[排名生物识别驱动程序在 Windows 更新上](ranking-a-biometric-driver-on-windows-update.md)。

有关 INX 文件和它们之间的区别 INF 文件中的信息，请参阅[使用 INX 文件转换为创建 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-inx-files-to-create-inf-files)。

若要替换旧驱动程序为 WBDI 驱动程序，使用以下过程：

1.  关闭所有当前处于活动状态的 WBF 应用程序。

2.  卸载 WBDI 驱动程序。

3.  停止 WBF 服务，重新启动它，然后再次将其停止。

4.  安装旧驱动程序。

 

 





