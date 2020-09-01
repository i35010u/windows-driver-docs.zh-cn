---
title: IPrintCoreHelperPS 接口详细信息
description: IPrintCoreHelperPS 接口详细信息
ms.assetid: 0e00012c-6ced-4369-b367-675465e29d93
keywords:
- IPrintCoreHelperPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60c1978a253008a46bbf75729d1a2030719adda4
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216374"
---
# <a name="details-of-the-iprintcorehelperps-interface"></a>IPrintCoreHelperPS 接口详细信息


Pscript5 没有等效于 GDL 分析器，因此对于 Pscript5 驱动程序，提供了其他方法来读取 PPD 文件中显示的数据。 除了基 **IPrintCoreHelper** 接口的所有方法， **IPrintCoreHelperPS** 接口还包含以下方法，这些方法提供对 PPD 文件中数据的访问权限：

-   [**IPrintCoreHelperPS::GetFeatureAttribute**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcorehelperps-getfeatureattribute)

-   [**IPrintCoreHelperPS::GetGlobalAttribute**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcorehelperps-getglobalattribute)

-   [**IPrintCoreHelperPS::GetOptionAttribute**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcorehelperps-getoptionattribute)

由于 PPD 信息不依赖于配置，因此不需要向这些方法提供输入 [**DEVMODEW**](/windows/win32/api/wingdi/ns-wingdi-devmodew) 参数。

 

