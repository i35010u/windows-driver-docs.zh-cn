---
title: 处理设备接口更改事件
description: 处理设备接口更改事件
keywords:
- 通知 WDK PnP，设备接口更改
- EventCategoryDeviceInterfaceChange 通知
- 设备接口更改通知 WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3b142f09d10505d2ce06ce138a08672f200f04d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785119"
---
# <a name="handling-device-interface-change-events"></a>处理设备接口更改事件





当驱动程序或用户模式组件启用或禁用设备接口实例时，PnP 管理器会调用注册到设备接口类上的 **EventCategoryDeviceInterfaceChange** 事件的所有通知回调例程。 为指示通知的原因，PnP 管理器会将回调例程的 *NotificationStructure* 参数的 **事件** 成员设置为 guid \_ 设备 \_ 接口 \_ 到达或 guid \_ 设备 \_ 接口 \_ 删除。

当处理 GUID \_ 设备 \_ 接口 \_ 到达事件时，通知回调例程应：

-   执行驱动程序定义的任务以处理新的接口。

    通常，通知回调例程会直接在回调的上下文中打开设备。 但是，如果打开设备可能会导致后续 PnP 事件 (例如，) 子设备的枚举，则回调例程应改为将辅助例程排队以打开设备;否则，可能会发生死锁。

    回调例程可能会自行启用接口，以响应新接口的可用性。

当处理 GUID \_ 设备 \_ 接口 \_ 删除事件时，通知回调例程应：

-   撤消在启用接口时执行的任何操作。

删除设备后，驱动程序应关闭在 GUID \_ 设备 \_ 接口 \_ 到达事件回调过程中打开的文件句柄。 对于有序的设备删除，驱动程序应在 GUID \_ 目标 \_ 设备 \_ 查询 \_ 删除事件回调期间关闭文件句柄。 对于意外删除，驱动程序应在 GUID \_ 目标 \_ 设备 \_ 删除 \_ 完成事件回调期间关闭文件句柄。 请勿在 GUID \_ 设备 \_ 接口 \_ 删除事件回调期间关闭文件句柄。

 

 




