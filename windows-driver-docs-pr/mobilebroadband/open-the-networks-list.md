---
title: 打开网络列表
description: 打开网络列表
ms.assetid: 55935290-ebcb-4105-9b51-c862654f9f56
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8ea284cb30d2a37ce75400ff2bbc7659ba2d7e7
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217832"
---
# <a name="open-the-networks-list"></a>打开网络列表


可以通过调用帐户的当前网络对象的 [**ShowConnectionUI**](/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandNetwork#Windows_Networking_NetworkOperators_MobileBroadbandNetwork_ShowConnectionUI) 方法来打开 "网络" 列表。

例如：

``` syntax
account.currentNetwork.showConnectionUI()
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的常见任务](./create-a-mobilebroadbandaccount-object.md)

 

