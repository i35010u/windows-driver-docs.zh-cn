---
title: IPrintCoreHelperPS 接口详细信息
description: IPrintCoreHelperPS 接口详细信息
keywords:
- IPrintCoreHelperPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08f7ac8cef5e51542abcde65510343b32bb3d8da
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797275"
---
# <a name="details-of-the-iprintcorehelperps-interface"></a>IPrintCoreHelperPS 接口详细信息


Pscript5 没有等效于 GDL 分析器，因此对于 Pscript5 驱动程序，提供了其他方法来读取 PPD 文件中显示的数据。 除了基 **IPrintCoreHelper** 接口的所有方法， **IPrintCoreHelperPS** 接口还包含以下方法，这些方法提供对 PPD 文件中数据的访问权限：

-   [**IPrintCoreHelperPS::GetFeatureAttribute**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcorehelperps-getfeatureattribute)

-   [**IPrintCoreHelperPS::GetGlobalAttribute**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcorehelperps-getglobalattribute)

-   [**IPrintCoreHelperPS::GetOptionAttribute**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcorehelperps-getoptionattribute)

由于 PPD 信息不依赖于配置，因此不需要向这些方法提供输入 [**DEVMODEW**](/windows/win32/api/wingdi/ns-wingdi-devmodew) 参数。

 

