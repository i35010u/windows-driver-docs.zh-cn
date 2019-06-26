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
ms.openlocfilehash: c27a027f8bb286f3c9b8e8f8b3b0cd289d3d65fe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353778"
---
# <a name="evaluating-changes-to-network-configuration"></a>评估对网络配置所做的更改





网络配置后，子系统将调用的通知对象的方法[ **INetCfgComponentNotifyGlobal** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547733(v=vs.85))并[INetCfgComponentNotifyBinding](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547730(v=vs.85))接口，通知对象应评估在子系统会发送的网络配置中所建议的更改，应执行与更改相关的操作。 通知对象的方法**INetCfgComponentNotifyGlobal**并**INetCfgComponentNotifyBinding**应实现接口来处理影响拥有该组件的更改对象。

下面的主题介绍如何通知对象处理对网络配置的更改的示例：

[添加组件](adding-a-component.md)

[更改组件的绑定](changing-bindings-for-a-component.md)

 

 





