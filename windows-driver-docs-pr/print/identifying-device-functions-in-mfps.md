---
title: 识别 MFP 中的设备函数
description: 识别 MFP 中的设备函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11051854d23ad3bb056798f206a3fea42a779d26
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835729"
---
# <a name="identifying-device-functions-in-mfps"></a>识别 MFP 中的设备函数

"设备和打印机" 用户界面使用设备容器标识符 (ContainerID) 来识别属于一个 MFP 的打印机和扫描仪函数。 ContainerID 是一个 GUID，在 MFP 或其他多功能设备中 (devnodes) 的所有功能设备实例都可以使用它将自身标识为同一多功能设备的一部分。 例如，MFP 中的打印机功能设备实例和扫描仪功能设备实例应具有相同的 ContainerID 值。

设备可能会报告 ContainerID。如果设备未报告 ContainerID，Windows PnP 将为设备分配一个 ContainerID。 Windows PnP 通过利用这一事实来执行此标识，其中许多多功能设备具有父设备，该设备表示整体的多功能设备，而子设备代表多功能设备中的单个功能。 PnP 管理器假定两个功能设备实例具有相同的父节点，并且如果两个实例都未标记为可移动设备，则这两个实例必须是同一多功能设备的永久成员。 通过使用此方法，Windows PnP 可以将常见的 ContainerIDs 分配给功能设备实例。

对于可能通过多个传输 (连接的设备，设备通过 USB 和 WSD) 进行连接，建议设备报告 ContainerID 以使不同的设备实例显示为一台设备。

有关 ContainerIDs 的详细信息，请参阅 [容器 ID](../install/container-ids.md)。
