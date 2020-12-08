---
title: 全双工模式
description: 全双工模式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38a78d5a1fbc90adff3c1ee2f1d3a509b3f7c69d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804605"
---
# <a name="full-duplex-mode"></a>全双工模式


## <span id="ddk_full_duplex_mode_kg"></span><span id="DDK_FULL_DUPLEX_MODE_KG"></span>


Storport 驱动程序支持专门为高性能总线定制的 i/o 模型。 此 i/o 模型允许微型端口驱动程序在全双工模式下运行，这意味着，微型端口驱动程序可以将新请求添加到其队列中（即使正在完成其他请求）。 此外，在全双工模式下，微型端口驱动程序不必同步其 [**StartIo**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 和中断服务例程的执行。 这可能导致显著的性能增强。 但是，小型端口驱动程序必须设计为利用全双工模式，因为在默认情况下，Storport 以半双工模式运行。

微型端口驱动程序必须将 Storport 配置为在执行其 [**HwStorFindAdapter**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter) 例程时以全双工模式运行。 为此，可将微型端口驱动程序的 [**端口 \_ 配置 \_ 信息 (STORPORT)**](/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))结构的 **SynchronizationModel** 成员初始化为 **StorSynchronizeFullDuplex**。

 

