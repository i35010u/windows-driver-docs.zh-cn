---
title: 安装生物识别驱动程序
description: 安装生物识别驱动程序
keywords:
- 生物识别驱动程序 WDK，安装
- 安装生物识别驱动程序 WDK 生物识别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d848a1cdf2fe57ea0ca2828ce60505af7ae19131
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784285"
---
# <a name="installing-a-biometric-driver"></a>安装生物识别驱动程序


供应商可以提供一个 INF 文件来安装 WBDI 驱动程序。

下面是用于安装生物识别设备的准则列表。 本主题中的代码示例取自 [WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)的 WudfBioUsbSample 文件 inx 文件：

-   WBDI 驱动程序应指定类 "生物识别"。 设置 ClassGuid 等于 DEVCLASS \_ 中 GUID 生物识别的值 \_ ：

    ```cpp
    [Version]
    Signature="$Windows NT$"
    Class=Biometric
    ClassGuid={53D29EF7-377C-4D14-864B-EB3A85769359}
    ```

-   在中。HW 部分，提供 AddReg 指令来指定三个包含要添加到注册表中的项的部分：

    ```cpp
    [Biometric_Install.NT.hw]
    AddReg=Biometric_Device_AddReg
    AddReg=DriverPlugInAddReg, DatabaseAddReg
    ```

-   提供中提到的命名节。HW 部分。 \[生物识别 \_ 设备 \_ AddReg \] 部分设置生物识别设备的值，包括独占标志和系统唤醒/设备空闲。 若要通过 Windows Biometric Framework 识别，基于 UMDF 的 WBDI 驱动程序必须将 "独占" 值设置为1。 \[生物识别设备 AddReg 部分的前两行 \_ \_ \] (ACL) 权限指定访问控制列表，使设备只能由管理员或本地系统帐户打开。 当你指定这些 ACL 权限时，第三方应用程序无法在 WinBio 服务未运行时打开设备并捕获指纹数据。 例如：

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

    ) 生物识别堆栈 (公开功能的 WBDI 驱动程序将独占值设置为零。 如果此值设置为零，则 Windows Biometric Framework 不会尝试控制设备，并且不会通过 WBF 公开设备。

    供应商可以有单个驱动程序二进制文件，它可以处理旧式堆栈和 WBF，但这两者不能同时运行。 仅当可以使用独占访问权限打开设备时，WBF 才会运行。

-   第二个命名节包含插件适配器的注册表值。 该示例使用 Microsoft 提供的传感器适配器和存储适配器。 本部分还通过设置 SystemSensor 值来启用 Windows 登录支持：

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

-   最后，第三部分为数据库服务设置以下注册表值。 标识 GUID 对于特定格式的每个供应商数据库必须是唯一的。 例如，在此示例中，在此代码示例中，将6E9D4C5A-55B4-4c52-90B7-DDDC75CA4D50 更改为你在 INF 文件中的唯一 GUID。

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

-   为区分 WBDI 和旧驱动程序，供应商必须在 INX 文件中为驱动程序设置功能分数。 [WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)示例中未设置功能分数。 有关设置功能分数的详细信息，请参阅 [对 Windows 更新上的生物识别驱动程序进行排名](ranking-a-biometric-driver-on-windows-update.md)。

有关 INX 文件及其与 INF 文件的区别的信息，请参阅 [使用 INX 文件创建 Inf 文件](../wdf/using-inx-files-to-create-inf-files.md)。

若要将 WBDI 驱动程序替换为旧驱动程序，请使用以下过程：

1.  关闭所有当前处于活动状态的 WBF 应用程序。

2.  卸载 WBDI 驱动程序。

3.  停止 WBF 服务，重新启动它，然后再次将其停止。

4.  安装旧驱动程序。

 

