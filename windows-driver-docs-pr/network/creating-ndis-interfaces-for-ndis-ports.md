---
title: 创建 NDIS 端口的 NDIS 接口
description: 创建 NDIS 端口的 NDIS 接口
ms.assetid: 3a856e4d-e32a-4c8a-8fa0-9976966bdf87
keywords:
- 端口 WDK NDIS，创建 NDIS 接口
- NDIS 端口 WDK，创建 NDIS 接口
- 注册 NDIS 接口提供程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d223278d2dde8313dbeca5238d8649bde0bcafa5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357334"
---
# <a name="creating-ndis-interfaces-for-ndis-ports"></a>创建 NDIS 端口的 NDIS 接口





默认情况下，NDIS 不会创建 NDIS 端口的 NDIS 网络接口。 如果有必要，请 NDIS 驱动程序可以调用[ **NdisIfRegisterProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff562716)函数注册为 NDIS 接口提供程序并调用[ **NdisIfRegisterInterface**](https://msdn.microsoft.com/library/windows/hardware/ff562715)函数以注册一个端口的接口。

有关 NDIS 网络接口的详细信息，请参阅[NDIS 6.0 网络接口](https://msdn.microsoft.com/library/windows/hardware/ff566525)。

 

 





