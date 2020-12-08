---
title: Hyper-V 可扩展交换机简介
description: Hyper-v 可扩展交换机支持一个接口，该接口允许 (称为可扩展交换机扩展) 的 NDIS 筛选器驱动程序的实例绑定到可扩展交换机驱动程序堆栈中。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c51415468b1d79fe5b6c1b501c86ae284b0d4c1c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794489"
---
# <a name="introduction-to-hyper-v-extensible-switch"></a>Hyper-V 可扩展交换机简介

Hyper-v 可扩展交换机支持一个接口，该接口允许 (称为 *可扩展交换机扩展*) 的 NDIS 筛选器驱动程序的实例绑定到可扩展交换机驱动程序堆栈中。 绑定和启用后，扩展可以监视、修改数据包并将数据包转发到可扩展的交换机端口。 这还允许扩展拒绝、重定向或将数据包发起给 Hyper-v 分区使用的端口。

从 Windows Server 2012 中的 NDIS 6.30 开始支持 Hyper-v 可扩展交换机。

本部分包括以下介绍 Hyper-v 可扩展交换机及其接口的主题：

-   [开始编写 Hyper-V 可扩展交换机扩展](getting-started-writing-a-hyper-v-extensible-switch-extension.md)
-   [Hyper-V 可扩展交换机概述](overview-of-the-hyper-v-extensible-switch.md)
-   [Hyper-V 可扩展交换机体系结构](hyper-v-extensible-switch-architecture.md)
-   [编写 Hyper-V 可扩展交换机扩展](writing-hyper-v-extensible-switch-extensions.md)
-   [安装 Hyper-V 可扩展交换机扩展](installing-hyper-v-extensible-switch-extensions.md)
-   [Hyper-V 可扩展交换机 OID](hyper-v-extensible-switch-oids.md)

 

 





