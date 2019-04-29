---
title: '[Version] 部分指令'
description: 本主题介绍中 INF [Version] 部分指令。
ms.assetid: 76AC10DC-AECC-4C35-8BEE-4B2E8B06FEE0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e472b66ca51893a81e181c97fde57322f4960594
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391287"
---
# <a name="version-section-directives"></a>\[版本\]部分指令


本主题介绍*\[版本\]* 部分 INF 中的指令。

收件箱的所有驱动程序不能引用 Layout.inf 文件。

收件箱的所有驱动程序不能引用任何目录文件。

例如：

``` syntax
[Version]
Signature="$Windows NT$"
Provider=%MSFT%
ClassGUID={4D36E968-E325-11CE-BFC1-08002BE10318}
Class=Display
DriverVer=11/22/2004, 6.14.10.7000

Note: 
no line item for LayoutFile=layout.inf
no line item for CatalogFile=delta.cat
```

WHQL 显示器驱动程序不能引用 Layout.inf 文件。

例如：

``` syntax
[Version]
Signature="$Windows NT$"
Provider=%IHV%
ClassGUID={4D36E968-E325-11CE-BFC1-08002BE10318}
Class=Display
DriverVer=11/22/2004, 6.14.10.7000

Note: 
no line item for LayoutFile=layout.inf
```

 

 





