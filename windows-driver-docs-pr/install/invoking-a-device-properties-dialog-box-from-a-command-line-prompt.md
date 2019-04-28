---
title: 调用命令行提示符下从设备属性对话框
description: 从命令行提示符调用设备属性对话框
ms.assetid: 616c93ee-8360-4bab-8e08-48a55cd617f1
keywords:
- 设备属性对话框框 WDK 设备安装
- 调用设备属性对话框
- DeviceProperties_RunDLL WDK 设备安装
- 机名称参数字段 WDK 设备安装
- 设备实例 ID 参数字段 WDK 设备独占指令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00964b69e87ff3846041d34e7d3e6629eb47446e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346120"
---
# <a name="invoking-a-device-properties-dialog-box-from-a-command-line-prompt"></a>从命令行提示符调用设备属性对话框


[DeviceProperties_RunDLL](deviceproperties-rundll-function-prototype.md)函数在设备管理器可以从命令行提示使用调用*rundll32.exe*。 下面的代码示例演示了调用的格式**DeviceProperties_RunDLL**从命令提示符。

```cpp
rundll32.exe devmgr.dll, DeviceProperties_RunDLL machine-name-parameter device-instance-ID-parameter
```

格式和要求*机名称参数*字段是针对提供的命令行字符串所述的相同*lpCmdLine*参数的**DeviceProperties_RunDLL**。 格式和要求*设备实例 ID 参数*字段也是与所述的相同*lpCmdLine*命令行字符串，受以下附加要求的约束：如果*设备实例 ID*子字段包含一个 & 号 (&)、*设备实例 ID*子字段必须用引号 （"）。

以下代码示例演示的格式和提供的要求*机名称参数*并*设备实例 ID 参数*调用**DeviceProperties_RunDLL**从命令行提示符。 这些示例对应于中提供的示例[设备属性对话框框中以编程方式安装应用程序中调用](invoking-a-device-properties-dialog-box-programmatically-in-an-install.md)。

-   (Windows XP 及更高版本)一个可选*机名称参数*字段未提供，其中指出，默认情况下，计算机是本地计算机。 所需*设备实例 ID 参数*字段提供[设备实例标识符](device-instance-ids.md)"根\\系统\\0000"。
    ```cpp
    rundll32.exe devmgr.dll,DeviceProperties_RunDLL /DeviceID root\system\0000
    ```

-   (Windows XP 及更高版本)一个可选*机名称参数*字段未提供，其中指出，默认情况下，计算机是本地计算机。 所需*设备实例 ID 参数*字段提供的设备实例标识符"PCI\\VEN_8086 DEV_2445 SUBSYS_010E1028 & REV_12\\3 172E68DD 0 & FD"。 因为设备实例标识符包含一个 & 号 (&)、*设备实例 ID*子字段括在引号 （"）。
    ```cpp
    rundll32.exe devmgr.dll,DeviceProperties_RunDLL /DeviceID "PCI\VEN_8086&DEV_2445&SUBSYS_010E1028&REV_12\3&172E68DD&0&FD" 
    ```

-   (Windows 2000 及更高版本)所需*机名称参数*字段提供了一对引号 ("") 作为*计算机名称*，指示计算机是本地计算机。 所需*设备实例 ID 参数*字段提供的设备实例标识符"根\\系统\\0000"。
    ```cpp
    rundll32.exe devmgr.dll,DeviceProperties_RunDLL /MachineName "" /DeviceID root\system\0000
    ```

-   (Windows 2000 及更高版本)所需*机名称参数*字段提供的远程计算机名称"\\\\RemoteMachineAbc"。 所需*设备实例 ID 参数*字段提供的设备实例标识符"根\\系统\\0000"。
    ```cpp
    rundll32.exe devmgr.dll,DeviceProperties_RunDLL /MachineName \\RemoteMachineAbc /DeviceID root\system\0000
    ```

 

 





