---
title: PnPUtil 返回值
description: PnPUtil 返回值
ms.date: 10/13/2020
ms.localizationpriority: medium
ms.openlocfilehash: 533759e8603550d830eaedf2f7c5cbd549de23ff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841023"
---
# <a name="pnputil-return-values"></a>PnPUtil 返回值


此页列出了 PnPUtil 工具返回的一些值。  有关其他可能值的信息，请参阅 [错误代码](/windows/win32/debug/system-error-codes)。

* `ERROR_SUCCESS` (0) ：请求的操作已成功完成。
* `ERROR_SUCCESS_REBOOT_REQUIRED` (3010) ：请求的操作已成功完成，需要重新启动系统。  例如，如果指定了  `/install /add-driver` 选项，则一个或多个设备已成功安装，需要重新启动系统才能完成安装。
* `ERROR_SUCCESS_REBOOT_INITIATED` (1641) ：操作成功，因为指定了选项，正在进行系统重启 `/reboot` 。

尽管仍可使用 PnPUtil 来批量安装驱动程序，但要获取可操作的返回值，我们建议 `/install /add-driver` 一次使用一个 INF 来指定。

下面是一些其他故障排除的最佳实践：

* 如果 `/add-driver` 指定了和 `/delete-driver` 选项，请查看 `%windir%\inf\setupapi.dev.log` 详细信息。

* 如果 `/enable-device` 指定了和 `/disable-device` 选项，请将 setupapi.log 日志详细级别设置为完全 (`0x2000ffff`) ，然后重试该操作。  如果再次失败，请查看 `%windir%\inf\setupapi.app.log` 详细信息。 有关详细级别的信息，请参阅 [设置 Setupapi.log 日志记录级别](../install/setting-setupapi-logging-levels.md)。
