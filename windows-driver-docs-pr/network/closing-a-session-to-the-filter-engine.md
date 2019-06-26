---
title: 关闭与筛选器引擎建立的会话
description: 关闭与筛选器引擎建立的会话
ms.assetid: e145fb8c-fe9f-4834-8df0-f2ceb5b13b09
keywords:
- Windows 筛选平台标注驱动程序 WDK、 关闭会话
- 标注驱动程序 WDK Windows 筛选平台，关闭会话
- 筛选器引擎 WDK Windows 筛选平台
- 关闭筛选引擎会话 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff129f1a737643dc3ee0cc8e2eeb286680aa4835
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384215"
---
# <a name="closing-a-session-to-the-filter-engine"></a>关闭与筛选器引擎建立的会话


标注驱动程序执行所需的管理任务后，它应关闭筛选器引擎的会话。 标注驱动程序将这是通过调用[ **FwpmEngineClose0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpmk/nf-fwpmk-fwpmengineclose0)函数。 例如：

```C++
status =
 FwpmEngineClose0(
 engineHandle  // An handle to the open session
    );
```

 

 





