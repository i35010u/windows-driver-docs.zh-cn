---
title: 自定义控制代码
description: 供应商可以定义自定义控件代码
ms.assetid: 66eebb4b-ee1e-42d2-9a4b-98a79a0f7b75
keywords:
- 生物识别驱动程序 WDK，控制代码
ms.date: 11/13/2017
ms.localizationpriority: medium
ms.openlocfilehash: 969f55aecbbcc2147da842b029f53e13591c4293
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563347"
---
# <a name="custom-control-codes"></a>自定义控制代码

供应商可以定义自定义控件代码开始 0x800。

若要定义特定于供应商的 I/O 控制代码，请使用以下参数使用系统提供 CTL_CODE 宏：

```c
#define IOCTL_BIOMETRIC_Device_Function CTL_CODE(FILE_DEVICE_BIOMETRIC, Function, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

所有输入/输出参数都是供应商定义的。 **状态**成员设置为下表中的值之一：

| 状态值 | 描述 |
| --- | --- |
| STATUS_SUCCESS，则为 S_OK， | 已成功完成该操作。 如果返回的数据大小是 DWORD，负载将包含调用所需的缓冲区的大小。 否则，有效负载包含完整输出缓冲区。 |
| E_INVALIDARG | 参数未正确指定。 |

供应商定义 Ioctl 可以用于任何特定于供应商的操作。 通过 Windows 生物识别服务，提供对设备的排他控制用于显示这些调用。 下面是一些示例的供应商可以如何使用供应商特定 Ioctl:

- 设置应用程序或组件和设备之间的专有安全会话。
- 使用从 WinBio 引擎或插件的数据库在设备上的匹配和存储功能的接口。
- 特定于供应商的设备事件的挂起 I/O。
- 管理特定于供应商的会话。

此功能是在 Windows 7 和更高版本的 Windows 中可用。


