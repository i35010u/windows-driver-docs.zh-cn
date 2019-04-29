---
title: C28145
description: 警告的 C28145 不透明 MDL 结构不应修改由驱动程序。
ms.assetid: efbd667b-fb0e-4a4d-bb6a-e8249c113a91
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28145
ms.openlocfilehash: ba336ed8a7c353fa107cd4378f3f5eb917049005
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361527"
---
# <a name="c28145"></a>C28145


警告 C28145:不透明 MDL 结构不应修改由驱动程序

驱动程序代码正在改变 MDL 结构的成员。

**MdlFlags**字段用于所有 MDL 字段用作代理。 应修改任何字段除外 MDL\_映射\_可以\_会失败，用于需要 Microsoft Windows 98 或 Windows NT (SP4) 兼容的驱动程序，因此 MDL\_页\_锁定，这用于需要 Windows 2000 兼容的驱动程序。

 

 





