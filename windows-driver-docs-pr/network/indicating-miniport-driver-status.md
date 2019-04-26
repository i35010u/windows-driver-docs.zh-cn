---
title: 指示微型端口驱动程序状态
description: 指示微型端口驱动程序状态
ms.assetid: 366caecb-6c4b-42f3-927d-b72db764d6cf
keywords:
- WDK 的 CoNDIS 的状态信息
- 面向连接的 NDIS WDK，微型端口驱动程序
- CoNDIS WDK 网络、 微型端口驱动程序
- 微型端口驱动程序 WDK 网络的 CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b998cc9d22959f273b4366c5824a63c0a632fea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327752"
---
# <a name="indicating-miniport-driver-status"></a>指示微型端口驱动程序状态





微型端口驱动程序提供到过量驱动程序的状态指示。 CoNDIS 状态指示函数是无连接状态指示函数类似。

若要报告的 NIC 上的面向连接的 NIC 的状态中的更改或中的特定 VC 活动状态的更改，面向连接的微型端口驱动程序调用[ **NdisMCoIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563562)。 如果微型端口驱动程序报告的特定 VC 状态中的更改，它会提供*NdisVcHandle*标识 VC。

本部分包括以下主题：

[CoNDIS 微型端口驱动程序状态指示](condis-miniport-driver-status-indications.md)

[处理的 CoNDIS 协议驱动程序中的状态指示](handling-status-indications-in-a-condis-protocol-driver.md)

 

 





