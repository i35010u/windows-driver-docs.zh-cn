---
title: 确定当前连接的移动宽带网络
description: 确定当前连接的移动宽带网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf7cc7c0954280258959590cfce069a2dc29d0ae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788579"
---
# <a name="determine-which-mobile-broadband-network-is-currently-connected"></a>确定当前连接的移动宽带网络


可以通过帐户的当前网络对象的 [**AccessPointName**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandNetwork#Windows_Networking_NetworkOperators_MobileBroadbandNetwork_AccessPointName) 属性检索 APN 来确定连接到的移动宽带网络。

例如：

``` syntax
account.currentNetwork.accessPointName
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的常见任务](./create-a-mobilebroadbandaccount-object.md)

 

