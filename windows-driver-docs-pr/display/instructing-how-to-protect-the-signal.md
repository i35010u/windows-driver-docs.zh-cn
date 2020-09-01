---
title: 指示如何保护信号
description: 指示如何保护信号
ms.assetid: d55a3660-5b7c-43e9-b1c5-b61f8b997a1a
keywords:
- 复制保护 WDK COPP，信号保护
- 视频复制保护 WDK COPP，信号保护
- COPP WDK DirectX VA，信号保护
- 受保护的视频 WDK COPP，信号保护
- 信号保护 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d15252a80a5282f616b6e195d8b1ddb414fae34
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066042"
---
# <a name="instructing-how-to-protect-the-signal"></a>指示如何保护信号


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

COPP 命令可提供有关如何保护通过与 DirectX VA COPP 设备关联的物理连接器的信号的说明。 若要设置信号保护，视频微型端口驱动程序的 [*COPPCommand*](./coppcommand.md) 函数接收指向 [**DXVA \_ COPPCommand**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppcommand) 结构的指针，并将 **GUIDCOMMANDID** 成员设置为 DXVA \_ COPPSetSignaling GUID，并将 **CommandData** 成员设置为指向 [**DXVA \_ COPPSetSignalingCmdData**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppsetsignalingcmddata) 结构的指针，该指针指定如何保护信号。

 

