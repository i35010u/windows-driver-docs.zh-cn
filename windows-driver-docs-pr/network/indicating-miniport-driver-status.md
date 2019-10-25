---
title: 指示微型端口驱动程序状态
description: 指示微型端口驱动程序状态
ms.assetid: 366caecb-6c4b-42f3-927d-b72db764d6cf
keywords:
- 状态信息 WDK CoNDIS
- 面向连接的 NDIS WDK，微型端口驱动程序
- CoNDIS WDK 网络，微型端口驱动程序
- 微型端口驱动程序 WDK 网络，CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96360f129a8debca86625926dd7b47b0a5c61fe8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824686"
---
# <a name="indicating-miniport-driver-status"></a>指示微型端口驱动程序状态





微型端口驱动程序为过量驱动程序提供状态指示。 CoNDIS 状态指示函数类似于无连接状态指示函数。

若要报告面向连接的 NIC 的状态更改或 NIC 上特定 VC 活动的状态更改，面向连接的微型端口驱动程序调用[**NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)。 如果微型端口驱动程序报告特定 VC 状态发生了变化，则它会提供标识 VC 的*NdisVcHandle* 。

本部分包括下列主题：

[CoNDIS 微型端口驱动程序状态指示](condis-miniport-driver-status-indications.md)

[处理 CoNDIS 协议驱动程序中的状态指示](handling-status-indications-in-a-condis-protocol-driver.md)

 

 





