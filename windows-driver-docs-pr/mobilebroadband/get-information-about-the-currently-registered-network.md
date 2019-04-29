---
title: 获取当前已注册网络的信息
description: 获取当前已注册网络的信息
ms.assetid: 94321933-fc93-4203-8de1-e715d66fd1e3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 936b189d5d82aab5dbfe2191cb11fc62bbedeccc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380168"
---
# <a name="get-information-about-the-currently-registered-network"></a>获取当前已注册网络的信息


可以获取的数据类、 服务提供程序 ID 和移动宽带设备当前已注册到的网络的名称。 若要执行此操作，请使用[ **RegisteredDataClass**](https://msdn.microsoft.com/library/windows/apps/hh967833)， [ **RegisteredProviderId**](https://msdn.microsoft.com/library/windows/apps/hh967834)，并[ **RegisteredProviderName** ](https://msdn.microsoft.com/library/windows/apps/hh967835)帐户当前的网络对象的属性。

例如：

``` syntax
var myNetwork = myNetworkAccountObject.currentNetwork
if (myNetwork != null && myNetwork.registeredDataClass == DataClasses.LteAdvanced)
{
  // user is connected to an LTE network
}
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 Api 的常见任务](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






