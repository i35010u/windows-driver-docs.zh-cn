---
title: WIA Microdriver 命令
description: WIA Microdriver 命令
ms.assetid: 54d0c35b-d8b3-4e38-85cf-d5b4f80f6daa
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a9d7f58639a5025b1b0b91076a02884d5dac1d7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525954"
---
# <a name="wia-microdriver-commands"></a>WIA Microdriver 命令


## <span id="ddk_wia_microdriver_commands_si"></span><span id="DDK_WIA_MICRODRIVER_COMMANDS_SI"></span>


以下设置的常量窗体的 WIA microdriver 命令集。 从 WIA 平板驱动程序中的命令传递到 microdriver *lCommand*的参数[ **MicroEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff545248)函数。 命令分为以下类别：

-   [自动文档送纸器命令](automatic-document-feeder-commands.md)

    支持自动文档送纸器 (ADF) 的 microdrivers 的命令。

-   [事件命令](event-commands.md)

    Microdriver 事件支持的命令。

-   [所需的命令](required-commands.md)

    必须由 microdriver 实现的命令。

-   [可选的命令](optional-commands.md)

    可以由 microdriver 实现作为其基本操作的增强功能的命令。

这些命令中定义*Wiamicro.h*，并可在 Windows Me 和 Windows XP 及更高版本。

 

 





