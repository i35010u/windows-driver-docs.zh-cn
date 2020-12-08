---
title: '[版本] 部分指令'
description: 本主题介绍 INF 中的 [Version] 节指令。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0839b8895bcddf2b8caeda79a16833aa3d77356
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810593"
---
# <a name="version-section-directives"></a>\[版本 \] 部分指令


本主题介绍 INF 中的 *\[ 版本 \]* 节指令。

所有收件箱驱动程序不得引用布局 .inf 文件。

所有收件箱驱动程序不得引用任何编录文件。

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

WHQL 显示驱动程序不得引用布局 .inf 文件。

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

 

 





