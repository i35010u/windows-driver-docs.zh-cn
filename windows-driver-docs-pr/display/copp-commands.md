---
title: COPP 命令
description: COPP 命令
ms.assetid: c745b7d9-be59-45f9-90f5-0a7ecef0a292
keywords:
- 复制保护 WDK COPP，命令
- 视频复制保护 WDK COPP，命令
- COPP WDK DirectX va，因此命令
- 受保护视频 WDK COPP 命令
- WDK COPP 命令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99c3c8cda0b7ad789e0115d1237ad4780e3a3484
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370272"
---
# <a name="copp-commands"></a>COPP 命令


## <span id="ddk_copp_command_gg"></span><span id="DDK_COPP_COMMAND_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。

微型端口驱动程序可以接收的请求与 DirectX VA COPP 设备相关联的物理连接器上执行操作。 微型端口驱动程序[ *COPPCommand* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)函数传递一个指向[ **DXVA\_COPPCommand** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppcommand)结构指定要执行的操作。 **GuidCommandID**并**CommandData** DXVA 成员\_COPPCommand 指定该操作。 支持以下操作：

-   [设置保护级别](setting-the-protection-level.md)

-   [指示如何保护信号](instructing-how-to-protect-the-signal.md)

 

 





