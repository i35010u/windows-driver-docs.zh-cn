---
title: IPrintCoreHelperPS 接口详细信息
description: IPrintCoreHelperPS 接口详细信息
ms.assetid: 0e00012c-6ced-4369-b367-675465e29d93
keywords:
- IPrintCoreHelperPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2684a9bdb0f5bdb9f8e989eb172fedf02a85f203
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802779"
---
# <a name="details-of-the-iprintcorehelperps-interface"></a>IPrintCoreHelperPS 接口详细信息


Pscript5 没有等效于 GDL 分析器，因此对于 Pscript5 驱动程序，提供了其他方法来读取 PPD 文件中显示的数据。 除了基 **IPrintCoreHelper** 接口的所有方法， **IPrintCoreHelperPS** 接口还包含以下方法，这些方法提供对 PPD 文件中数据的访问权限：

-   [**IPrintCoreHelperPS::GetFeatureAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcorehelperps-getfeatureattribute)

-   [**IPrintCoreHelperPS::GetGlobalAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcorehelperps-getglobalattribute)

-   [**IPrintCoreHelperPS::GetOptionAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcorehelperps-getoptionattribute)

由于 PPD 信息不依赖于配置，因此不需要向这些方法提供输入 [**DEVMODEW**](https://docs.microsoft.com/windows/win32/api/wingdi/ns-wingdi-devmodew) 参数。

 

 




