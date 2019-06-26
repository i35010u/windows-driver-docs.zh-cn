---
title: IHV 驱动程序中的自动配置
description: IHV 驱动程序中的自动配置
ms.assetid: 81febae0-6fab-4226-9e98-7705d606caf4
keywords:
- IHV 驱动程序自动配置 WDK 打印机
- 自动配置 WDK 打印机，IHV 驱动程序
- 打印机自动配置 WDK 打印机，IHV 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 718f7f1a1857e7e59f4cc219498e2debc993c79a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370471"
---
# <a name="autoconfiguration-in-an-ihv-driver"></a>IHV 驱动程序中的自动配置


支持自动配置的独立 IHV 驱动程序必须满足以下要求：

1.  请按照 Microsoft [bidi 通信架构](https://docs.microsoft.com/windows-hardware/drivers/print/bidi-communications-schema-reference)并[bidi 通信接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_print/index)Windows SDK 文档中所述。

2.  支持打印机\_事件\_配置\_中的更新打印机事件[ **DrvPrinterEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvprinterevent)函数。

3.  请注意 bidi 通知架构了解接收的通知的功能。 请参阅[Bidi 通信架构](bidirectional-communication-schema.md)。

**请注意**  不需要创建一个独立的驱动程序，以自动配置为提供支持。 相反，可以编写类驱动程序充分利用 Microsoft 打印机之一的 GPD 或 PPD 文件。 有关详细信息，请参阅[自动配置的现成支持](in-box-support-for-autoconfiguration.md)。

 

 

 




