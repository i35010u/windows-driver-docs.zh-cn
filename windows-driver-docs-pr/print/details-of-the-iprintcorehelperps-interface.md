---
title: IPrintCoreHelperPS 接口的详细信息
description: IPrintCoreHelperPS 接口的详细信息
ms.assetid: 0e00012c-6ced-4369-b367-675465e29d93
keywords:
- IPrintCoreHelperPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a89d865c49e23ed8645a572342476606a17c1bed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547760"
---
# <a name="details-of-the-iprintcorehelperps-interface"></a>IPrintCoreHelperPS 接口的详细信息


Pscript5 不具有等效于 GDL 分析器，因此对于 Pscript5 驱动程序，提供了其他方法来读取 PPD 文件中显示的数据。 除了所有基方法**IPrintCoreHelper**接口， **IPrintCoreHelperPS**接口包含以下方法，提供对 PPD 文件中的数据的访问：

-   [**IPrintCoreHelperPS::GetFeatureAttribute**](https://msdn.microsoft.com/library/windows/hardware/ff551998)

-   [**IPrintCoreHelperPS::GetGlobalAttribute**](https://msdn.microsoft.com/library/windows/hardware/ff552899)

-   [**IPrintCoreHelperPS::GetOptionAttribute**](https://msdn.microsoft.com/library/windows/hardware/ff552903)

因为 PPD 信息不依赖于配置中，不需要提供输入[ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)对这些方法的参数。

 

 




