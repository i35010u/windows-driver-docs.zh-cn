---
title: 驱动程序的 DO_DEVICE_INITIALIZING 注释
description: 用于指定是否应将带批注的函数清除设备对象的 "标志" 字段中的 DO_DEVICE_INITIALIZING 位。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72b624ffaf4dff2b4a8ae10027d7dd97356d3ba3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839013"
---
# <a name="do_device_initializing-annotation-for-drivers"></a>\_ \_ 为驱动程序初始化设备批注


使用 \_ 内核 \_ 明文 \_ do \_ init \_ 批注指定是否应在 \_ \_ 设备对象的 "标志" 字段中清除 "执行设备初始化" 位。

此批注具有以下语法：

```
_Kernel_clear_do_init_(yes|no)
```

调用使用 \_ 内核 \_ 清除 \_ do init 进行批注的函数 \_ \_ (是) 豁免调用函数不必清除 "执行 \_ 设备初始化" \_ 位。

当函数返回 success 时，注释应始终始终用在条件上下文中，除非将批注应用于函数类型定义。 例如，在以下用于驱动程序的函数类型定义中 \_ 添加 \_ 设备函数类，批注指定该函数不能引发 IRQL，并且函数应清除 "执行 \_ 设备 \_ 初始化" 位。

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

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[Windows 驱动程序的 SAL 2.0 注释](sal-2-annotations-for-windows-drivers.md)










