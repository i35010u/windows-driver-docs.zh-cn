---
title: 直接从用户模式查询微型端口驱动程序
description: 直接从用户模式查询微型端口驱动程序
ms.assetid: e0d153bf-0e50-47bc-b4e2-10f04c532b99
keywords:
- 用户模式驱动程序查询 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45c501fd0efd92a89deecadef7ada927760d7a66
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385442"
---
# <a name="querying-a-miniport-driver-directly-from-user-mode"></a>直接从用户模式查询微型端口驱动程序





应用程序可以使用[ **IOCTL\_NDIS\_查询\_全局\_统计信息**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff548975(v=vs.85))直接查询信息从微型端口驱动程序的 nic。 在此操作，该应用程序可以使用任何查询的微型端口驱动程序支持的 OID。

 

 





