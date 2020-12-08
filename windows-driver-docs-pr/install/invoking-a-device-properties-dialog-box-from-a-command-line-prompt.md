---
title: 通过命令行提示符调用 "设备属性" 对话框
description: 从命令行提示符调用设备属性对话框
keywords:
- "\"设备属性\" 对话框 WDK 设备安装"
- "\"调用设备属性\" 对话框"
- DeviceProperties_RunDLL WDK 设备安装
- 计算机名称-参数字段 WDK 设备安装
- 设备实例 ID-参数字段 WDK 设备指令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 681be2df1f21c133f0d2a2cd49444bea1e6d004c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841233"
---
# <a name="invoking-a-device-properties-dialog-box-from-a-command-line-prompt"></a>从命令行提示符调用设备属性对话框


使用 *rundll32.exe*，可以从命令行提示符调用设备管理器中的 [DeviceProperties_RunDLL](deviceproperties-rundll-function-prototype.md)函数。 下面的代码示例演示从命令提示符调用 **DeviceProperties_RunDLL** 的格式。

```cpp
rundll32.exe devmgr.dll, DeviceProperties_RunDLL machine-name-parameter device-instance-ID-parameter
```

*计算机名称参数* 字段的格式和要求与 **DeviceProperties_RunDLL** 的 *lpCmdLine* 参数提供的命令行字符串的格式和要求相同。 *设备实例 id 参数* 字段的格式和要求也与 *lpCmdLine* 命令行字符串所述的格式和要求相同，但有以下附加要求：如果 *设备实例 id* 子字段包含与号 ( # A0) ，则必须用引号将 *设备实例 id* 子字段括起来 ( ") 。

下面的代码示例说明了提供 *计算机名称参数* 和 *设备实例 ID 参数* 以从命令行提示符调用 **DeviceProperties_RunDLL** 的格式和要求。 这些示例对应于在 [安装应用程序中以编程方式调用设备属性对话框](invoking-a-device-properties-dialog-box-programmatically-in-an-install.md)中提供的示例。

-    (Windows XP 和更高版本) 不提供可选的 *计算机名称参数* 字段，这表示默认情况下该计算机是本地计算机。 必需的 *设备实例 ID 参数* 字段提供 [设备实例标识符](device-instance-ids.md) "root \\ 系统 \\ 0000"。
    ```cpp
    rundll32.exe devmgr.dll,DeviceProperties_RunDLL /DeviceID root\system\0000
    ```

-    (Windows XP 和更高版本) 不提供可选的 *计算机名称参数* 字段，这表示默认情况下该计算机是本地计算机。 必需的 *设备实例 ID 参数* 字段提供设备实例标识符 "PCI \\ VEN_8086&DEV_2445 &SUBSYS_010E1028&REV_12&\\ 172E68DD&0&FD"。 因为设备实例标识符包含与号 ( # A0) ，所以， *设备实例 ID* 子字段用引号括起来 ( ") 。
    ```cpp
    rundll32.exe devmgr.dll,DeviceProperties_RunDLL /DeviceID "PCI\VEN_8086&DEV_2445&SUBSYS_010E1028&REV_12\3&172E68DD&0&FD" 
    ```

-    (Windows 2000 及更高版本) 所需的 *计算机名称参数* 字段提供一对引号 ( "" ) 作为 *计算机名*，这表示计算机是本地计算机。 必需的 *设备实例 ID 参数* 字段提供设备实例标识符 "root \\ 系统 \\ 0000"。
    ```cpp
    rundll32.exe devmgr.dll,DeviceProperties_RunDLL /MachineName "" /DeviceID root\system\0000
    ```

-    (Windows 2000 及更高版本) 所需的 *计算机名称参数* 字段提供远程计算机名称 " \\ \\ RemoteMachineAbc"。 必需的 *设备实例 ID 参数* 字段提供设备实例标识符 "root \\ 系统 \\ 0000"。
    ```cpp
    rundll32.exe devmgr.dll,DeviceProperties_RunDLL /MachineName \\RemoteMachineAbc /DeviceID root\system\0000
    ```

 

 





