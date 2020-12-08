---
title: 通过监视窗口控制变量
description: 通过监视窗口控制变量
keywords:
- 监视窗口，全局变量
- 监视窗口，本地变量
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ccf7f1d4c808b1c1f371a87f0366b668c69da881
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838665"
---
# <a name="controlling-variables-through-the-watch-window"></a>通过监视窗口控制变量


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


在 WinDbg 中，还可以使用监视窗口显示和更改全局变量和局部变量。

监视窗口可以显示所需的任何变量列表。 这些变量可以包含来自任何函数的全局变量和局部变量。 在任何时候，监视窗口都将显示与当前函数的作用域匹配的那些变量的值。 还可以通过监视窗口更改这些变量的值。

与 "局部变量" 窗口不同，监视窗口不受本地上下文更改的影响。 只有在当前程序计数器的作用域中定义的那些变量才能显示或修改其值。

 

 





