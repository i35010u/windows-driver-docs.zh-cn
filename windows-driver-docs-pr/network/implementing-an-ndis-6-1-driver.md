---
title: 实现 NDIS 6.1 驱动程序
description: 实现 NDIS 6.1 驱动程序
ms.assetid: a2b5d722-88b3-4321-9d0d-451f465194d1
keywords:
- NDIS WDK，网络驱动程序中的版本
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da47aad532bd43516fd5c1eaaed3a69946638720
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566559"
---
# <a name="implementing-an-ndis-61-driver"></a>实现 NDIS 6.1 驱动程序





NDIS 6.1 驱动程序必须报告正确的 NDIS 版本时它会向 NDIS 注册。

必须更新的主版本号和次的 NDIS 版本编号在 NDIS\_*Xxx*\_驱动程序\_特征结构与支持 NDIS 6.1。 **MajorNdisVersion**成员必须包含 0x06:sp 和**MinorNdisVersion**成员必须包含 0x01。 此要求适用于微型端口、 协议和筛选器驱动程序。

 

 





