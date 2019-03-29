---
title: 访问传感器类扩展
description: 访问传感器类扩展
ms.assetid: 206A00AE-45D7-49D8-97E2-45A6DACFCB08
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0b1325be764d4272929c2802a6a705b45921d3b8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575558"
---
# <a name="access-the-sensor-class-extension"></a>访问传感器类扩展


| 模块     | 类/接口 |
|------------|-----------------|
| Device.cpp | CMyDevice       |

 

Microsoft 支持两个传感器 Api。 同时简化访问设备，检索数据，并设置属性：

-   **桌面 API** （适用于传统的桌面应用）-使用 COM/Win32; 在 c + + 编写应用程序。
-   **WinRT API**在 HtML 和 JavaScript，或者，XAML 和 Visual Basic 中 （适用于 Windows 应用）-编写应用程序C#或 c + +。

传感器类扩展 (**ISensorClassExtension**) 链接传感器驱动程序和传感器 Api。 您的驱动程序使用它来完成以下：

-   初始化和 unitialize 传感器类扩展
-   引发事件
-   进程 WPD 输入/输出控制代码 (Ioctl)
-   关闭 UMDF 文件句柄

## <a name="initializing-the-class-extension"></a>初始化类扩展

SpbAccelerometer 示例 WUDFx.dll （Windows 用户模式驱动程序框架的组件） 调用时初始化类扩展**CMyDevice::OnPrepareHardware**:

```cpp
if (SUCCEEDED(hr))
{
    // Initialize the sensor class extension
    hr = m_spClassExtension->Initialize(pWdfDevice, spUnknown);
}
```

### <a name="releasing-the-class-extension"></a>释放此类扩展

示例驱动程序不初始化，并在调用 CMyDevice::OnReleaseHardware 发布此类扩展：

```cpp
if (m_spClassExtension != nullptr)
{
   hr = m_spClassExtension->Uninitialize();
}
```

### <a name="supporting-data-events-with-the-class-extension"></a>支持此类扩展的数据事件

当传感器应用程序注册的数据事件的事件处理程序时，示例驱动程序将发布使用的事件通知**ISensorClassExtension::PostEvent**。 中将发生这种情况**CSensorDdi::PostDataEvent**:

```cpp
if (SUCCEEDED(hr))
{
   hr = m_spClassExtension->PostEvent(SensorId, spCollection);
}
```

### <a name="supporting-state-change-events-with-the-class-extension"></a>支持使用此类扩展的状态更改事件

当传感器应用程序注册状态更改事件的事件处理程序时，示例驱动程序将发布使用的事件通知**ISensorClassExtension::PostStateChange**。 中将发生这种情况**CSensorDdi::PostStateChange**:

```cpp
HRESULT hr = m_spClassExtension->PostStateChange(SensorId, state);
```

 

 




