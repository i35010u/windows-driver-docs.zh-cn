---
title: WIA 微驱动程序命令
description: WIA 微驱动程序命令
ms.assetid: 54d0c35b-d8b3-4e38-85cf-d5b4f80f6daa
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65e2fd837e715ad944eeb8cff9a8f62e4882d0e6
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192581"
---
# <a name="wia-microdriver-commands"></a>WIA 微驱动程序命令


## <span id="ddk_wia_microdriver_commands_si"></span><span id="DDK_WIA_MICRODRIVER_COMMANDS_SI"></span>


以下常量集构成了 WIA microdriver 命令集。 命令将从[**MicroEntry**](/windows-hardware/drivers/ddi/wiamicro/nf-wiamicro-microentry)函数的*lCommand*参数中的 WIA 平板驱动程序传递到 microdriver。 这些命令分为以下几类：

-   [自动文档送纸器命令](automatic-document-feeder-commands.md)

    支持自动文档送纸器 (ADF) 的 microdrivers 命令。

-   [事件命令](event-commands.md)

    Microdriver 事件支持的命令。

-   [必需命令](required-commands.md)

    必须由 microdriver 实现的命令。

-   [可选命令](optional-commands.md)

    可由 microdriver 实现的命令，作为其基本操作的增强功能。

这些命令在 *Wiamicro*中定义，在 windows Me 和 windows XP 及更高版本中可用。

 

