---
title: AV/C 连接方案
description: AV/C 连接方案
keywords:
- 连接 WDK AV/C
- AV/C WDK，连接方案
- 数字视频 WDK AV/C
- DV WDK AV/C
- Set-Top Box WDK AV/C
- STB WDK AV/C
- TV WDK AV/C
- 电视 WDK AV/C
- 子次级支持 WDK AV/C
- 内部连接 WDK AV/C
- 设备间连接 WDK AV/C
- Avc.sys 函数驱动程序 WDK，连接
- 外部插头连接 WDK AV/C
ms.date: 03/05/2021
ms.localizationpriority: medium
ms.openlocfilehash: 68200e57f47a8f4df5dc111da154f907b9d1269e
ms.sourcegitcommit: 57ffd9cfed01220923bdd0b20539e32a0e211caf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102236417"
---
# <a name="avc-connection-scenarios"></a>AV/C 连接方案

在 Windows Vista 之前，连接和兼容性管理 (中的 CCM) 协议 *Avc.sys* 支持单一连接方案，在此方案中，计算机充当外部 AV/C 设备的控制器来启动来自设备的数据流。 例如，若要开始流式传输， *Avc.sys* 中的连接管理在设备上的子单位与设备单位的同步输出插头之间建立连接，方法是使用 "连接" 和 "断开连接单元" 命令 ([**AVC \_ function \_ 获取**](./avc-function-acquire.md) 和 [**AVC \_ 函数) \_ 版本**](./avc-function-release.md)。

在 Windows Vista 中，已对连接管理进行了改进，以支持7个以上的连接方案，使 *Avc.sys* 支持8个单位/子单位的连接方案。 连接管理的改进增加了对从子源插入到其他子源的连接的支持;子单元连接可以在同一 AV/C 单位内或不同的 AV/C 单位内。 *Avc.sys* 通过使用信号源，然后输入-选择 CCM 协议单元命令建立连接。  (*Avc.sys* 支持其他 CCM 协议单元命令（如输出预设），且仅支持 AV/C 规范所需的级别。 ) 

有两种常规连接类型与 AV/C 单元和子单元连接相关：

- *一种连接，其中，外部设备连接到主计算机，并且计算机可以控制连接，但它不是连接的一部分*。 此连接类型不使用任何基于主机的内存。 相反，连接是包含设备的无内存介质，主机只充当控制器。 此类连接的一个示例是 Set-Top (框的调谐器子) ，它将数据直接流式传输到数字电视的 "监视" 子单位，而不会在计算机上处理数据流。

- *一种连接，其中，外部设备通过使用标准介质连接到主计算机，并使用缓冲区将数据从设备复制到主计算机的内存*。 这种连接类型的一个示例是将数据流式传输到计算机的数字视频 (DV) 设备，稍后处理数据。 *Msdv.sys* 驱动程序在 DV 设备和主计算机) 之间使用这种类型的连接 (。

在 *Avc.sys* 中为 Windows Vista 实现的改进连接管理适用于第一种连接类型，在该连接中，设备可以响应 AV/C 命令进行内部连接。 *Avc.sys* 中改进的连接管理可以在同一 IEEE 1394 总线) 上的两个磁带子单元连接之间建立端到端连接，如果设备支持 AV/c CCM 协议 (。

> [!NOTE]
> *Avc.sys* 不支持 (内存缓冲区) 的第二种连接类型。 但是，连接的内存缓冲区类型遵循 [IEC 61883](../ieee/iec-61883-client-drivers.md) 协议，并受同一堆栈中的底层 *61883.sys* 驱动程序的支持 (在这种情况下，计算机涉及到内存缓冲区连接) 。

## <a name="supported-connection-scenarios-in-windows-vista"></a>Windows Vista 中支持的连接方案

四种方案 (1 到 4) 表示单元 *内部* 连接。 这些连接完全包含在一个 AV/C 单元中。 其他四个方案 (5 到 8) 表示单元 *间* 的连接。 这些连接介于两个不同的 AV/C 单元之间。

以下主题讨论了8种不同的 AV/C 连接管理方案，以及 [**AVCCONNECTINFO**](/windows-hardware/drivers/ddi/avc/ns-avc-_avcconnectinfo) 结构成员的各个值：

[在一个 AV/C 单元中的子单元插头和单元插头之间的连接](connections-between-subunit-plugs-and-unit-plugs-within-one-av-c-unit.md)

[在一个 AV/C 单元中的两个子单元插头之间的连接](connections-between-two-subunit-plugs-within-one-av-c-unit.md)

[在不同 AV/C 单元中的两个子单元插头之间的连接](connections-between-two-subunit-plugs-in-different-av-c-units.md)

[在不同 AV/C 单元中的两个单元插头之间的连接](connections-between-two-unit-plugs-in-different-av-c-units.md)
