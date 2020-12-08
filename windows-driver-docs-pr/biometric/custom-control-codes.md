---
title: 自定义控制代码
description: 供应商可以定义自定义控制代码
keywords:
- 生物识别驱动程序 WDK，控制代码
ms.date: 11/13/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f2d3a243d2df63d88542f77599d51c7b15a4789
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798629"
---
# <a name="custom-control-codes"></a>自定义控制代码

供应商可以从0x800 开始定义自定义控制代码。

若要定义供应商特定的 i/o 控制代码，请将系统提供的 CTL_CODE 宏用于以下参数：

```c
#define IOCTL_BIOMETRIC_Device_Function CTL_CODE(FILE_DEVICE_BIOMETRIC, Function, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

所有输入/输出参数均由供应商定义。 **Status** 成员设置为下表中的值之一：

| 状态值 | 说明 |
| --- | --- |
| S_OK，STATUS_SUCCESS | 操作已成功完成。 如果返回的数据的大小为 DWORD，则负载包含调用所需的缓冲区大小。 否则，负载包含完整的输出缓冲区。 |
| E_INVALIDARG | 未正确指定参数。 |

供应商定义的 IOCTLs 可用于任何供应商特定的操作。 这些调用都通过 Windows 生物识别服务，该服务具有设备的独占控制权。 下面是一些供应商如何使用特定于供应商的 IOCTLs 的示例：

- 在应用程序或组件与设备之间设置专用的安全会话。
- 在设备上通过 WinBio 引擎或数据库插件提供匹配和存储功能的接口。
- 针对供应商特定设备事件挂起的 i/o。
- 管理供应商特定的会话。

此功能在 windows 7 和更高版本的 Windows 中可用。


