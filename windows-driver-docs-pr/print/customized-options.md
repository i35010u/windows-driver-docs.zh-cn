---
title: 自定义选项
description: 自定义选项
keywords:
- 打印机选项 WDK Unidrv，自定义
- 自定义打印机选项 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49b009116d9f02af5670d68b7bfe8127052a1a23
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797389"
---
# <a name="customized-options"></a>自定义选项





自定义选项是指不是由 GPD 语言的预定义名称定义的选项。 您必须为这些选项创建唯一名称。

自定义选项可以与自定义的功能相关联。 有关与自定义功能关联的自定义选项的示例，请参阅 [自定义功能](customized-features.md)。

还可以为某些 [标准功能](standard-features.md)指定自定义选项。 例如，如果您的打印机提供的纸张大小不是 **PaperSize** 功能的标准选项之一所描述的，则可以通过创建选项的唯一名称来指定自定义的纸张大小选项。

自定义选项名称在功能中必须是唯一的，但选项名称可在不同的功能中重复使用。 此外，还可以在自定义功能中使用标准选项名称。 例如，可以在多个 \* [功能](feature-entry-format.md)条目中为自定义功能使用标准选项名称。

 

 




