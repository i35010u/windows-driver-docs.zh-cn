---
title: 清理 SAN 的进程
description: 清理 SAN 的进程
ms.assetid: a6ae5882-4cde-43cf-8814-ea7ef5acee58
keywords:
- SAN 处理清理 WDK
- 清理 SAN 过程 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bb500a6110faf1eb791207d19128817e5bc84d0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563775"
---
# <a name="cleaning-up-a-process-for-a-san"></a>清理 SAN 的进程





准备就绪以进行清除的进程在其中运行应用程序时，它开始调用 Windows 套接字开关**WSPCleanup**函数。 开关，反过来，调用[ **WSPCleanup** ](https://msdn.microsoft.com/library/windows/hardware/ff566270) TCP/IP 提供程序和所有 SAN 服务提供程序的函数。 所有提供程序应释放它们使用的资源。 例如，资源可以包括用来同步事件的对象和用于执行数据传输的内存。

 

 





