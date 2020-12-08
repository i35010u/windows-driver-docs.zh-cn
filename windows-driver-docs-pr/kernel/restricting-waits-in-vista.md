---
title: 在 Vista 中限制等待
description: 在 Vista 中限制等待
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a28f9d153267700bf1be0bcd427cb15f58ac5e61
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820619"
---
# <a name="restricting-waits-in-vista"></a>在 Vista 中限制等待


由于许多设备驱动程序开发人员使用 [同步 I/o 编程技术](synchronous-i-o-programming.md)，因此当设备需要时间来响应时，Windows 可能会减慢或 "冻结"。 为了减少此问题，Vista 中的 i/o 管理器会在几分钟后停止执行 "停滞" 等待设备响应的程序。

**注意**   强烈建议在设备驱动程序中避免使用 [同步 I/o 编程技术](synchronous-i-o-programming.md) 。 如果 Vista 停止执行驱动程序代码，因为您的驱动程序正在等待设备，则您的设备可能处于未知状态。

 

 

 




