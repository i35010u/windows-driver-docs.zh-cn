---
title: AV/C 连接方案
description: AV/C 连接方案
ms.assetid: 392f996c-47aa-4ceb-adf9-0c8fd114a511
keywords:
- 连接 WDK AV/C
- AV/C WDK，连接方案
- 数字的视频 WDK AV/C
- DV WDK AV/C
- 机顶盒 WDK AV/C
- STB WDK AV/C
- 电视 WDK AV/C
- 电视 WDK AV/C
- 子单元支持 WDK AV/C
- 内部单元连接 WDK AV/C
- 内部单位连接 WDK AV/C
- Avc.sys 功能驱动程序 WDK，连接
- 外部即插即用连接 WDK AV/C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c414a77ea2d7d330e62f9cbf383e8ce4adca0914
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384809"
---
# <a name="avc-connection-scenarios"></a>AV/C 连接方案





在 Windows Vista 之前的连接和兼容性管理 (CCM) 协议中*Avc.sys*支持单个连接方案中，计算机充当外部 AV/C 设备启动流式处理数据的控制器从设备中。 例如，若要开始流式处理中的连接管理*Avc.sys*之间建立了连接在设备上的子单元和将设备单位等时输出插件通过使用连接和断开连接单元命令 ([**AVC\_函数\_ACQUIRE** ](https://msdn.microsoft.com/library/windows/hardware/ff554148)并[ **AVC\_函数\_发布**](https://msdn.microsoft.com/library/windows/hardware/ff554169)，分别）。 有关 AV/C 规范和 CCM 协议的详细信息，请参阅[1394年贸易协会](https://go.microsoft.com/fwlink/p/?linkid=518448)网站。

在 Windows Vista 中，连接管理进行了改进以支持七个更多连接方案，以便*Avc.sys*支持八个单元/子单元连接方案。 连接管理改进可添加子单元插入到其他子单元插入; 支持的连接将子单元连接可以是同一 AV/C 单位中或在不同的 AV/C 单位。 *Avc.sys*使用信号源，然后输入选择 CCM 协议单元命令之间建立连接。 (*Avc.sys*支持其他 CCM 协议单元命令，如输出预设，仅对 AV/C 规范要求的级别。)

有两种常规类型的连接与 AV/C 单位和子单元连接相关的：

-   *在其中外部设备连接到主机计算机和计算机的连接可以控制的连接，但它不是连接的一部分*。 此连接类型不使用任何基于主机的内存。 相反，该连接是一个内存小于媒介与设备和主机只是充当一个控制器。 此类型的一个示例是连接的调谐器子单元的数据流式传输到数字电视信号，监视器子单元直接处理数据的流的计算机集顶部框 (STB)。

-   *在其中外部设备连接到主计算机通过使用标准中等规模，并使用缓冲区来将数据从设备复制到主计算机的内存的连接*。 此类型的示例是连接的数据流式传输到计算机，它更高版本处理数字视频 (DV) 设备。 *Msdv.sys*驱动程序将使用此类型的连接 （之间 DV 设备和主机计算机）。

为 Windows Vista 中实现的改进的连接管理*Avc.sys*适用于连接，在其中了设备可以响应 AV/C 命令以生成内部连接到的第一个类型。 中的改进的连接管理*Avc.sys*可以端到端之间建立连接两个磁带子单元连接中不同的 AV/C 设备 （同一 IEEE 1394 总线上），如果设备支持 AV/C CCM 协议。

**请注意**  *Avc.sys*不支持连接 （内存缓冲区） 的第二个类型。 但是，连接的内存缓冲区类型遵循[IEC 61883](https://msdn.microsoft.com/library/windows/hardware/ff537188)协议，支持由基础*是 61883.sys* （其中的计算机涉及到内存缓冲区中的同一堆栈中的驱动程序连接）。

 

### <a name="supported-connection-scenarios-in-windows-vista"></a>Windows Vista 中的受支持的连接方案

四种方案 (1 到 4) 表示*内部*-设备连接。 这些连接都在一个 AV/C 完全包含在。 四个其他方案 (5 至 8) 表示*间*-设备连接。 这些连接是两个不同的 AV/C 单位之间。

以下主题讨论的成员的八个不同 AV/C 连接管理方案和相应的值[ **AVCCONNECTINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff554101)结构：

[子单元插入和一个 AV/C 单位内的单元插入之间的连接](connections-between-subunit-plugs-and-unit-plugs-within-one-av-c-unit.md)

[一个 AV/C 单位内的两个子单元插入之间的连接](connections-between-two-subunit-plugs-within-one-av-c-unit.md)

[两个不同的 AV C 单元中的子单元插入之间的连接](connections-between-two-subunit-plugs-in-different-av-c-units.md)

[在不同的 AV C 单位中的两个单元插入之间的连接](connections-between-two-unit-plugs-in-different-av-c-units.md)

 

 




