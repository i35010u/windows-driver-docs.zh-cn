---
title: 使用 Storport 驱动程序的函数角色类型来声明函数
description: 若要启用 SDV 分析 Storport 驱动程序，必须使用为 Storport 定义的函数角色类型声明中声明函数。 Storport.h 中定义的函数角色类型。
ms.assetid: 40BD11CD-A559-4F90-BF39-4ED2FB800392
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64ecfc2e698591f8e373ed2e76d88cf034561acb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561972"
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
| HW\_初始化                            | [**HwStorInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff557396)                                                                               |
| HW\_BUILDIO                               | [**HwStorBuildIo**](https://msdn.microsoft.com/library/windows/hardware/ff557369)                                                                                     |
| HW\_STARTIO                               | [**HwStorStartIo**](https://msdn.microsoft.com/library/windows/hardware/ff557423)                                                                                     |
| HW\_中断                             | [**HwStorInterrupt**](https://msdn.microsoft.com/library/windows/hardware/ff557403)                                                                                 |
| HW\_计时器                                 | [**HwStorTimer**](https://msdn.microsoft.com/library/windows/hardware/ff557426)                                                                                         |
| HW\_查找\_适配器                         | [**HwStorFindAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff557390)                                                                             |
| HW\_重置\_总线                            | [**HwStorResetBus**](https://msdn.microsoft.com/library/windows/hardware/ff557415)                                                                                   |
| HW\_适配器\_控件                      | [**HwStorAdapterControl**](https://msdn.microsoft.com/library/windows/hardware/ff557365)                                                                       |
| HW\_被动\_初始化\_例程          | [**HwStorPassiveInitializeRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff557407)                                                   |
| HW\_DPC\_例程                          | [**HwStorDpcRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff557383)                                                                               |
| HW\_免费\_适配器\_资源              | HwFreeAdapterResources 一部分[**虚拟\_HW\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff568010)结构。  |
| HW\_PROCESS\_SERVICE\_REQUEST             | HwProcessServiceRequest 一部分[**虚拟\_HW\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff568010)结构。 |
| HW\_完成\_服务\_IRP                | HwCompleteServiceIrp 一部分[**虚拟\_HW\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff568010)结构。    |
| HW\_初始化\_跟踪                   | HwInitializeTracing 一部分[**虚拟\_HW\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff568010)结构。     |
| HW\_清理\_跟踪                      | HwCleanupTracing 一部分[**虚拟\_HW\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff568010)结构。        |
| 虚拟\_HW\_查找\_适配器                | HwFindAdapter 一部分[**虚拟\_HW\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff568010)结构。           |
| HW\_消息\_用信号通知\_中断\_例程 | [**HwMSInterruptRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff557268)                                                                       |

 

 

 





