---
title: WIA 微型驱动程序如何从 WIA 接收断开连接
description: WIA 微型驱动程序如何从 WIA 服务接收断开连接事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9f9b3a3c2fcaba5b653d15670120b8620b06b56
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793729"
---
# <a name="how-the-wia-minidriver-receives-a-disconnect-event-from-the-wia-service"></a>WIA 微型驱动程序如何从 WIA 服务接收断开连接事件

当设备从计算机意外地断开连接时，例如当用户从计算机断开 USB 电缆时，WIA 服务将使用 WIA [**IWiaMiniDrv::drvNotifyPnpEvent**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent) \_ 事件 \_ 设备 \_ 断开连接事件调用 IWiaMiniDrv：:d rvnotifypnpevent 方法。 有关 **IWiaMiniDrv：:D rvnotifypnpevent** 方法的示例实现，请参阅 [添加中断事件支持](adding-interrupt-event-support.md)。

WIA 微型驱动程序不应尝试在此事件期间或之后与硬件通信。 此事件表示 WIA 服务将卸载微型驱动程序。 当 WIA 服务重新加载微型驱动程序时，允许的下一个设备访问权限。 建议微型驱动程序设置一个标志，阻止所有 [IWiaMiniDrv](iwiaminidrv-com-interface.md) 接口调用访问该硬件，直到它重新连接。

WIA \_ 事件 \_ 设备 \_ 断开连接事件并非始终发送到 wia 微型驱动程序。 当计算机关闭并且 WIA 服务正在卸载 WIA 驱动程序时，它不会发送此事件。 此事件应视为设备硬件禁用操作。

