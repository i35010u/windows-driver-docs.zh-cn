---
title: DeviceProperties_RunDLL 函数原型
description: DeviceProperties_RunDLL 函数原型
ms.assetid: 15c93f6d-56e7-4872-a94b-0c948e2cd76f
keywords:
- 设备属性对话框框 WDK 设备安装
- 调用设备属性对话框
- DeviceProperties_RunDLL WDK 设备安装
- 机名称参数字段 WDK 设备安装
- 设备实例 ID 参数字段 WDK 设备独占指令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c761d8a554267920e29c8f53647ff0637d85dee1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523889"
---
# <a name="devicepropertiesrundll-function-prototype"></a>DeviceProperties_RunDLL 函数原型


DeviceProperties_RunDLL 函数将打开指定设备安装在本地或远程计算机上的设备属性对话框。

```cpp
void DeviceProperties_RunDLL(
  HWND       hwndStub,
  HINSTANCE  hAppInstance,
  LPCTSTR    lpCmdLine,
  int        nCmdShow
  );
```

### <a name="parameters"></a>参数

<a href="" id="hwndstub"></a>*hwndStub*  
创建要在其中显示用户界面项目该 DeviceProperties_RunDLL 窗口的句柄。

<a href="" id="happinstance"></a>*hAppInstance*  
此参数不用于调用设备属性对话框，应设置为**NULL**。

<a href="" id="lpcmdline"></a>*lpCmdLine*  
指向以 NULL 结尾的命令行字符串，其中包含的常量*机名称参数*字段跟*设备实例 ID 参数*字段采用以下格式：

*机名称参数设备-实例的 ID 的参数*

<a href="" id="machine-name-parameter"></a>*machine-name-parameter*  
*机名称参数*字段提供与由指定设备相关联的计算机的名称*设备实例 ID 参数*字段。 格式*机名称参数*字段是 **/MachineName** **** *计算机名称*，其中 **/MachineName**指示*计算机名称*提供计算机名称。 有关详细信息*机名称参数*字段中，请参阅备注部分。

<a href="" id="device-instance-id-parameter"></a>*device-instance-ID-parameter*  
*设备实例 ID 参数*字段提供[设备实例标识符](device-instance-ids.md)要为其显示设备属性对话框的设备。 格式*设备实例 ID 参数*字段是 **/DeviceId** **** *设备实例 ID*，其中 **/DeviceId**指示*设备实例 ID*提供设备实例标识符。 *设备实例 ID 参数*字段为必填项。

<a href="" id="ncmdshow"></a>*nCmdShow*  
此参数不用于调用设备属性对话框，应设置为**NULL**。

### <a name="return-value"></a>返回值

无

### <a name="headers"></a>标头

DeviceProperties_RunDLL 未在公共标头中声明，可以仅在调用间接通过 rundll32 或通过以编程方式获取指向函数的指针。

### <a href="" id="comments"></a>备注

在 Windows XP 中，*机名称参数*字段是必填只为远程计算机，并且如果*机名称参数*字段未提供，默认情况下使用本地计算机。 在 Windows 2000*机名称参数*字段是本地计算机或远程计算机所必需的。 若要指定本地计算机，请设置*计算机名*中*机名称参数*字段对一对引号 ("")。 如果计算机是远程计算机，设置*计算机名称*为有效的计算机名称。 有效的计算机名必须包含前缀的包含对反斜杠 (\\ \)跟计算机名称。

命令行字符串的示例如下：

-   (Windows XP 及更高版本)指定本地计算机是可选的这种情况下，命令行字符串需要包含设备实例标识符。 例如，以下命令行指定默认情况下和设备实例标识符的本地计算机"根\\系统\\0000"。
    ```cpp
    /DeviceId root\system\0000
    ```

-   (Windows 2000 及更高版本)下面的命令行字符串提供的远程计算机名称"\\\\RemoteMachineAbc"和设备实例标识符"根\\系统\\0000"。
    ```cpp
    /MachineName \\RemoteMachineAbc /DeviceId root\system\0000
    ```

-   (Windows 2000 及更高版本)下面的命令行字符串指定的本地计算机，指定由一对引号 ("")，并提供设备实例标识符"根\\系统\\0000"。
    ```cpp
    /MachineName "" /DeviceId root\system\0000
    ```

 

 





