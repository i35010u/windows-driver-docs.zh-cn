---
title: 使用 Storport 驱动程序的函数角色类型来声明函数
description: 若要启用 SDV 分析 Storport 驱动程序，必须使用为 Storport 定义的函数角色类型声明中声明函数。 Storport.h 中定义的函数角色类型。
ms.assetid: 40BD11CD-A559-4F90-BF39-4ED2FB800392
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ad901f3f8148b928ac3e37eb12af7e07d7019c1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371421"
---
# <a name="declaring-functions-by-using-function-role-types-for-storport-drivers"></a>使用 Storport 驱动程序的函数角色类型来声明函数


若要启用 SDV 分析 Storport 驱动程序，必须使用为 Storport 定义的函数角色类型声明中声明函数。 Storport.h 中定义的函数角色类型。

您必须通过指定相应的角色类型声明 Storport 驱动程序中的每个回调函数。

下面的代码示例显示了 DriverIntialize 回调函数的函数角色类型声明。 函数角色类型为 sp\_驱动程序\_初始化。

```
sp_DRIVER_INITIALIZE DriverEntry;
```

如果回调函数有函数原型声明，必须将函数原型替换函数角色类型声明。

| 函数角色类型                        | Storport 例程                                                                                                               |
|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| sp\_驱动程序\_初始化                    | DriverEntry                                                                                                                    |
| HW\_初始化                            | [**HwStorInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_initialize)                                                                               |
| HW\_BUILDIO                               | [**HwStorBuildIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_buildio)                                                                                     |
| HW\_STARTIO                               | [**HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio)                                                                                     |
| HW\_中断                             | [**HwStorInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_interrupt)                                                                                 |
| HW\_计时器                                 | [**HwStorTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_timer)                                                                                         |
| HW\_查找\_适配器                         | [**HwStorFindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_find_adapter)                                                                             |
| HW\_重置\_总线                            | [**HwStorResetBus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_reset_bus)                                                                                   |
| HW\_适配器\_控件                      | [**HwStorAdapterControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_adapter_control)                                                                       |
| HW\_被动\_初始化\_例程          | [**HwStorPassiveInitializeRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_passive_initialize_routine)                                                   |
| HW\_DPC\_例程                          | [**HwStorDpcRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_dpc_routine)                                                                               |
| HW\_免费\_适配器\_资源              | HwFreeAdapterResources 一部分[**虚拟\_HW\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_virtual_hw_initialization_data)结构。  |
| HW\_PROCESS\_SERVICE\_REQUEST             | HwProcessServiceRequest 一部分[**虚拟\_HW\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_virtual_hw_initialization_data)结构。 |
| HW\_完成\_服务\_IRP                | HwCompleteServiceIrp 一部分[**虚拟\_HW\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_virtual_hw_initialization_data)结构。    |
| HW\_初始化\_跟踪                   | HwInitializeTracing 一部分[**虚拟\_HW\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_virtual_hw_initialization_data)结构。     |
| HW\_清理\_跟踪                      | HwCleanupTracing 一部分[**虚拟\_HW\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_virtual_hw_initialization_data)结构。        |
| 虚拟\_HW\_查找\_适配器                | HwFindAdapter 一部分[**虚拟\_HW\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_virtual_hw_initialization_data)结构。           |
| HW\_消息\_用信号通知\_中断\_例程 | [**HwMSInterruptRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_message_signaled_interrupt_routine)                                                                       |

 

 

 





