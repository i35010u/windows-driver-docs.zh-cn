---
title: 通知对象示意图
description: 通知对象示意图
keywords:
- 通知对象 WDK 网络，关系图
- 网络通知对象 WDK，关系图
- 网络配置子系统 WDK
- 子系统 WDK 网络配置
- 通知 WDK 网络，notifyo 对象关系图
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b801ce7f39ff465279fa501da7c161c25997f9c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820577"
---
# <a name="notify-object-diagram"></a>通知对象示意图





下图显示了安装或控制网络的客户端应用程序如何调用 *网络配置子系统*。 此子系统调用网络类安装程序来安装网络组件并注册这些组件的通知对象。 通知对象回发到子系统，以代表拥有对象的组件配置网络。

![说明安装或控制网络的客户端应用程序如何调用网络配置子系统的关系图](images/netcfg.png)

 

 





