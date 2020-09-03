---
title: 使用 Storport 驱动程序的函数角色类型来声明函数
description: 若要使 SDV 能够分析 Storport 驱动程序，必须使用为 Storport 定义的函数角色类型声明来声明函数。 函数角色类型在 Storport. h 中定义。
ms.assetid: 40BD11CD-A559-4F90-BF39-4ED2FB800392
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d34b3250e7159f9447d9950c68ac3e9521a427d0
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383957"
---
# <a name="declaring-functions-by-using-function-role-types-for-storport-drivers"></a>使用 Storport 驱动程序的函数角色类型来声明函数


若要使 SDV 能够分析 Storport 驱动程序，必须使用为 Storport 定义的函数角色类型声明来声明函数。 函数角色类型在 Storport. h 中定义。

必须通过指定相应的角色类型，在 Storport 驱动程序中声明每个回调函数。

下面的代码示例演示了 DriverIntialize 回调函数的函数角色类型声明。 函数角色类型是 sp \_ 驱动程序 \_ 初始化。

```
sp_DRIVER_INITIALIZE DriverEntry;
```

如果回调函数具有函数原型声明，则必须将函数原型替换为函数角色类型声明。

| 函数角色类型                        | Storport 例程                                                                                                               |
|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| sp \_ 驱动程序 \_ 初始化                    | DriverEntry                                                                                                                    |
| HW \_ 初始化                            | [**HwStorInitialize**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_initialize)                                                                               |
| HW \_ BUILDIO                               | [**HwStorBuildIo**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_buildio)                                                                                     |
| HW \_ STARTIO                               | [**HwStorStartIo**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio)                                                                                     |
| HW \_ 中断                             | [**HwStorInterrupt**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_interrupt)                                                                                 |
| HW \_ 计时器                                 | [**HwStorTimer**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_timer)                                                                                         |
| HW \_ 查找 \_ 适配器                         | [**HwStorFindAdapter**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)                                                                             |
| 硬件 \_ 重置 \_ 总线                            | [**HwStorResetBus**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_reset_bus)                                                                                   |
| HW \_ 适配器 \_ 控件                      | [**HwStorAdapterControl**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_adapter_control)                                                                       |
| HW \_ 被动 \_ 初始化 \_ 例程          | [**HwStorPassiveInitializeRoutine**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_passive_initialize_routine)                                                   |
| HW \_ DPC \_ 例程                          | [**HwStorDpcRoutine**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_dpc_routine)                                                                               |
| HW \_ 免费 \_ 适配器 \_ 资源              | [**虚拟 \_ HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/storport/ns-storport-_virtual_hw_initialization_data)结构的 HwFreeAdapterResources 部分。  |
| HW \_ 处理 \_ 服务 \_ 请求             | [**虚拟 \_ HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/storport/ns-storport-_virtual_hw_initialization_data)结构的 HwProcessServiceRequest 部分。 |
| HW \_ 完成 \_ 服务 \_ IRP                | [**虚拟 \_ HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/storport/ns-storport-_virtual_hw_initialization_data)结构的 HwCompleteServiceIrp 部分。    |
| HW \_ 初始化 \_ 跟踪                   | [**虚拟 \_ HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/storport/ns-storport-_virtual_hw_initialization_data)结构的 HwInitializeTracing 部分。     |
| HW \_ 清理 \_ 跟踪                      | [**虚拟 \_ HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/storport/ns-storport-_virtual_hw_initialization_data)结构的 HwCleanupTracing 部分。        |
| 虚拟 \_ HW \_ 查找 \_ 适配器                | [**虚拟 \_ HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/storport/ns-storport-_virtual_hw_initialization_data)结构的 HwFindAdapter 部分。           |
| HW \_ 消息 \_ 信号 \_ 中断 \_ 例程 | [**HwMSInterruptRoutine**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_message_signaled_interrupt_routine)                                                                       |

 

 

