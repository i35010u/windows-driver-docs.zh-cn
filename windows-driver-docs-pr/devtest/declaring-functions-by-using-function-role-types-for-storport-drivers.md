---
title: 使用 Storport 驱动程序的函数角色类型来声明函数
description: 若要使 SDV 能够分析 Storport 驱动程序，必须使用为 Storport 定义的函数角色类型声明来声明函数。 函数角色类型在 Storport. h 中定义。
ms.assetid: 40BD11CD-A559-4F90-BF39-4ED2FB800392
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de028e62d53936f924cf7a55366cfc7f4e925291
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840288"
---
# <a name="declaring-functions-by-using-function-role-types-for-storport-drivers"></a>使用 Storport 驱动程序的函数角色类型来声明函数


若要使 SDV 能够分析 Storport 驱动程序，必须使用为 Storport 定义的函数角色类型声明来声明函数。 函数角色类型在 Storport. h 中定义。

必须通过指定相应的角色类型，在 Storport 驱动程序中声明每个回调函数。

下面的代码示例演示了 DriverIntialize 回调函数的函数角色类型声明。 函数角色类型为 sp\_驱动程序\_INITIALIZE。

```
sp_DRIVER_INITIALIZE DriverEntry;
```

如果回调函数具有函数原型声明，则必须将函数原型替换为函数角色类型声明。

| 函数角色类型                        | Storport 例程                                                                                                               |
|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| sp\_驱动程序\_初始化                    | DriverEntry                                                                                                                    |
| HW\_初始化                            | [**HwStorInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_initialize)                                                                               |
| HW\_BUILDIO                               | [**HwStorBuildIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_buildio)                                                                                     |
| HW\_STARTIO                               | [**HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio)                                                                                     |
| HW\_中断                             | [**HwStorInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_interrupt)                                                                                 |
| HW\_定时器                                 | [**HwStorTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_timer)                                                                                         |
| HW\_查找\_适配器                         | [**HwStorFindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)                                                                             |
| HW\_重置\_总线                            | [**HwStorResetBus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_reset_bus)                                                                                   |
| HW\_适配器\_控制                      | [**HwStorAdapterControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_adapter_control)                                                                       |
| HW\_被动\_初始化\_例程          | [**HwStorPassiveInitializeRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_passive_initialize_routine)                                                   |
| HW\_DPC\_例程                          | [**HwStorDpcRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_dpc_routine)                                                                               |
| HW\_免费\_适配器\_资源              | HwFreeAdapterResources 部分[**虚拟\_硬件\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_virtual_hw_initialization_data)结构。  |
| HW\_处理\_服务\_请求             | HwProcessServiceRequest 部分[**虚拟\_硬件\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_virtual_hw_initialization_data)结构。 |
| \_SERVICE\_IRP 的硬件\_完成                | HwCompleteServiceIrp 部分[**虚拟\_硬件\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_virtual_hw_initialization_data)结构。    |
| HW\_初始化\_跟踪                   | HwInitializeTracing 部分[**虚拟\_硬件\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_virtual_hw_initialization_data)结构。     |
| 硬件\_清理\_跟踪                      | HwCleanupTracing 部分[**虚拟\_硬件\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_virtual_hw_initialization_data)结构。        |
| 虚拟\_HW\_查找\_适配器                | HwFindAdapter 部分[**虚拟\_硬件\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_virtual_hw_initialization_data)结构。           |
| HW\_消息\_\_例程\_中断发出信号 | [**HwMSInterruptRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_message_signaled_interrupt_routine)                                                                       |

 

 

 





