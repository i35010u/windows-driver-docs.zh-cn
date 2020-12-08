---
title: IPrintCoreHelper 接口详细信息
description: IPrintCoreHelper 接口详细信息
keywords:
- IPrintCoreHelper
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31a208f2e293c6edb5f417c103dcc1b6a5aa86a7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797281"
---
# <a name="details-of-the-iprintcorehelper-interface"></a>IPrintCoreHelper 接口详细信息


**IPrintCoreHelper** 接口大致基于 Pscript5 UI 替换接口。 不过， **IPrintCoreHelper** 接口在本质上不同于原始 Pscript5 helper 接口。

-   **IPrintCoreHelper** 接口没有 **QuerySimulatedCapabilities** 方法。 相反， **IPrintCoreHelper** 接口以明确定义且可识别的方式将模拟功能映射到功能和选项的常规列表。

-   在 **IPrintCoreHelper** 接口中，要求调用方传入 [**DEVMODEW**](/windows/win32/api/wingdi/ns-wingdi-devmodew) 结构而不是 [**OEMUIOBJ**](/windows-hardware/drivers/ddi/printoem/ns-printoem-_oemuiobj) 结构。

如果使用 **IPrintCoreHelper** 接口或从它继承的接口，应考虑以下几点：

-   对于 **IPrintCoreHelper** 接口，用于 **GetOption** 或 **SETOPTIONS** 方法的字符串是 GPD 字符串，而不是 GDL 字符串，因此，在 ifdef GDL 块中定义的特性和选项对于 \# helper 接口方法不可用。

-   如果 **IPrintCoreHelper** 接口上的方法 (及其 subinterfaces) 具有 OUT 参数，并且如果该方法失败，out 参数将保留调用方法时的值。

-   **IPrintCoreHelper** 接口的内存模型与以前的 Pscript5 接口的内存模型略有不同。 调用方不负责清理从 helper 接口传递回的参数，并且调用方无需分配要传入的缓冲区。 核心驱动程序处理这些类型的内存管理。

本部分提供下列主题：

[IPrintCoreHelperUni 接口详细信息](details-of-the-iprintcorehelperuni-interface.md)

[IPrintCoreHelperPS 接口详细信息](details-of-the-iprintcorehelperps-interface.md)

 

