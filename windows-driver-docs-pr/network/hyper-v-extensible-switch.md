---
title: Hyper-v 可扩展交换机简介
description: Hyper-v 可扩展交换机支持一个接口, 该接口允许 NDIS 筛选器驱动程序 (称为可扩展交换机扩展) 的实例绑定到可扩展交换机驱动程序堆栈中。
ms.assetid: FB6AA190-0DB1-441E-9BC6-2FD3A6D88114
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb0144903b92991bf75a0fa9b015f382a86f069e
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565753"
---
# <a name="introduction-to-hyper-v-extensible-switch"></a>Hyper-v 可扩展交换机简介

Hyper-v 可扩展交换机支持一个接口, 该接口允许 NDIS 筛选器驱动程序 (称为*可扩展交换机扩展*) 的实例绑定到可扩展交换机驱动程序堆栈中。 绑定和启用后, 扩展可以监视、修改数据包并将数据包转发到可扩展的交换机端口。 这还允许扩展拒绝、重定向或将数据包发起给 Hyper-v 分区使用的端口。

从 Windows Server 2012 中的 NDIS 6.30 开始支持 Hyper-v 可扩展交换机。

本部分包括以下介绍 Hyper-v 可扩展交换机及其接口的主题:

-   [编写 Hyper-v 可扩展交换机扩展入门](getting-started-writing-a-hyper-v-extensible-switch-extension.md)
-   [Hyper-v 可扩展交换机概述](overview-of-the-hyper-v-extensible-switch.md)
-   [Hyper-v 可扩展交换机体系结构](hyper-v-extensible-switch-architecture.md)
-   [编写 Hyper-v 可扩展交换机扩展](writing-hyper-v-extensible-switch-extensions.md)
-   [安装 Hyper-v 可扩展交换机扩展](installing-hyper-v-extensible-switch-extensions.md)
-   [Hyper-v 可扩展交换机 Oid](hyper-v-extensible-switch-oids.md)

 

 





