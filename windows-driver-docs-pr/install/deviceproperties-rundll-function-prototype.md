---
title: DeviceProperties_RunDLL 函数原型
description: DeviceProperties_RunDLL 函数原型
keywords:
- "\"设备属性\" 对话框 WDK 设备安装"
- "\"调用设备属性\" 对话框"
- DeviceProperties_RunDLL WDK 设备安装
- 计算机名称-参数字段 WDK 设备安装
- 设备实例 ID-参数字段 WDK 设备指令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7690224cf5e5198118d1242a7f0ff89be4ab2b33
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782829"
---
# <a name="deviceproperties_rundll-function-prototype"></a>DeviceProperties_RunDLL 函数原型


DeviceProperties_RunDLL 函数将打开安装在本地或远程计算机上的指定设备的 "设备属性" 对话框。

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
用于显示 DeviceProperties_RunDLL 创建的用户界面项的窗口的句柄。

<a href="" id="happinstance"></a>*hAppInstance*  
此参数不用于调用设备属性对话框并且应设置为 **NULL**。

<a href="" id="lpcmdline"></a>*lpCmdLine*  
指向常量以 NULL 结尾的字符串的指针，该字符串包含一个 *计算机名称参数* 字段，后跟一个 *设备实例 ID-参数* 字段，格式如下：

*计算机名称参数设备实例 ID-参数*

<a href="" id="machine-name-parameter"></a>*计算机名称参数*  
*计算机名称参数* 字段提供与 *设备实例 ID-参数* 字段指定的设备相关联的计算机的名称。 *计算机名称参数* 字段的格式为 **/MachineName**  ****  *machine-name*，其中 **/MachineName** 指示 *计算机* 名称提供计算机名。 有关 *计算机名称参数* 字段的详细信息，请参阅 "备注" 部分。

<a href="" id="device-instance-id-parameter"></a>*设备实例 ID-参数*  
*设备实例 ID 参数* 字段提供要显示其 "设备属性" 对话框的设备的 [设备实例标识符](device-instance-ids.md)。 *设备实例 id 参数* 字段的格式为 **/DeviceId**  ****  *device-instance-ID*，其中 **/DeviceId** 表示 *设备实例 id* 提供了一个设备实例标识符。 需要 *设备实例 ID 参数* 字段。

<a href="" id="ncmdshow"></a>*nCmdShow*  
此参数不用于调用设备属性对话框并且应设置为 **NULL**。

### <a name="return-value"></a>返回值

无

### <a name="headers"></a>标头

DeviceProperties_RunDLL 未在公共标头中声明，只能通过编程方式获取指向函数的指针或使用 rundll32.exe 来间接调用。

### <a name="remarks"></a><a href="" id="comments"></a>注释

在 Windows XP 上， *计算机名称参数* 字段仅对远程计算机是必需的，并且，如果未提供 *计算机名称参数* 字段，则默认情况下使用本地计算机。 在 Windows 2000 上， *计算机名称参数* 字段是本地计算机或远程计算机必需的。 若要指定本地计算机，请将计算机 *名称参数* 字段中的 *计算机名称* 设置为一对引号 ( "" ) 。 如果该计算机是远程计算机，请将 *计算机名称* 设置为有效的计算机名称。 有效的计算机名称必须包含一个前缀，该前缀包含一对反斜杠 (\\ \) 后跟计算机名。

下面是命令行字符串的示例：

-    (Windows XP 和更高版本) 指定本地计算机是可选的，在这种情况下，命令行字符串只需包含设备实例标识符。 例如，以下命令行默认指定本地计算机和设备实例标识符 "root \\ 系统 \\ 0000"。
    ```cpp
    /DeviceId root\system\0000
    ```

-    (Windows 2000 及更高版本) 下面的命令行字符串提供远程计算机名称 " \\ \\ RemoteMachineAbc" 和设备实例标识符 "root \\ 系统 \\ 0000"。
    ```cpp
    /MachineName \\RemoteMachineAbc /DeviceId root\system\0000
    ```

-    (Windows 2000 及更高版本) 下面的命令行字符串指定一个本地计算机，该计算机由一对引号 ( "" ) 指定，并提供设备实例标识符 "root \\ system \\ 0000"。
    ```cpp
    /MachineName "" /DeviceId root\system\0000
    ```

 

 





