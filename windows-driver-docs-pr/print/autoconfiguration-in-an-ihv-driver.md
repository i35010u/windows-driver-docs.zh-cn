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
ms.openlocfilehash: 0503b4b823536212b94a0814ad78e07ca0944948
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842837"
---
# <a name="autoconfiguration-in-an-ihv-driver"></a>IHV 驱动程序中的自动配置


支持自动配置的独立 IHV 驱动程序必须满足以下要求：

1.  遵循 Microsoft[双向通信架构](https://docs.microsoft.com/windows-hardware/drivers/print/bidi-communications-schema-reference)和 Windows SDK 文档中所述的[双向通信接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)。

2.  支持打印机\_事件\_CONFIGURATION\_更新[**DrvPrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent)函数中的打印机事件。

3.  请注意，双向通知架构能够理解收到的通知。 请参阅[双向通信架构](bidirectional-communication-schema.md)。

**请注意**  不必创建独立驱动程序即可为自动配置提供支持。 您可以改为编写利用 Microsoft 打印机类驱动程序之一的 GPD 或 PPD 文件。 有关详细信息，请参阅[自动配置的内置支持](in-box-support-for-autoconfiguration.md)。

 

 

 




