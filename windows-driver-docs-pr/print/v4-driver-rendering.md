---
title: V4 打印机驱动程序渲染
description: 若要将打印作业呈现到打印设备的页面描述语言中，v4 打印驱动程序模型使用 XPSDrv Render 模块。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cad50a0135e407fe7ad02a18bb7b44b76274d6b7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785911"
---
# <a name="v4-printer-driver-rendering"></a>V4 打印机驱动程序渲染


若要将打印作业呈现到打印设备的页面描述语言中，v4 打印驱动程序模型使用 [XPSDrv Render 模块](xpsdrv-render-module.md)。

V4 驱动程序模型不会将 XPSDrv render 模块用于任何其他目的。 因此，适用于 XPS 直通设备的驱动程序不必包含任何筛选器。 但所有其他设备的驱动程序都必须包括呈现到设备 PDL 中的筛选器，或者必须通过使用 v4 清单文件中的 **RequiredClass** 指令来利用打印类驱动程序中的现有呈现支持。

本部分提供有关以下主题中的 v4 驱动程序呈现功能的详细信息。

[V4 打印机驱动程序渲染体系结构](v4-driver-rendering-architecture.md)

[XPSDrv 的改进](improvements-in-xpsdrv.md)

[标准 XPS 筛选器](standard-xps-filters.md)

[V4 打印类驱动程序渲染](print-class-driver-rendering.md)

## <a name="related-topics"></a>相关主题
[支持的 PrintTicket 功能](supported-printticket-features.md)  
[V4 打印机驱动程序](v4-printer-driver.md)  
[XPSDrv 渲染器模块](xpsdrv-render-module.md)  



