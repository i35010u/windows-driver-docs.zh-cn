---
title: 关闭与筛选器引擎建立的会话
description: 关闭与筛选器引擎建立的会话
ms.assetid: e145fb8c-fe9f-4834-8df0-f2ceb5b13b09
keywords:
- Windows 筛选平台标注驱动程序 WDK，关闭会话
- 标注驱动程序 WDK Windows 筛选平台，关闭会话
- 筛选引擎 WDK Windows 筛选平台
- 关闭筛选器引擎会话 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7efde17cc8c0ca1242a0d8e98ce9eee9e7cdf255
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838196"
---
# <a name="closing-a-session-to-the-filter-engine"></a>关闭与筛选器引擎建立的会话


标注驱动程序执行所需的管理任务后，应关闭与筛选器引擎的会话。 标注驱动程序通过调用[**FwpmEngineClose0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpmk/nf-fwpmk-fwpmengineclose0)函数来实现此功能。 例如：

```C++
status =
 FwpmEngineClose0(
 engineHandle  // An handle to the open session
    );
```

 

 





