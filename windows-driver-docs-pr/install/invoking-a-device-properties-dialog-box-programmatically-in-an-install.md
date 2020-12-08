---
title: 安装应用程序中的 "调用设备属性" 对话框
description: 在安装应用程序中以编程方式调用设备属性对话框
keywords:
- "\"设备属性\" 对话框 WDK 设备安装"
- "\"调用设备属性\" 对话框"
- DeviceProperties_RunDLL WDK 设备安装
- 以编程方式调用 "设备属性" 对话框 WDK
- pDeviceProperties 函数指针 WDK
- 机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64c94b1d74e94a0f22f637c2ea2b19a6f0e73afe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841063"
---
# <a name="invoking-a-device-properties-dialog-box-programmatically-in-an-installation-application"></a>在安装应用程序中以编程方式调用设备属性对话框


若要在安装应用程序中以编程方式调用 "设备属性" 对话框，应用程序代码应执行以下操作：

-   在应用程序代码中包含宏定义和类型定义，以确保在生成应用程序时链接 [DeviceProperties_RunDLL](deviceproperties-rundll-function-prototype.md) 的适当版本。 Windows 支持 Unicode 版本和 ASCII 版本。

-   加载 *devmgr.dll*。

-   获取指向 **DeviceProperties_RunDLL** 函数的指针。

-   调用 **DeviceProperties_RunDLL**，并提供适当的参数。

下面的代码示例演示如何定义引用 **DeviceProperties_RunDLL** 函数的 *pDeviceProperties* 函数指针。 如果在代码编译时定义了 _UNICODE 宏，则 *pDeviceProperties* 是指向函数的 UNICODE 版本的指针;否则， *pDeviceProperties* 是指向 ASCII 版本函数的指针。

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

下面的代码示例使用在前面的代码示例中提供的 *pDeviceProperties* 的定义，并演示如何以编程方式加载 *devmgr.dll* 以及如何获取指向适当版本的 **DeviceProperties_RunDLL** 的函数指针。

```cpp
HINSTANCE  hDevMgr = LoadLibrary(_TEXT("devmgr.dll"));
 if (hDevMgr) {
 pDeviceProperties = (PDEVICEPROPERTIES)GetProcAddress((HMODULE)hDevMgr, DeviceProperties_RunDLL);
}
```

获取 *pDeviceProperties* 函数指针之后，必须在对 **DeviceProperties_RunDLL** 的调用中提供计算机名称和 [设备实例标识符](device-instance-ids.md)。 下面的代码示例演示了这些项的相应格式和要求：

-    (Windows XP 和更高版本) 不提供可选的 *计算机名称参数* 字段，这表示默认情况下该计算机是本地计算机。 必需的 *设备实例 ID 参数* 字段提供设备实例标识符 "root \\ 系统 \\ 0000"。
    ```cpp
    if (pDeviceProperties){
     pDeviceProperties(m_hWnd, NULL, _TEXT("/DeviceID root\\system\\0000"), NULL);
    };
    ```

-    (Windows XP 和更高版本) 不提供可选的 *计算机名称参数* 字段，这表示默认情况下该计算机是本地计算机。 必需的 *设备实例 ID 参数* 字段提供设备实例标识符 "PCI \\ VEN_8086&DEV_2445 &SUBSYS_010E1028&REV_12&\\ 172E68DD&0&FD"。
    ```cpp
    if (pDeviceProperties){
     pDeviceProperties(m_hWnd, NULL, _TEXT("/DeviceID PCI\\VEN_8086\&DEV_2445\&SUBSYS_010E1028\&REV_12\\3\&172E68DD\&0\&FD"), NULL);
    };
    ```

-    (Windows 2000 及更高版本) 所需的 *计算机名称参数* 字段提供一对双引号 ( "" ) 对于 *计算机名称*，这表示计算机是本地计算机。 必需的 *设备实例 ID 参数* 字段提供设备实例标识符 "root \\ 系统 \\ 0000"。
    ```cpp
    if (pDeviceProperties){
     pDeviceProperties(m_hWnd, NULL, _TEXT("/MachineName \"\" /DeviceID root\\system\\0000"), NULL);
    };
    ```

-    (Windows 2000 和更高版本中) 所需的 *计算机名称参数* 字段提供远程计算机名称 " \\ \\ RemoteMachineAbc"，并且所需的 *设备实例 ID 参数* 字段提供设备实例标识符 "root \\ 系统 \\ 0000"。
    ```cpp
    if (pDeviceProperties){
     pDeviceProperties(m_hWnd, NULL, _TEXT("/MachineName \\\\RemoteMachineAbc /DeviceID root\\system\\0000"), NULL);
    };
    ```

 

 





