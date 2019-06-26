---
title: WIA 微驱动程序命令
description: WIA 微驱动程序命令
ms.assetid: 54d0c35b-d8b3-4e38-85cf-d5b4f80f6daa
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 857678af1b7c9142d525718bfe851008dc5b6ac1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355200"
---
# <a name="wia-microdriver-commands"></a>WIA 微驱动程序命令


## <span id="ddk_wia_microdriver_commands_si"></span><span id="DDK_WIA_MICRODRIVER_COMMANDS_SI"></span>


以下设置的常量窗体的 WIA microdriver 命令集。 从 WIA 平板驱动程序中的命令传递到 microdriver *lCommand*的参数[ **MicroEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamicro/nf-wiamicro-microentry)函数。 命令分为以下类别：

-   [自动文档送纸器命令](automatic-document-feeder-commands.md)

    支持自动文档送纸器 (ADF) 的 microdrivers 的命令。

-   [事件命令](event-commands.md)

    Microdriver 事件支持的命令。

-   [所需的命令](required-commands.md)

    必须由 microdriver 实现的命令。

-   [可选的命令](optional-commands.md)

    可以由 microdriver 实现作为其基本操作的增强功能的命令。

这些命令中定义*Wiamicro.h*，并可在 Windows Me 和 Windows XP 及更高版本。

 

 





