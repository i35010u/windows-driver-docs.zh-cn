---
title: 调用安装应用程序中的设备属性对话框
description: 在安装应用程序中以编程方式调用设备属性对话框
ms.assetid: c573acac-581e-44f1-b46b-eceb1f3d5484
keywords:
- 设备属性对话框框 WDK 设备安装
- 调用设备属性对话框
- DeviceProperties_RunDLL WDK 设备安装
- 以编程方式调用设备属性对话框 WDK
- pDeviceProperties 函数指针 WDK
- 机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3b92d4c9f74caf5b02dee1a54ae40cfe8be305f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576452"
---
# <a name="invoking-a-device-properties-dialog-box-programmatically-in-an-installation-application"></a>在安装应用程序中以编程方式调用设备属性对话框


若要调用以编程方式安装应用程序中的设备属性对话框，应用程序代码应执行以下操作：

-   包含宏的定义和类型，请确保适当版本的应用程序代码中定义[DeviceProperties_RunDLL](deviceproperties-rundll-function-prototype.md)时生成应用程序链接。 Windows 支持的 Unicode 版本和 ASCII 版本。

-   负载*devmgr.dll*。

-   获取一个指向**DeviceProperties_RunDLL**函数。

-   调用**DeviceProperties_RunDLL**，提供适当的参数。

下面的代码示例演示如何定义*pDeviceProperties*引用的函数指针**DeviceProperties_RunDLL**函数。 如果编译代码，定义了 _UNICODE 宏*pDeviceProperties*是指向 Unicode 版本的函数中; 否则为*pDeviceProperties*是指向的 ASCII 版本函数。

```cpp
#ifdef _UNICODE 
  #define DeviceProperties_RunDLL  "DeviceProperties_RunDLLW"
 typedef void (_stdcall *PDEVICEPROPERTIES)(
    HWND hwndStub,
    HINSTANCE hAppInstance,
    LPWSTR lpCmdLine,
 int nCmdShow
   ;
#else
  #define DeviceProperties_RunDLL  "DeviceProperties_RunDLLA"
 typedef void (_stdcall *PDEVICEPROPERTIES)(
    HWND hwndStub,
    HHINSTANCE hAppInstance,
    LPSTR lpCmdLine,
 int nCmdShow
  );
#endif

PDEVICEPROPERTIES pDeviceProperties;
```

下面的代码示例使用的定义*pDeviceProperties* ，在前面的代码示例中提供和显示如何加载*devmgr.dll*以编程方式以及如何获取该函数指向适当版本的指针**DeviceProperties_RunDLL**。

```cpp
HINSTANCE  hDevMgr = LoadLibrary(_TEXT("devmgr.dll"));
 if (hDevMgr) {
 pDeviceProperties = (PDEVICEPROPERTIES)GetProcAddress((HMODULE)hDevMgr, DeviceProperties_RunDLL);
}
```

获取后*pDeviceProperties*函数指针，则必须提供计算机名称和[设备实例标识符](device-instance-ids.md)对的调用中**DeviceProperties_RunDLL**。 下面的代码示例说明了相应的格式和这些项要求：

-   (Windows XP 及更高版本)一个可选*机名称参数*字段未提供，其中指出，默认情况下，计算机是本地计算机。 所需*设备实例 ID 参数*字段提供的设备实例标识符"根\\系统\\0000"。
    ```cpp
    if (pDeviceProperties){
     pDeviceProperties(m_hWnd, NULL, _TEXT("/DeviceID root\\system\\0000"), NULL);
    };
    ```

-   (Windows XP 及更高版本)一个可选*机名称参数*字段未提供，其中指出，默认情况下，计算机是本地计算机。 所需*设备实例 ID 参数*字段提供的设备实例标识符"PCI\\VEN_8086 DEV_2445 SUBSYS_010E1028 & REV_12\\3 172E68DD 0 & FD"。
    ```cpp
    if (pDeviceProperties){
     pDeviceProperties(m_hWnd, NULL, _TEXT("/DeviceID PCI\\VEN_8086\&DEV_2445\&SUBSYS_010E1028\&REV_12\\3\&172E68DD\&0\&FD"), NULL);
    };
    ```

-   (Windows 2000 及更高版本)所需*机名称参数*字段提供了一对双引号 ("") 用于*计算机名称*，指示计算机是本地计算机。 所需*设备实例 ID 参数*字段提供的设备实例标识符"根\\系统\\0000"。
    ```cpp
    if (pDeviceProperties){
     pDeviceProperties(m_hWnd, NULL, _TEXT("/MachineName \"\" /DeviceID root\\system\\0000"), NULL);
    };
    ```

-   (Windows 2000 及更高版本)所需*机名称参数*字段提供的远程计算机名称"\\\\RemoteMachineAbc"和所需*设备实例 ID 参数*字段提供设备实例标识符"根\\系统\\0000"。
    ```cpp
    if (pDeviceProperties){
     pDeviceProperties(m_hWnd, NULL, _TEXT("/MachineName \\\\RemoteMachineAbc /DeviceID root\\system\\0000"), NULL);
    };
    ```

 

 





