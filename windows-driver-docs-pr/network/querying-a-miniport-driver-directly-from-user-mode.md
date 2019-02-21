---
title: 查询直接从用户模式下的微型端口驱动程序
description: 查询直接从用户模式下的微型端口驱动程序
ms.assetid: e0d153bf-0e50-47bc-b4e2-10f04c532b99
keywords:
- 用户模式驱动程序查询 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: defd016d20795ee0fcd45a388394588ef863e3d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522358"
---
# <a name="querying-a-miniport-driver-directly-from-user-mode"></a>查询直接从用户模式下的微型端口驱动程序





应用程序可以使用[ **IOCTL\_NDIS\_查询\_全局\_统计信息**](https://msdn.microsoft.com/library/windows/hardware/ff548975)直接查询信息从微型端口驱动程序的 nic。 在此操作，该应用程序可以使用任何查询的微型端口驱动程序支持的 OID。

 

 





