---
title: 处理设备接口更改事件
description: 处理设备接口更改事件
ms.assetid: 8966ca72-41d6-42bb-84a9-8f907a514338
keywords:
- 通知 WDK 即插即用设备接口更改
- EventCategoryDeviceInterfaceChange 通知
- 设备接口更改通知 WDK 即插即用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa09bfe834a0135fae404b6e4a2e6831d40a700c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542004"
---
# <a name="handling-device-interface-change-events"></a>处理设备接口更改事件





当驱动程序或用户模式组件启用或禁用设备接口实例时，即插即用管理器调用所有通知为注册的回调例程**EventCategoryDeviceInterfaceChange**在设备上的事件接口类。 若要指示通知的原因，即插即用管理器设置**事件**成员的回调例程*NotificationStructure* GUID 参数\_设备\_接口\_到达或 GUID\_设备\_接口\_删除。

当处理一个 GUID\_设备\_接口\_到达事件通知回调例程应：

-   用于处理新接口执行驱动程序定义的任务。

    通常情况下，通知回调例程直接在回调的上下文中打开设备。 但是，如果打开设备可能会导致后续即插即用事件发生 （例如枚举子设备），回调例程应改为加入队列的辅助角色例程，以打开设备;否则，可能发生死锁。

    回调例程可能会启用对新接口的可用性的响应中自己的接口。

当处理一个 GUID\_设备\_接口\_删除事件通知回调例程应：

-   撤消接口已启用时，它执行任何操作。

删除设备后，该驱动程序应关闭其 GUID 期间打开的文件句柄\_设备\_接口\_到达事件回调。 为有序设备删除时，该驱动程序应关闭文件句柄期间 GUID\_目标\_设备\_查询\_删除事件回调。 有关在意外删除，该驱动程序应关闭文件句柄期间 GUID\_目标\_设备\_删除\_完成事件回调。 在 GUID 不关闭文件句柄\_设备\_接口\_删除事件回调。

 

 




