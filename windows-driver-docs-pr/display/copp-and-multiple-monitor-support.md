---
title: COPP 和多监视器支持
description: COPP 和多监视器支持
ms.assetid: 96bd24f6-4aba-4605-8fd4-465c86061044
keywords:
- 复制保护 WDK COPP，多个监视器
- 视频复制保护 WDK COPP，多个监视器
- COPP WDK DirectX VA，多个监视器
- 受保护视频 WDK COPP，多个监视器
- 多个监视器 WDK COPP
- 监视 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aab7bad643d839cfc720262a25e40b4fc467dcb9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346935"
---
# <a name="copp-and-multiple-monitor-support"></a>COPP 和多监视器支持


## <span id="ddk_copp_and_multiple_monitor_support_gg"></span><span id="DDK_COPP_AND_MULTIPLE_MONITOR_SUPPORT_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。

支持 COPP 的仅多监视器模式是双视图。 不支持各种克隆和影院模式。 此规则的唯一例外是这种情况，其中的图形适配器使用复合和 S-视频连接器，并同时源通过这两个连接器相同的显示信号。 在这种情况下，微型端口驱动程序应报告该连接器是 S-视频，并且应确保适当的保护措施应用于请求 COPP 调用通过应用程序启动时的两个显示输出。

 

 





