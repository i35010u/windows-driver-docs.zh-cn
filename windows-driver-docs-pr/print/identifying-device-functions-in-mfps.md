---
title: 识别 MFP 中的设备函数
description: 识别 MFP 中的设备函数
ms.assetid: 14016c43-b93a-4009-848b-1bcf3f1d94b6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c040bfae10bdc7c27884a91e62902ea730b3e665
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380834"
---
# <a name="identifying-device-functions-in-mfps"></a>识别 MFP 中的设备函数

设备和打印机用户界面使用的设备容器标识符 (ContainerID) 来标识属于 MFP 打印机和扫描仪功能。 ContainerID 是一个 GUID，中的所有功能的设备实例 (devnodes) MFP 或其他多功能设备可用于标识其自身作为同一个多功能设备的一部分。 例如，打印机功能的设备实例和 MFP 中的扫描程序功能的设备实例应具有相同的 ContainerID 值。

设备可能会报告 ContainerID.If 设备不报告 ContainerID、 即插即用的 Windows 将分配一个设备。 Windows 即插即用通过充分利用许多的多功能设备都有表示作为一个整体的多功能设备，父设备和子设备表示多功能中的各个函数的这一事实来执行此标识设备。 即插即用 manager 假定两个功能的设备实例都具有相同父和任一实例标记为可移动设备，两个实例必须是相同的多功能设备的永久成员。 通过使用此方法，即插即用的 Windows 可以将常见 ContainerIDs 分配给功能的设备实例。

可能通过多个传输连接的设备 （即设备连接时通过 USB 和 WSD），建议设备报告 ContainerID 以使不同的设备实例显示为一台设备。

有关 ContainerIDs 详细信息，请参阅[容器 ID](https://docs.microsoft.com/windows-hardware/drivers/install/container-ids)。
