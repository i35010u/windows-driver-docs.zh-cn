---
title: 评估对网络配置所做的更改
description: 评估对网络配置所做的更改
ms.assetid: 7e73fbb4-8d7d-44fb-96c9-aa748c207553
keywords:
- 通知对象 WDK 网络，请更改处理
- 网络通知对象 WDK 中，更改处理
- 更改网络配置 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 742ebfb2c94a8251845416b4bfa6455be670b0dd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368301"
---
# <a name="evaluating-changes-to-network-configuration"></a>评估对网络配置所做的更改





网络配置后，子系统将调用的通知对象的方法[ **INetCfgComponentNotifyGlobal** ](https://msdn.microsoft.com/library/windows/hardware/ff547733)并[INetCfgComponentNotifyBinding](https://msdn.microsoft.com/library/windows/hardware/ff547730)接口，通知对象应评估在子系统会发送的网络配置中所建议的更改，应执行与更改相关的操作。 通知对象的方法**INetCfgComponentNotifyGlobal**并**INetCfgComponentNotifyBinding**应实现接口来处理影响拥有该组件的更改对象。

下面的主题介绍如何通知对象处理对网络配置的更改的示例：

[添加组件](adding-a-component.md)

[更改组件的绑定](changing-bindings-for-a-component.md)

 

 





