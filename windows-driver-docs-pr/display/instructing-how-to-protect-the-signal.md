---
title: 指导如何保护信号
description: 指导如何保护信号
ms.assetid: d55a3660-5b7c-43e9-b1c5-b61f8b997a1a
keywords:
- 复制保护 WDK COPP，信号保护
- 视频复制保护 WDK COPP，信号保护
- COPP WDK DirectX VA，信号保护
- 受保护的视频 WDK COPP，信号保护
- 信号保护 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4697f60565483f682f466a6a11bedc103f1c644f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840362"
---
# <a name="instructing-how-to-protect-the-signal"></a>指导如何保护信号


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

COPP 命令可提供有关如何保护通过与 DirectX VA COPP 设备关联的物理连接器的信号的说明。 若要设置信号保护，视频微型端口驱动程序的[*COPPCommand*](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)函数接收指向[**DXVA\_COPPCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppcommand)结构的指针，并将**guidCommandID**成员设置为 DXVA\_COPPSetSignaling GUID 和**将 CommandData**成员设置为指向[**DXVA\_COPPSetSignalingCmdData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppsetsignalingcmddata)结构的指针，该指针指定如何保护信号。

 

 





