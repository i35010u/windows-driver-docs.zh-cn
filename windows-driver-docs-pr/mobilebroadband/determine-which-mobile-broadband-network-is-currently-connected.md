---
title: 确定当前连接的移动宽带网络
description: 确定当前连接的移动宽带网络
ms.assetid: 65a47e79-3976-4f72-b810-982e7222fee3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 323b182aa9c211f79b438be20727e510f44d7a1f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215298"
---
# <a name="determine-which-mobile-broadband-network-is-currently-connected"></a>确定当前连接的移动宽带网络


可以通过帐户的当前网络对象的 [**AccessPointName**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandNetwork#Windows_Networking_NetworkOperators_MobileBroadbandNetwork_AccessPointName) 属性检索 APN 来确定连接到的移动宽带网络。

例如：

``` syntax
account.currentNetwork.accessPointName
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的常见任务](./create-a-mobilebroadbandaccount-object.md)

 

