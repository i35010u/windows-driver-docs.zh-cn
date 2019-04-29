---
title: 设置 Copy-File 标志以支持 PnP 停止
description: 设置 Copy-File 标志以支持 PnP 停止
ms.assetid: 9f716ac0-c181-489f-8bc4-ccca8c141b06
keywords:
- INF 文件 WDK 显示中，复制文件标志
- 复制文件标志 WDK 显示
- 即插即用停止 WDK 显示
- 插停止 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd7d9995e934a29dfe3a7078bdac289963a91d74
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390469"
---
# <a name="setting-a-copy-file-flag-to-support-pnp-stop"></a>设置 Copy-File 标志以支持 PnP 停止


新的复制文件标志是为了正确支持插即用 (PnP) 停止 （即，不需要系统重新启动的驱动程序升级） 写入到 Windows 显示驱动程序模型 (WDDM) 的显示器驱动程序的必需的。

**请注意**  此标志是仅用于用户模式显示驱动程序二进制文件而不用于显示微型端口驱动程序必需的。

 

下面的示例显示了只需复制文件部分，了解用户模式下添加的新复制文件标志显示驱动程序并不会显示微型端口驱动程序：

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

有关详细信息**CopyFiles**与关联的指令和文件部分**CopyFiles**，请参阅[ **INF CopyFiles 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546346).

 

 





