---
title: V4 打印机驱动程序渲染
description: 用于呈现打印作业打印设备的页面描述语言到，v4 打印驱动程序模型使用 XPSDrv 呈现模块。
ms.assetid: 8952063C-3706-43A0-BA6B-231E7CD01514
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fa8369d625a1c5e0ce9633243507b984a819c4c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358675"
---
# <a name="v4-printer-driver-rendering"></a>V4 打印机驱动程序渲染


用于呈现打印作业打印设备的页面描述语言到，v4 打印驱动程序模型使用[XPSDrv 呈现模块](xpsdrv-render-module.md)。

V4 驱动程序模型不用于任何其他目的使用 XPSDrv 呈现器模块。 因此 XPS 直接设备的驱动程序不需要包括任何筛选器。 但对于所有其他设备的驱动程序也必须包括筛选器的呈现到设备 PDL，或者它们必须通过使用现有的呈现支持打印类驱动程序从**RequiredClass**指令 v4 清单文件中。

本部分提供有关以下主题中的 v4 驱动程序呈现的详细信息。

[V4 打印机驱动程序呈现体系结构](v4-driver-rendering-architecture.md)

[XPSDrv 中的改进](improvements-in-xpsdrv.md)

[标准 XPS 筛选器](standard-xps-filters.md)

[V4 打印类驱动程序呈现](print-class-driver-rendering.md)

## <a name="related-topics"></a>相关主题
[支持的 PrintTicket 功能](supported-printticket-features.md)  
[V4 打印机驱动程序](v4-printer-driver.md)  
[XPSDrv 呈现器模块](xpsdrv-render-module.md)  



