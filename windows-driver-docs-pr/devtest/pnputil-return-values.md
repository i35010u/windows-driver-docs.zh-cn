---
title: PnPUtil 返回值
description: PnPUtil 返回值
ms.assetid: c26ecf54-b3d4-4559-9ec1-ff535cf03d77
ms.date: 02/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0cdc4b82841cc2726edc438e548afc3feb5d27cd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345803"
---
# <a name="pnputil-return-values"></a>PnPUtil 返回值


下表包括一些更常见 PnPUtil 工具将返回的值：

* `ERROR_SUCCESS` (0):请求的操作已成功完成。
* `ERROR_SUCCESS_REBOOT_REQUIRED` (3010):请求的操作已成功完成且系统重新启动是必需的。  例如，如果`/install /add-driver`未指定选项，已成功安装一个或多个设备，需要的系统重启以完成安装。
* `ERROR_SUCCESS_REBOOT_INITIATED` (1641):该操作已成功完成，因为系统在重新启动正在进行`/reboot`指定选项。

虽然仍可以使用 PnPUtil 安装驱动程序大容量，若要获取可操作的返回值建议指定`/install /add-driver`使用一次一个 INF。
