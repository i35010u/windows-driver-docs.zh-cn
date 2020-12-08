---
title: 访问传感器类扩展
description: 访问传感器类扩展
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: f13cb53a8ba6cfb8f3f8560c3bc54f43f9e52ab3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812389"
---
# <a name="access-the-sensor-class-extension"></a>访问传感器类扩展


| 模块     | 类/接口 |
|------------|-----------------|
| 设备 .cpp | CMyDevice       |

 

Microsoft 支持两个传感器 Api。 这两个简化访问设备、检索数据和设置属性：

-   适用于传统桌面应用的 **桌面 API** () -使用 COM/Win32;可在 c + + 中编写应用。
-   适用于 Windows 应用的 **WINRT API** () -在 HtML 和 JavaScript 中编写应用，或者在 XAML 和 Visual Basic、c # 或 c + + 中编写应用。

传感器类扩展 (**ISensorClassExtension**) 链接传感器驱动程序和传感器 api。 驱动程序使用它来完成以下操作：

-   初始化并 unitialize 传感器类扩展
-   引发事件
-   处理 WPD 输入/输出控制代码 (IOCTLs) 
-   关闭 UMDF 文件句柄

## <a name="initializing-the-class-extension"></a>初始化类扩展

当 (Windows 用户模式驱动程序框架) 调用 **CMyDevice：： OnPrepareHardware** 的组件 WUDFx.dll 时，SpbAccelerometer 示例将初始化类扩展：

```cpp
if (SUCCEEDED(hr))
{
    // Initialize the sensor class extension
    hr = m_spClassExtension->Initialize(pWdfDevice, spUnknown);
}
```

### <a name="releasing-the-class-extension"></a>释放类扩展

调用 CMyDevice：： OnReleaseHardware 时，示例驱动程序会取消初始化并释放类扩展：

```cpp
if (m_spClassExtension != nullptr)
{
   hr = m_spClassExtension->Uninitialize();
}
```

### <a name="supporting-data-events-with-the-class-extension"></a>通过类扩展支持数据事件

当传感器应用为数据事件注册事件处理程序时，示例驱动程序将使用 **ISensorClassExtension：:P ostevent** 发送事件通知。 这会在 **CSensorDdi 中发生：:P ostdataevent**：

```cpp
if (SUCCEEDED(hr))
{
   hr = m_spClassExtension->PostEvent(SensorId, spCollection);
}
```

### <a name="supporting-state-change-events-with-the-class-extension"></a>支持具有类扩展的状态更改事件

当传感器应用为状态更改事件注册事件处理程序时，示例驱动程序将使用 **ISensorClassExtension：:P oststatechange** 发布事件通知。 这会在 **CSensorDdi 中发生：:P oststatechange**：

```cpp
HRESULT hr = m_spClassExtension->PostStateChange(SensorId, state);
```

 

 




