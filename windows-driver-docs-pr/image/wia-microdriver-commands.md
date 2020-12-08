---
title: WIA 微驱动程序命令
description: WIA 微驱动程序命令
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 496a6a4380675e8dae4a3a9251a643ceb8565599
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826487"
---
# <a name="wia-microdriver-commands"></a>WIA 微驱动程序命令


## <span id="ddk_wia_microdriver_commands_si"></span><span id="DDK_WIA_MICRODRIVER_COMMANDS_SI"></span>


以下常量集构成了 WIA microdriver 命令集。 命令将从 [**MicroEntry**](/windows-hardware/drivers/ddi/wiamicro/nf-wiamicro-microentry)函数的 *lCommand* 参数中的 WIA 平板驱动程序传递到 microdriver。 这些命令分为以下几类：

-   [自动文档送纸器命令](automatic-document-feeder-commands.md)

    支持自动文档送纸器 (ADF) 的 microdrivers 命令。

-   [事件命令](event-commands.md)

    Microdriver 事件支持的命令。

-   [必需命令](required-commands.md)

    必须由 microdriver 实现的命令。

-   [可选命令](optional-commands.md)

    可由 microdriver 实现的命令，作为其基本操作的增强功能。

这些命令在 *Wiamicro* 中定义，在 windows Me 和 windows XP 及更高版本中可用。

 

