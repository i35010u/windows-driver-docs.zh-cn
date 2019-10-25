---
title: IPrintCoreHelper 接口详细信息
description: IPrintCoreHelper 接口详细信息
ms.assetid: df736ca2-425e-4fc8-bdcb-bdbd5caa3e22
keywords:
- IPrintCoreHelper
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85e5ab345d54c806c29a016bfb1a6e41c4c7a7f2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829019"
---
# <a name="details-of-the-iprintcorehelper-interface"></a>IPrintCoreHelper 接口详细信息


**IPrintCoreHelper**接口大致基于 Pscript5 UI 替换接口。 不过， **IPrintCoreHelper**接口在本质上不同于原始 Pscript5 helper 接口。

-   **IPrintCoreHelper**接口没有**QuerySimulatedCapabilities**方法。 相反， **IPrintCoreHelper**接口以明确定义且可识别的方式将模拟功能映射到功能和选项的常规列表。

-   在**IPrintCoreHelper**接口中，要求调用方传入[**DEVMODEW**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)结构而不是[**OEMUIOBJ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/ns-printoem-_oemuiobj)结构。

如果使用**IPrintCoreHelper**接口或从它继承的接口，应考虑以下几点：

-   对于**IPrintCoreHelper**接口，用于**GetOption**或**SETOPTIONS**方法的字符串是 GPD 字符串，而不是 GDL 字符串，因此 \#ifdef GDL 块中定义的功能和选项不可用于helper 接口方法。

-   如果**IPrintCoreHelper**接口（及其 subinterfaces）上的方法具有 OUT 参数，并且如果该方法失败，OUT 参数将保留调用方法时的值。

-   **IPrintCoreHelper**接口的内存模型与以前的 Pscript5 接口的内存模型略有不同。 调用方不负责清理从 helper 接口传递回的参数，并且调用方无需分配要传入的缓冲区。 核心驱动程序处理这些类型的内存管理。

本部分提供下列主题：

[IPrintCoreHelperUni 接口的详细信息](details-of-the-iprintcorehelperuni-interface.md)

[IPrintCoreHelperPS 接口的详细信息](details-of-the-iprintcorehelperps-interface.md)

 

 




