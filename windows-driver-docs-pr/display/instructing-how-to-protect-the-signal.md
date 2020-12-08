---
title: 指示如何保护信号
description: 指示如何保护信号
keywords:
- 复制保护 WDK COPP，信号保护
- 视频复制保护 WDK COPP，信号保护
- COPP WDK DirectX VA，信号保护
- 受保护的视频 WDK COPP，信号保护
- 信号保护 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d56ff7cd8b689340103606ae627cce4019b4e1ce
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838075"
---
# <a name="instructing-how-to-protect-the-signal"></a>指示如何保护信号


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

COPP 命令可提供有关如何保护通过与 DirectX VA COPP 设备关联的物理连接器的信号的说明。 若要设置信号保护，视频微型端口驱动程序的 [*COPPCommand*](./coppcommand.md) 函数接收指向 [**DXVA \_ COPPCommand**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppcommand) 结构的指针，并将 **GUIDCOMMANDID** 成员设置为 DXVA \_ COPPSetSignaling GUID，并将 **CommandData** 成员设置为指向 [**DXVA \_ COPPSetSignalingCmdData**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppsetsignalingcmddata) 结构的指针，该指针指定如何保护信号。

 

