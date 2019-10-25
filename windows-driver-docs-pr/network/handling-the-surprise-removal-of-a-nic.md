---
title: 处理 NIC 意外删除
description: 处理 NIC 意外删除
ms.assetid: afd94749-8f2a-4cce-a646-1f616a845a0e
keywords:
- 意外删除 WDK 网络
- Nic WDK 网络，意外删除
- 网络接口卡 WDK 网络，意外删除
- 即插即用 WDK NDIS 微型端口，意外 NIC 删除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ac8ba30425578fe336d0317786927c491b5ee25
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842546"
---
# <a name="handling-the-surprise-removal-of-a-nic"></a>处理 NIC 意外删除





如果用户从正在运行的系统中删除网络接口卡（NIC），而不事先通过用户界面（UI）通知系统，则会出现意外删除。

适用于 Windows Vista 和更高版本操作系统的微型端口驱动程序应能够处理意外删除。 具体而言，具有 Windows 驱动模型（WDM）下边缘的 NDIS 微型端口驱动程序应能够处理此类事件。 如果 NDIS-WDM 微型端口驱动程序不处理意外删除，则在无法完成意外删除之前，微型端口驱动程序发送到基础总线驱动程序的任何挂起的 Irp 都无法完成。

对于 Windows Vista 和更高版本，无需直接控制硬件的微型端口驱动程序（例如，具有 WDM 下边缘的微型端口驱动程序）应将 NDIS\_微型端口\_属性\_意外\_删除\_OK 属性调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)时的标志。 如果设置此标志，则当用户执行意外删除 NIC 时，会阻止显示警告。 无法处理意外删除的微型端口驱动程序不应设置此标志。

支持意外删除的微型端口驱动程序会自行尝试检测在正常操作过程中意外删除的[*MiniportDevicePnPEventNotify*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_device_pnp_event_notify)。 删除 NIC 后，尝试读取 NIC 的 i/o 端口通常会导致返回值，并将所有位设置为1。 如果微型端口驱动程序读取此类值，则它应检查是否存在具有更最终测试的硬件。 例如，微型端口驱动程序可以将值写入 i/o 端口，然后尝试从该端口读取该值。 小型端口驱动程序还可以检查 NIC 的 i/o 寄存器中的有效值。 如果以这种方式检测意外删除，则会阻止微型端口驱动程序在中断 DPC 中尝试读取已删除的 NIC 时，不会在无限循环中挂起。 以这种方式停止响应的微型端口驱动程序会阻止 NDIS 调用驱动程序的*MiniportDevicePnPEventNotify*函数。

 

 





