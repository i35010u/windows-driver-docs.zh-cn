---
title: 了解删除 IRP 的命令是何时发出的
description: 了解删除 IRP 的命令是何时发出的
ms.assetid: e92e30ce-ca0d-4f00-b54a-778bafba15b3
keywords:
- 删除 Irp WDK PnP
- Irp WDK PnP
- I/o 请求数据包 WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f609a1974aebb13763d488a80dfe7c05ac36bf3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838380"
---
# <a name="understanding-when-remove-irps-are-issued"></a>了解删除 IRP 的命令是何时发出的





下图显示了删除设备的驱动程序时所涉及的典型 Irp 序列。

![说明典型删除 irp 转换的关系图](images/rem-irps.png)

以下说明与上图中的带圆圈数字相对应：

1.  查询删除

    PnP 管理器颁发[**IRP\_MN\_QUERY\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)，以询问是否可以在不中断计算机的情况下删除设备。 当用户请求更新设备的驱动程序，（在 Windows 2000 和更高版本上）设备管理器禁用设备时，它也会发送此 IRP。 （在 Windows 98/Me 上，PnP 管理器会在这种情况下发送停止 Irp; 有关详细信息，请参阅[停止设备](stopping-a-device.md)。）

    如果设备堆栈中的所有驱动程序返回状态\_成功，则驱动程序会将设备置于 "消除挂起" 状态。 在此状态下，驱动程序不能启动阻止设备被删除的任何操作。

    在这种 "清除" 删除情况下，PnP 管理器会先发送一个查询删除 IRP，然后再发送删除 IRP。 有关 "意外" 删除的说明，请参阅步骤5。

    尽管上面的关系图中未显示，但总线驱动程序可能会收到**IRP\_MN\_查询\_删除**未启动的设备的\_设备。 如果用户请求动态删除计算机上物理上存在但已禁用的设备，则可能会发生这种情况。

2.  成功查询后删除

    PnP 管理器颁发[**IRP\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)以删除设备驱动程序。

    驱动程序必须成功进行此请求。 设备的驱动程序执行任何必要的清理，从设备堆栈分离，并删除 FDO 和任何筛选器 DOs。 父总线驱动程序将保留 PDO，直到用户从计算机物理上删除该设备。

    请注意，在删除 IRP 之前，驱动程序可能会收到[**IRP\_MN\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)，但这不是必需的。 在 Windows 2000 和更高版本中， **IRP\_MN\_停止\_设备**仅用于暂停设备进行资源重新平衡;这并不是一个删除步骤。 如果用户在设备停止时删除设备硬件，PnP 管理器会在停止 IRP 后的某个时间点发送删除 IRP，但停止不是删除的先决条件。

3.  Reenumerate 设备

    如果设备在驱动程序删除其设备对象之后 reenumerated，则 PnP 管理器会调用驱动程序的[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程，并颁发[**IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)以恢复设备。 （另请参阅[PnP 透视图中的设备状态](state-transitions-for-pnp-devices.md#ddk-state-transitions-for-pnp-devices-kg)。）

4.  取消查询删除

    PnP 管理器颁发[**IRP\_MN\_cancel\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-remove-device)以取消查询-删除请求。

    为了响应**IRP\_MN\_取消\_删除\_设备**，驱动程序会将设备恢复到其启动状态。

5.  意外删除（Windows 2000 和更高版本的 Windows）

    在 Windows 2000 和更高版本的系统上，如果用户在不使用拔出或弹出硬件程序的情况下从计算机断开设备，则 PnP 管理器会[ **\_意外\_删除 irp 发送 irp\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal) 。

    这种情况称为 "意外" 删除，因为驱动程序不会提前发出警告。

    为了响应**IRP\_MN\_意外\_删除**IRP，设备的驱动程序将无法完成的 i/o，并释放设备使用的硬件资源。 驱动程序必须确保没有任何组件尝试访问设备，因为它不再存在。

    所有驱动程序都必须处理**IRP\_MN\_惊喜\_删除**IRP，并将状态设置\_为 "成功"。

    无法取消**IRP\_MN\_意外\_删除**。

6.  删除意外删除后删除（Windows 2000 和更高版本的 Windows）

    关闭设备的所有打开的句柄时，PnP 管理器会发送[**IRP\_MN\_删除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)设备驱动程序\_设备请求。 每个驱动程序都从设备堆栈分离，并删除其设备对象。

7.  意外删除（Windows 98/Me）

    在 Windows 98/Me 上，驱动程序不会收到 IRP\_MN 在删除设备时不会出现任何警告， [ **\_意外\_删除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)。 PnP 管理器只发送**IRP\_MN\_删除\_设备**。 WDM 驱动程序必须具有处理**irp\_MN\_意外\_删除**的代码，然后使用**irp\_MN\_删除\_设备**（Windows 2000 和更高版本的意外删除行为）和**IRP\_MN\_** 在没有以前的意外删除 IRP （Windows 98/Me 行为）的情况下删除\_设备。

8.  启动失败后删除（Windows 2000 及更高版本）

    如果设备的其中一个驱动程序未能通过**irp\_MN\_启动\_设备**，PnP 管理器会将**irp\_MN 发送到\_删除\_设备**请求到设备堆栈。 这种删除 IRP 可确保通知设备的所有驱动程序设备未成功启动。 为了响应**IRP\_MN\_删除\_设备**IRP，设备的驱动程序将撤消其启动操作（如果已成功启动 IRP）并撤消其*AddDevice*操作。 PnP 管理器将此类设备标记为 "启动失败"。

    此行为仅适用于 Windows 2000 和更高版本的平台。 在 Windows 98/Me 上，PnP 管理器发送**IRP\_MN\_停止\_设备**，以响应失败的启动。

PnP 设备的驱动程序可能会收到**IRP\_MN\_** 在更多情况下\_删除操作，而不是说明典型删除 IRP 转换的图中显示的情况。 例如，用户可以将 PC 卡插入到计算机中，然后在设备开始之前将其删除。 在这种情况下，PnP 管理器会在调用驱动程序的*AddDevice*例程后发出意外删除 irp，但在发出**IRP\_MN\_启动\_设备**请求之前。 在调用驱动程序的*AddDevice*例程后，必须随时准备 PnP 设备的驱动程序来处理删除的 irp。

 

 




