---
title: COPP 命令
description: COPP 命令
keywords:
- 复制保护 WDK COPP，命令
- 视频复制保护 WDK COPP，命令
- COPP WDK DirectX VA，命令
- 受保护的视频 WDK COPP，命令
- 命令 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d43778c8e32c2f03e4af28a1f9c92996281952cd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824231"
---
# <a name="copp-commands"></a>COPP 命令


## <span id="ddk_copp_command_gg"></span><span id="DDK_COPP_COMMAND_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

视频微型端口驱动程序可以接收请求，以在与 DirectX VA COPP 设备关联的物理连接器上执行操作。 视频微型端口驱动程序的 [*COPPCommand*](./coppcommand.md) 函数将被传递到 [**DXVA \_ COPPCommand**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppcommand) 结构的指针，该结构指定要执行的操作。 DXVA COPPCommand 的 **guidCommandID** 和 **CommandData** 成员 \_ 指定操作。 支持以下操作：

-   [设置保护级别](setting-the-protection-level.md)

-   [指导如何保护信号](instructing-how-to-protect-the-signal.md)

 

