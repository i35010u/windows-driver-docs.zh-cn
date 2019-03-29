---
title: 驱动程序的 DO_DEVICE_INITIALIZING 注释
description: 用于指定是否应清除标志字段中的设备对象的 DO_DEVICE_INITIALIZING 位批注的函数。
ms.assetid: EFC5F0A3-7B20-49A5-9D50-1737DF76DC9E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca73e667c23f41ee2d7f89b9d651514b861e142c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567170"
---
# <a name="dodeviceinitializing-annotation-for-drivers"></a>不要\_设备\_驱动程序的初始化批注


使用\_内核\_清除\_做\_init\_批注指定带批注的函数是否应清除执行\_设备\_中的正在初始化位标记的设备对象的字段。

此批注的语法如下：

```
_Kernel_clear_do_init_(yes|no)
```

调用函数的使用进行批注\_内核\_清除\_做\_init\_(yes) 免除对调用函数无需清除执行\_设备\_正在初始化位。

批注几乎始终应在条件的上下文中时该函数将返回成功，除非批注应用于函数类型定义。 例如，在驱动程序的以下函数类型定义\_添加\_设备函数类批注指定函数不能提升 IRQL 和该函数会清除执行\_设备\_正在初始化位。

```
typedef
_IRQL_always_function_max_(PASSIVE_LEVEL)
_IRQL_requires_same_
_Kernel_clear_do_init_(yes)
__drv_functionClass(DRIVER_ADD_DEVICE)
NTSTATUS
DRIVER_ADD_DEVICE (
    _In_ struct _DRIVER_OBJECT *DriverObject,
    _In_ struct _DEVICE_OBJECT *PhysicalDeviceObject
    );
typedef DRIVER_ADD_DEVICE *PDRIVER_ADD_DEVICE;
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[Windows 驱动程序的 SAL 2.0 注释](sal-2-annotations-for-windows-drivers.md)










