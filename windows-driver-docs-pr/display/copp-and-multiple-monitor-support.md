---
title: COPP 和多监视器支持
description: COPP 和多监视器支持
keywords:
- 复制保护 WDK COPP，多个监视器
- 视频副本保护 WDK COPP，多个监视器
- COPP WDK DirectX VA，多监视器
- 受保护的视频 WDK COPP、多个监视器
- 多监视器 WDK COPP
- 监视 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3873200e85c10e7108e0fee7a700792742a2e31
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824233"
---
# <a name="copp-and-multiple-monitor-support"></a>COPP 和多监视器支持


## <span id="ddk_copp_and_multiple_monitor_support_gg"></span><span id="DDK_COPP_AND_MULTIPLE_MONITOR_SUPPORT_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

COPP 支持的唯一多监视器模式为双屏。 不支持各种仿制和影院模式。 此规则的唯一例外情况是图形适配器同时使用复合和 S 视频连接器，并同时通过这两个连接器将同一显示信号送入同一视频。 在这种情况下，视频微型端口驱动程序应报告连接器为 S-视频，并确保在由通过应用程序启动的 COPP 调用请求时，将相应的保护应用于两个显示输出。

 

 





