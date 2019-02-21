---
title: 自定义的选项
description: 自定义的选项
ms.assetid: 8b54c59e-b469-488a-ae31-52045c00c971
keywords:
- 打印机选项 WDK Unidrv，自定义
- 自定义的打印机选项 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1caff8562f1b5e306908267500eb0e8fcc7e0a86
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547751"
---
# <a name="customized-options"></a>自定义的选项





自定义的选项在未定义的 GPD 语言中的预定义名称。 必须创建这些选项的唯一名称。

自定义的选项可以与自定义的功能相关联。 与自定义功能相关联的自定义选项的示例，请参阅[自定义功能](customized-features.md)。

此外可以指定自定义的选项的一些[标准功能](standard-features.md)。 例如，如果您的打印机提供未由的标准选项之一描述的纸张大小**PaperSize**功能，您可以通过创建选项的唯一名称来指定自定义的纸张大小选项。

自定义的选项名称中必须是唯一一项功能，但可以在不同的功能中重用的选项名称。 此外，可以使用自定义功能内的标准选项名称。 因此，例如，您可以使用标准选项名称 ON 和 OFF 内多个\*[功能](feature-entry-format.md)条目的自定义功能。

 

 




