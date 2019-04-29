---
title: 通过监视窗口控制变量
description: 通过监视窗口控制变量
ms.assetid: bd857442-fbd7-4c00-9743-6077d38ee38e
keywords:
- 监视窗口中，全局变量
- 监视窗口中，本地变量
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9fd952b95525585095a9008dcdfef5c5ca7c6a92
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375041"
---
# <a name="controlling-variables-through-the-watch-window"></a>通过监视窗口控制变量


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


在 WinDbg 中，您还可以使用监视窗口可显示和更改全局和本地变量。

监视窗口可以显示任何所需的变量的列表。 这些变量可以包含全局变量和局部变量从任何函数。 在任何时候，监视窗口显示与当前函数的作用域匹配这些变量的值。 此外可以更改通过监视窗口的这些变量的值。

与局部变量窗口中，监视窗口不受对本地上下文的更改。 当前的程序计数器的作用域中定义的变量可以具有其值显示或修改。

 

 





