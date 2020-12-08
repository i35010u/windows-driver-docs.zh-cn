---
title: 实现 NDIS 6.1 驱动程序
description: 实现 NDIS 6.1 驱动程序
keywords:
- NDIS WDK，网络驱动程序中的版本
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6498b0e8d1359fb8e2c2a080ba53c1f9425eba3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840013"
---
# <a name="implementing-an-ndis-61-driver"></a>实现 NDIS 6.1 驱动程序





当 ndis 6.1 驱动程序使用 NDIS 注册时，它必须报告正确的 NDIS 版本。

必须在 NDIS Xxx 驱动程序特征结构中更新主要和次要 NDIS 版本号 \_ *Xxx* \_ \_ ，才能支持 ndis 6.1。 **MajorNdisVersion** 成员必须包含0x06，且 **MinorNdisVersion** 成员必须包含0x01。 此要求适用于微型端口、协议和筛选器驱动程序。

 

 





