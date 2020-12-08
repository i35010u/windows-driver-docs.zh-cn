---
title: 直接从用户模式查询微型端口驱动程序
description: 直接从用户模式查询微型端口驱动程序
keywords:
- 用户模式驱动程序查询 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9da3d6408bd0fc713fe2cdc41f48c37889909bdf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803501"
---
# <a name="querying-a-miniport-driver-directly-from-user-mode"></a>直接从用户模式查询微型端口驱动程序





应用程序可以使用 [**IOCTL \_ NDIS \_ 查询 \_ 全局 \_ 统计**](/previous-versions/windows/hardware/network/ff548975(v=vs.85)) 信息直接从微型端口驱动程序的 NIC 中查询信息。 在此操作中，应用程序可以使用微型端口驱动程序支持的任何查询 OID。

 

