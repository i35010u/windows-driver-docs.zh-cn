---
title: 在 CDB 中配置异常和事件
description: 可以将 CDB 配置为以特定方式响应指定的异常和事件。 对于每个异常，可以设置中断状态和处理状态。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99635a40d4990dd70228d2e5e3495707a02a11be
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821599"
---
# <a name="configuring-exceptions-and-events-in-cdb"></a>在 CDB 中配置异常和事件


可以将 CDB 配置为以特定方式响应指定的异常和事件。 对于每个异常，可以设置中断状态和处理状态。 对于每个事件，可以设置中断状态。

可以通过执行下列操作之一来配置中断状态或处理状态：

-   使用 [**SXE**](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)、 **SXD**、 **SXN** 或 **SXI** 命令。

-   使用 [**CDB 命令行**](cdb-command-line-options.md)上的 **-x**、 **-xe**、 **-xd**、 **-xn** 或 **-xi** 选项。
-   在 Tools.ini 文件中使用 **sxe** 或 **sxd** 关键字。

有关异常和事件的详细讨论，请参阅 [控制异常和事件](controlling-exceptions-and-events.md)。

 

 





