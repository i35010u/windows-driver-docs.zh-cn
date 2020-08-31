---
title: 设置 Copy-File 标志以支持 PnP 停止
description: 设置 Copy-File 标志以支持 PnP 停止
ms.assetid: 9f716ac0-c181-489f-8bc4-ccca8c141b06
keywords:
- INF 文件 WDK 显示，复制文件标志
- 复制文件标志 WDK 显示
- PnP 停止 WDK 显示
- 即插即用停止 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c2cb8c58934bc1b3e71388922d533ae8dfc6919
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066659"
---
# <a name="setting-a-copy-file-flag-to-support-pnp-stop"></a>设置 Copy-File 标志以支持 PnP 停止


向 Windows 显示驱动程序模型写入 Windows 显示驱动程序模型的显示驱动程序需要新的复制文件标志 (WDDM) 以便正确支持即插即用 (PnP) 停止 (即无需重新启动系统的驱动程序升级) 。

**注意**   此标志仅适用于用户模式显示驱动程序二进制文件，而不适用于显示小型端口驱动程序。

 

下面的示例演示了新的复制文件标志，该标志仅添加到用户模式显示驱动程序的复制文件部分，而不显示微型端口驱动程序：

```cpp
;
; File sections
;

[r200.Miniport]
r200.sys

[r200.Display]
r200umd.dll,,,0x00004000  ; COPYFLG_IN_USE_TRY_RENAME
r200umd2.dll,,,0x00004000 ; COPYFLG_IN_USE_TRY_RENAME
```

有关与**CopyFiles**关联的**CopyFiles**指令和文件部分的详细信息，请参阅[**INF CopyFiles 指令**](../install/inf-copyfiles-directive.md)。

 

