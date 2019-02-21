---
title: 在 CDB 中配置异常和事件
description: 你可以配置 CDB 来以特定方式对指定的异常和事件做出反应。 对于每个异常，可以设置中断状态和处理状态。
ms.assetid: EA23057E-3241-43F2-84D3-CA5E56721583
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: db7a65d06bbb9f425a3d1bf3f19d0b219703766e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533159"
---
# <a name="configuring-exceptions-and-events-in-cdb"></a>在 CDB 中配置异常和事件


你可以配置 CDB 来以特定方式对指定的异常和事件做出反应。 对于每个异常，可以设置中断状态和处理状态。 对于每个事件，可以设置中断状态。

可以通过执行下列任一配置中断状态或处理状态：

-   使用[ **SXE**](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)， **SXD**， **SXN**，或**SXI**命令。

-   使用 **-x**， **-xe**， **-xd**， **-xn**，或 **-xi**选项[ **CDB 命令行**](cdb-command-line-options.md)。
-   使用**sxe**或**sxd** Tools.ini 文件中的关键字。

有关异常和事件的详细讨论，请参阅[控制异常和事件](controlling-exceptions-and-events.md)。

 

 





