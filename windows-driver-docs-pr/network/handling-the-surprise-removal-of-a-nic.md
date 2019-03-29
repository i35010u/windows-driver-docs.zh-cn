---
title: 处理 NIC 意外删除
description: 处理 NIC 意外删除
ms.assetid: afd94749-8f2a-4cce-a646-1f616a845a0e
keywords:
- 意外删除 WDK 网络
- Nic WDK 网络，意外删除
- 网络接口卡 WDK 网络，意外删除
- 即插即用 WDK NDIS 微型端口，在意外删除 NIC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3132b3b85b026a8ef707a9cdf07653a608f3cb5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565429"
---
# <a name="handling-the-surprise-removal-of-a-nic"></a>处理 NIC 意外删除





当用户中删除网络接口卡 (NIC) 从正在运行的系统，而不通知事先通过用户界面 (UI) 系统时出现意外删除。

Windows Vista 和更高版本的操作系统的微型端口驱动程序应能处理意外删除。 具体而言，Windows 驱动程序模型 (WDM) 的下边缘与的 NDIS 微型端口驱动程序应该能够处理此类事件。 如果 NDIS WDM 微型端口驱动程序不处理意外删除，无法完成任何挂起的微型端口驱动程序发送到基础总线驱动程序之前被意外删除的 Irp。

对于 Windows Vista 和更高版本中，一个微型端口驱动程序 （如使用 WDM 下边缘的微型端口驱动程序），不直接控制硬件应设置 NDIS\_微型端口\_特性\_惊讶\_删除\_调用时的确定的特性标志[ **NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)。 将设置此标志可阻止用户在执行在意外删除 NIC 时显示一条警告 不能处理意外删除的微型端口驱动程序不应设置此标志。

微型端口驱动程序支持意外删除本身应尝试检测正常操作-上下文的外部过程在意外删除[ *MiniportDevicePnPEventNotify*](https://msdn.microsoft.com/library/windows/hardware/ff559369)。 删除 NIC 后，尝试读取 NIC 的 I/O 端口通常返回结果的所有位设置为一个值。 如果微型端口驱动程序将读取此类值，它应与多本测试检查硬件存在。 例如，微型端口驱动程序无法写入到 I/O 端口值，然后尝试从该端口读取值。 微型端口驱动程序还可以检查 NIC 的 I/O 寄存器中的有效值。 检测在意外删除中的方式可防止微型端口驱动程序时它会尝试读取已删除的 NIC 的寄存器中中断 DPC 挂起一个无限循环中... 停止响应以这种方式的微型端口驱动程序调用的驱动程序阻止 NDIS *MiniportDevicePnPEventNotify*函数。

 

 





