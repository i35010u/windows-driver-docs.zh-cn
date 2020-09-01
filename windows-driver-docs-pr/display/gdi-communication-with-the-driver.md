---
title: GDI 与驱动程序的通信
description: GDI 与驱动程序的通信
ms.assetid: 81d9e87f-883b-4019-86fc-bccde861de46
keywords:
- GDI WDK Windows 2000 显示器，驱动程序通信
- 图形驱动程序 WDK Windows 2000 显示器、驱动程序通信
- 绘制 WDK GDI，驱动程序通信
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15b492cc2f595611974490c56ddfde0c52b2e56c
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065846"
---
# <a name="gdi-communication-with-the-driver"></a>GDI 与驱动程序的通信


## <span id="ddk_gdi_communication_with_the_driver_gg"></span><span id="DDK_GDI_COMMUNICATION_WITH_THE_DRIVER_GG"></span>


驱动程序仅将一个函数导出到 GDI： [**DrvEnableDriver**](/windows/desktop/api/winddi/nf-winddi-drvenabledriver)。 所有其他支持驱动程序的函数（包括 [**DrvDisableDriver**](/windows/desktop/api/winddi/nf-winddi-drvdisabledriver) 函数）通过指针数组向 GDI 公开。 对 **DrvEnableDriver** 的 GDI 调用将初始化驱动程序并传递回驱动程序支持的图形 DDI 函数的列表。 虽然驱动程序必须支持一些函数，但 GDI 将处理从驱动程序的 **DrvEnableDriver** 例程收到的函数列表中不包含的操作。 当驱动程序要卸载时，GDI 将调用 *DrvDisableDriver* 。 有关图形 DDI 函数的详细讨论，请参见 [使用图形 ddi](using-the-graphics-ddi.md)。

GDI 使大量的对象和服务可供驱动程序使用。 它们分为两类：用户对象和服务例程。

 

