---
title: 蓝牙打印
description: 蓝牙打印
ms.assetid: 6c40c142-9b52-4878-a84b-82d411086304
keywords:
- 打印机驱动程序 WDK，蓝牙
- 蓝牙 WDK，打印
- 无线连接 WDK 打印机
ms.date: 06/02/2020
ms.localizationpriority: medium
ms.openlocfilehash: ddcdf0dcc281e7b2e70ac562ba0895bab7fbf46c
ms.sourcegitcommit: a2003149edf03fb18c0c9608a010583e9599ebd1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2020
ms.locfileid: "84418960"
---
# <a name="bluetooth-printing"></a>蓝牙打印

如果打印设备支持蓝牙，则它应满足以下要求：

- 如果打印设备在其 USB 或并行总线上返回 1284 ID，则蓝牙总线必须返回 1284 ID。 如果出于[即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)（PnP）和标识目的，设备将在并行或 USB 总线上返回 1284 Id，蓝牙总线还必须使用 1284 id 才能进行 PnP 标识。

  > [!NOTE]
  > 即使从来没有并行端口或 USB 端口的 skimmingDevices 应该仍包含 1284 ID，用户也应注意到的信息。 如果没有 1284 ID，PnP 将不会创建打印队列。

- 设备应返回其 USB 或并行总线返回的同一 1284 ID，以便 Microsoft Windows 操作系统可以正确识别设备，并且不会将其与通过不同总线连接的同一设备混淆。 如果任何总线上的设备使用的 ID 都为1284，则应通过蓝牙返回相同的 ID。

  Windows 操作系统不使用 1284 ID 跟踪通过多个总线附加的设备。 打印机应使用相同的 1284 ID，以便操作系统可以通过单个 INF 条目加载适当的驱动程序。 打印机总线驱动程序使用和未指定总线创建 PnP Id。 例如，蓝牙打印机获取格式为 "BTHPRINT hpdeskje1234" 的 ID \\ ，格式为 "hpdeskje1234"。 第一种形式是特定于总线的，第二种形式是与主线无关。 您可以使用其中任一 Id 创建 INF，这取决于您的驱动程序包是否完全是特定于总线的。

- 设备必须支持蓝牙硬副本替换配置文件（HCRP）。 有关 HCRP for Bluetooth 的详细信息，请参阅[蓝牙](https://go.microsoft.com/fwlink/p/?linkid=26268)网站。

  > [!NOTE]
  > Microsoft 支持串行端口配置文件（SPP），但需要进行身份验证。 但是，我们建议使用 HCRP 而不是 SPP，因为 HCRP 提供了更好的用户体验。
