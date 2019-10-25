---
title: WIA 微型驱动程序如何从 WIA 接收断开连接
description: WIA 微型驱动程序如何从 WIA 服务接收断开连接事件
ms.assetid: 6ae3c230-d026-469e-a699-860a295fba85
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 056c06ffdf18b9387d9f2b33de239b1df3b8a1f4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840831"
---
# <a name="how-the-wia-minidriver-receives-a-disconnect-event-from-the-wia-service"></a>WIA 微型驱动程序如何从 WIA 服务接收断开连接事件

当设备从计算机意外地断开连接时（例如，当用户从计算机断开 USB 电缆连接时），WIA 服务将使用 WIA\_事件\_设备调用[**IWiaMiniDrv：:D rvnotifypnpevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)方法\_断开连接事件。 有关**IWiaMiniDrv：:D rvnotifypnpevent**方法的示例实现，请参阅[添加中断事件支持](adding-interrupt-event-support.md)。

WIA 微型驱动程序不应尝试在此事件期间或之后与硬件通信。 此事件表示 WIA 服务将卸载微型驱动程序。 当 WIA 服务重新加载微型驱动程序时，允许的下一个设备访问权限。 建议微型驱动程序设置一个标志，阻止所有[IWiaMiniDrv](iwiaminidrv-com-interface.md)接口调用访问该硬件，直到它重新连接。

WIA\_事件\_设备\_断开连接事件并非始终发送到 WIA 微型驱动程序。 当计算机关闭并且 WIA 服务正在卸载 WIA 驱动程序时，它不会发送此事件。 此事件应视为设备硬件禁用操作。

 



