---
title: 了解删除 IRP 的命令是何时发出的
description: 了解删除 IRP 的命令是何时发出的
keywords:
- 删除 Irp WDK PnP
- Irp WDK PnP
- I/o 请求数据包 WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77310b39a4405e21e700c9b0c05a72f3f8940c18
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840691"
---
# <a name="understanding-when-remove-irps-are-issued"></a>了解删除 IRP 的命令是何时发出的





下图显示了删除设备的驱动程序时所涉及的典型 Irp 序列。

![说明典型删除 irp 转换的关系图](images/rem-irps.png)

以下说明与上图中的带圆圈数字相对应：

1.  查询删除

    PnP 管理器颁发 [**IRP \_ MN \_ 查询 \_ 删除 \_ 设备**](./irp-mn-query-remove-device.md) ，以询问是否可以在不中断计算机的情况下删除设备。 当用户请求更新设备的驱动程序时，它还会发送此 IRP，并在 Windows 2000 和更高) 版本上 ()  (设备管理器禁用设备时发送。  (在 Windows 98/Me 上，PnP 管理器会在这种情况下发送停止 Irp;有关详细信息，请参阅 [停止设备](stopping-a-device.md) 。 ) 

    如果设备堆栈中的所有驱动程序都返回状态 " \_ 成功"，则驱动程序会将设备置于 "消除挂起" 状态。 在此状态下，驱动程序不能启动阻止设备被删除的任何操作。

    在这种 "清除" 删除情况下，PnP 管理器会先发送一个查询删除 IRP，然后再发送删除 IRP。 有关 "意外" 删除的说明，请参阅步骤5。

    尽管上面的关系图中未显示，但总线驱动程序可能会为未启动的设备接收 **IRP \_ MN \_ 查询 \_ 删除 \_ 设备** 。 如果用户请求动态删除计算机上物理上存在但已禁用的设备，则可能会发生这种情况。

2.  成功查询后删除

    PnP 管理器颁发 [**IRP \_ MN \_ remove \_ 设备**](./irp-mn-remove-device.md) ，以删除设备驱动程序。

    驱动程序必须成功进行此请求。 设备的驱动程序执行任何必要的清理，从设备堆栈分离，并删除 FDO 和任何筛选器 DOs。 父总线驱动程序将保留 PDO，直到用户从计算机物理上删除该设备。

    请注意，在删除 IRP 之前，驱动程序可能会收到 [**IRP \_ MN \_ 停止 \_ 设备**](./irp-mn-stop-device.md) ，但这不是必需的。 在 Windows 2000 和更高版本中， **IRP \_ MN \_ 停止 \_ 设备** 仅用于暂停设备以进行资源重新平衡; 它不是删除的步骤。 如果用户在设备停止时删除设备硬件，PnP 管理器会在停止 IRP 后的某个时间点发送删除 IRP，但停止不是删除的先决条件。

3.  Reenumerate 设备

    如果设备在驱动程序删除其设备对象之后 reenumerated，则 PnP 管理器会调用驱动程序的 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程，并颁发 [**IRP \_ MN \_ 启动 \_ 设备**](./irp-mn-start-device.md) 来恢复设备。  (另请参阅 [PnP 透视图中的设备状态](state-transitions-for-pnp-devices.md#ddk-state-transitions-for-pnp-devices-kg) 。 ) 

4.  取消查询删除

    PnP 管理器颁发 [**IRP \_ MN \_ cancel \_ remove \_ 设备**](./irp-mn-cancel-remove-device.md) 以取消查询-删除请求。

    为了响应 **IRP \_ MN \_ CANCEL \_ REMOVE \_ 设备**，驱动程序将设备恢复到其启动状态。

5.  意外删除 windows 2000 和更高版本的 Windows () 

    在 Windows 2000 和更高版本的系统上，如果用户在不使用拔出或弹出硬件程序的情况下从计算机断开设备，则 PnP 管理器会发送 [**IRP \_ MN \_ 惊喜 \_ 删除**](./irp-mn-surprise-removal.md) irp。

    这种情况称为 "意外" 删除，因为驱动程序不会提前发出警告。

    为了响应 **IRP MN 的 \_ \_ 意外 \_ 删除** IRP，该设备的驱动程序将无法完成任何未完成的 i/o 并释放设备使用的硬件资源。 驱动程序必须确保没有任何组件尝试访问设备，因为它不再存在。

    所有驱动程序都必须处理 **IRP \_ MN \_ 意外 \_ 删除** irp，并且必须将状态设置为 "成功" \_ 。

    无法取消 **IRP \_ MN \_ 意外 \_ 删除** 。

6.  删除后删除 (Windows 2000 和更高版本的 Windows) 

    关闭设备的所有打开的句柄时，PnP 管理器会将 [**IRP \_ MN \_ REMOVE \_ 设备**](./irp-mn-remove-device.md) 请求发送到设备的驱动程序。 每个驱动程序都从设备堆栈分离，并删除其设备对象。

7.  意外删除 Windows 98 () 

    在 Windows 98/Me 上，驱动程序不会在删除设备时收到 [**IRP \_ MN \_ 意外 \_ 删除**](./irp-mn-surprise-removal.md) ，而不会发出警告。 PnP 管理器只发送 **IRP \_ MN \_ 删除 \_ 设备**。 WDM 驱动程序必须具有处理 **irp \_ MN \_ 意外 \_ 删除** 的代码，后跟 **irp \_ MN \_ remove \_ 设备** (windows 2000 和更高版本的意外) 删除的行为，并且 **IRP \_ MN \_ 删除 \_ 设备** ，而没有以前的意外删除 IRP (Windows 98/Me 行为) 。

8.  在启动失败后删除 (Windows 2000 和更高版本) 

    如果设备的其中一个驱动程序未能通过 **irp \_ MN \_ 启动 \_ 设备**，PnP 管理器会将 **irp \_ MN \_ 删除 \_ 设备** 请求发送到设备堆栈。 这种删除 IRP 可确保通知设备的所有驱动程序设备未成功启动。 为响应 **IRP \_ MN \_ REMOVE \_ DEVICE** IRP，如果设备的驱动程序成功启动 IRP) 并撤消其 *AddDevice* 操作，则该设备的驱动程序将撤消其启动 (操作。 PnP 管理器将此类设备标记为 "启动失败"。

    此行为仅适用于 Windows 2000 和更高版本的平台。 在 Windows 98/Me 上，PnP 管理器会发送 **IRP \_ MN \_ 停止 \_ 设备** ，以响应失败的启动。

PnP 设备的驱动程序可以在更多情况下接收 **IRP \_ MN \_ 意外 \_ 删除** ，而不是说明典型的删除 IRP 转换。 例如，用户可以将 PC 卡插入到计算机中，然后在设备开始之前将其删除。 在这种情况下，PnP 管理器会在调用驱动程序的 *AddDevice* 例程之后、发出 **IRP \_ MN \_ 开始 \_ 设备** 请求之前发出意外的 IRP。 在调用驱动程序的 *AddDevice* 例程后，必须随时准备 PnP 设备的驱动程序来处理删除的 irp。

 

