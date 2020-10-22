---
title: Windows 内核模式即插即用管理器
description: Windows 内核模式即插即用管理器
ms.assetid: 43d06dbe-da66-4103-8be3-f27ff075a1b4
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3d75abca0f5e3ca176ead9a39277538a7834110d
ms.sourcegitcommit: 1690ad77580a2cfc47debb9751fd109a5991dd52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345957"
---
# <a name="windows-kernel-mode-plug-and-play-manager"></a>Windows 内核模式即插即用管理器


即插即用 (PnP) 是硬件技术和软件技术的组合，使 PC 能够识别设备何时添加到系统中。 通过 PnP，系统配置可以在用户的少量输入或无输入的情况下进行更改。 例如，当接通 USB 拇指驱动器后，Windows 可以检测拇指驱动器，并自动将其添加到文件系统。 但是，若要执行此操作，硬件必须遵循某些要求，因此必须满足驱动程序的要求。

有关用于驱动程序的 PnP 的详细信息，请参阅 [即插即用](introduction-to-plug-and-play.md)。

PnP 管理器实际上是 i/o 管理器的子系统。 有关 i/o 管理器的详细信息，请参阅 [Windows Kernel-Mode I/o 管理器](windows-kernel-mode-i-o-manager.md)。

有关 PnP 例程的列表，请参阅 [即插即用例程](/windows-hardware/drivers/ddi/_kernel/#plug-and-play-routines)。

请注意，没有可为 PnP 管理器提供直接接口的例程;也就是说，没有 "**Pp**" 例程。

Windows 驱动程序框架 (WDF) 提供一组库来简化 PnP 管理。 有关 WDF 的详细信息，请参阅 [内核模式驱动程序框架概述](../wdf/index.md)。

 

