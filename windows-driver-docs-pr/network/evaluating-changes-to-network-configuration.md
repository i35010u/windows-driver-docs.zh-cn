---
title: 评估对网络配置所做的更改
description: 评估对网络配置所做的更改
keywords:
- 通知对象 WDK 网络，更改处理
- 网络通知对象 WDK，更改处理
- 对网络配置 WDK 的更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40cc1874ef2e64932b786cb0e4d6aef809600d7e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788449"
---
# <a name="evaluating-changes-to-network-configuration"></a>评估对网络配置所做的更改





网络配置子系统调用 notify 对象的 [**INetCfgComponentNotifyGlobal**](/previous-versions/windows/hardware/network/ff547733(v=vs.85)) 和 [INetCfgComponentNotifyBinding](/previous-versions/windows/hardware/network/ff547730(v=vs.85)) 接口的方法之后，notify 对象应评估子系统发送的网络配置中的建议更改，并应执行与更改相关的操作。 应该实现 notify 对象的 **INetCfgComponentNotifyGlobal** 和 **INetCfgComponentNotifyBinding** 接口的方法，以仅处理影响拥有对象的组件的更改。

以下主题描述了通知对象如何处理网络配置更改的示例：

[添加组件](adding-a-component.md)

[更改组件的绑定](changing-bindings-for-a-component.md)

 

