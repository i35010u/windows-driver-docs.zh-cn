---
title: 关闭 SAN 连接
description: 关闭 SAN 连接
ms.assetid: 1ef509e4-fc8c-4feb-ae65-3c0f19033f34
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19858d4c05810c8203fee980eaf11afd20c0e5b7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362011"
---
# <a name="shutting-down-a-san-connection"></a>关闭 SAN 连接





Windows 套接字开关使用其会话协议关闭的情况下连接到 SAN 的套接字。 开关的处理，即**WSPRecvDisconnect**， **WSPSendDisconnect**，并**WSPShutdown**来自应用程序调用。 此开关不转发到 SAN 服务提供商这些调用。 此开关使用其会话协议禁用接收和传输 SAN 套接字上的数据。

 

 





