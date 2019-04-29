---
title: 了解删除 IRP 的命令是何时发出的
description: 了解删除 IRP 的命令是何时发出的
ms.assetid: e92e30ce-ca0d-4f00-b54a-778bafba15b3
keywords:
- 删除 Irp WDK 即插即用
- WDK PnP Irp
- I/O 请求数据包 WDK 即插即用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3d658f24a3a803057f393bcc410621083a79bd2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355308"
---
# <a name="understanding-when-remove-irps-are-issued"></a>了解删除 IRP 的命令是何时发出的





下图显示了典型的 Irp 序列涉及中删除设备驱动程序。

![说明典型的关系图删除 irp 转换](images/rem-irps.png)

以下说明与上图中带圆圈的数字相对应：

1.  删除查询

    即插即用 manager 问题[ **IRP\_MN\_查询\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551705)询问是否可以无需中断在计算机中移除某个设备。 它还会发送此 IRP，当用户请求时更新设备管理器禁用的设备驱动程序的设备和 （在 Windows 2000 和更高版本）。 (在 Windows 98 上 / PnP 管理器发送我，在此情况下停止 Irp; 请参阅[停止设备](stopping-a-device.md)有关详细信息。)

    如果设备堆栈中的所有驱动程序返回状态\_成功后，驱动程序已将设备置于挂起删除状态。 在此状态下，驱动程序必须启动删除阻止设备的任何操作。

    在"清理"删除此种情况下，即插即用管理器发送查询删除 IRP 发送删除 IRP 之前。 请参阅有关"意外"删除的说明的步骤 5。

    尽管它不上述关系图中所示，总线驱动程序可能会收到**IRP\_MN\_查询\_删除\_设备**未启动的设备。 如果用户请求能够动态删除计算机上以物理方式存在但已禁用的设备，则可能发生此问题。

2.  成功查询后删除

    即插即用 manager 问题[ **IRP\_MN\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551738)删除设备驱动程序。

    驱动程序必须成功完成此请求。 设备的驱动程序执行任何必要的清理、 从设备堆栈中分离和删除 FDO 和任何筛选 DOs。 父总线驱动程序将保留 PDO，直到用户从计算机中物理移除设备。

    请注意驱动程序可能会收到[ **IRP\_MN\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551755)在删除之前 IRP，但它不是必需。 在 Windows 2000 及更高版本， **IRP\_MN\_停止\_设备**只能与使用暂停设备的资源重新平衡; 它不是步删除。 如果用户删除设备硬件设备停止时，即插即用管理器将在某个时候删除 IRP 发送后停止 IRP，但停止不是删除的先决条件。

3.  Reenumerate 设备

    如果设备重新枚举驱动程序已删除其设备对象后，即插即用管理器会调用驱动程序的[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程和问题[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)可恢复已暂停设备。 (另请参阅[视角即插即用设备状态](state-transitions-for-pnp-devices.md#ddk-state-transitions-for-pnp-devices-kg)图。)

4.  取消查询删除

    即插即用 manager 问题[ **IRP\_MN\_取消\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff550823)来取消的查询删除请求。

    以响应**IRP\_MN\_取消\_删除\_设备**，驱动程序将设备恢复为其已启动状态。

5.  意外删除 （Windows 2000 和更高版本的 Windows）

    在 Windows 2000 和更高版本的系统，如果用户断开而无需使用拔出或弹出硬件程序从计算机的设备的即插即用的管理器将发送[ **IRP\_MN\_惊讶\_删除**](https://msdn.microsoft.com/library/windows/hardware/ff551760) IRP。

    这种情况下被称为"意外"删除，因为驱动程序不出现任何提前警告。

    以响应**IRP\_MN\_惊讶\_删除**IRP，设备的驱动程序失败，任何未完成 i/o 操作和发布使用设备的硬件资源。 驱动程序必须确保没有任何组件尝试访问设备，因为它已不再存在。

    所有驱动程序必须处理**IRP\_MN\_惊讶\_删除**IRP，必须将状态设置为状态\_成功。

    **IRP\_MN\_惊讶\_删除**无法取消。

6.  删除后意外删除 （Windows 2000 和更高版本的 Windows）

    PnP 管理器时都将关闭所有打开的句柄到设备，将发送[ **IRP\_MN\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551738)到设备的驱动程序的请求。 每个驱动程序从设备堆栈中分离，并删除其设备对象。

7.  意外删除 (Windows 98 / 我)

    在 Windows 98 上 / 我来说，不会收到一个驱动程序[ **IRP\_MN\_惊讶\_删除**](https://msdn.microsoft.com/library/windows/hardware/ff551760)何时设备删除而不发出警告。 PnP 管理器仅发送**IRP\_MN\_删除\_设备**。 WDM 驱动程序必须具有代码处理两者**IRP\_MN\_惊讶\_删除**跟**IRP\_MN\_删除\_设备** （Windows 2000 和更高版本的行为感到惊讶删除） 和一个**IRP\_MN\_删除\_设备**事先惊讶-删除 IRP (Windows 98 / 我行为）。

8.  删除后失败的启动 (Windows 2000 及更高版本)

    如果某个设备的驱动程序出现故障**IRP\_MN\_启动\_设备**，即插即用管理器将发送**IRP\_MN\_删除\_设备**对设备堆栈请求。 此类删除 IRP 可确保这些设备的所有驱动程序将收到通知设备未成功启动。 以响应**IRP\_MN\_删除\_设备**IRP，设备的驱动程序撤消其开始操作 （如果它们已成功开始 IRP） 和撤消其*AddDevice*操作。 PnP 管理器将标记此类设备为"失败开始"。

    此行为适用于 Windows 2000 和更高版本的平台。 在 Windows 98 上 / PnP 管理器发送的我**IRP\_MN\_停止\_设备**以响应失败的启动。

即插即用设备的驱动程序可以接收**IRP\_MN\_惊讶\_删除**多情况下不显示在图中演示典型的那些将删除 IRP 转换中。 例如，用户无法 PC 卡插入计算机并启动设备之前，请删除它。 在这种情况下，即插即用的管理器将驱动程序的后发出意外删除 IRP *AddDevice*例程是被调用，但在发出之前**IRP\_MN\_启动\_设备**请求。 驱动程序的即插即用设备必须准备好处理 Irp 随时删除驱动程序的后*AddDevice*调用例程。

 

 




