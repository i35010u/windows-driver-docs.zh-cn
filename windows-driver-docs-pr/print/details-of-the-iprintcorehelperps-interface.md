---
title: IPrintCoreHelperPS 接口详细信息
description: IPrintCoreHelperPS 接口详细信息
ms.assetid: 0e00012c-6ced-4369-b367-675465e29d93
keywords:
- IPrintCoreHelperPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18b4bea3e7f34b7fd840b7b81e675f0a692d8af5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382060"
---
# <a name="details-of-the-iprintcorehelperps-interface"></a>IPrintCoreHelperPS 接口详细信息


Pscript5 不具有等效于 GDL 分析器，因此对于 Pscript5 驱动程序，提供了其他方法来读取 PPD 文件中显示的数据。 除了所有基方法**IPrintCoreHelper**接口， **IPrintCoreHelperPS**接口包含以下方法，提供对 PPD 文件中的数据的访问：

-   [**IPrintCoreHelperPS::GetFeatureAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcorehelperps-getfeatureattribute)

-   [**IPrintCoreHelperPS::GetGlobalAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcorehelperps-getglobalattribute)

-   [**IPrintCoreHelperPS::GetOptionAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcorehelperps-getoptionattribute)

因为 PPD 信息不依赖于配置中，不需要提供输入[ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)对这些方法的参数。

 

 




