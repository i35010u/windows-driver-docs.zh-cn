---
title: 清理 SAN 的进程
description: 清理 SAN 的进程
ms.assetid: a6ae5882-4cde-43cf-8814-ea7ef5acee58
keywords:
- SAN 处理清理 WDK
- 清理 SAN 过程 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d88a75364760a1a0c02e3e427d9a51fa89ca9fc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382784"
---
# <a name="cleaning-up-a-process-for-a-san"></a>清理 SAN 的进程





准备就绪以进行清除的进程在其中运行应用程序时，它开始调用 Windows 套接字开关**WSPCleanup**函数。 开关，反过来，调用[ **WSPCleanup** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566270(v=vs.85)) TCP/IP 提供程序和所有 SAN 服务提供程序的函数。 所有提供程序应释放它们使用的资源。 例如，资源可以包括用来同步事件的对象和用于执行数据传输的内存。

 

 





