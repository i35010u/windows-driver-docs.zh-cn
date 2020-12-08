---
title: 在筛选器中提供 IPrintCoreHelper 配置服务
description: 在筛选器中提供 IPrintCoreHelper 配置服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d8664a2c7b296cba32745a751fe87187e9e88d6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807181"
---
# <a name="providing-iprintcorehelper-configuration-service-to-filters"></a>在筛选器中提供 IPrintCoreHelper 配置服务


**IPrintCoreHelper** 接口是由 Windows Vista Unidrv/PScript5 配置模块实现的新接口。 此接口允许客户端计算机执行以下操作：

1.  枚举 GPD 或 PPD 功能、选项和约束。

2.  获取 PPD 的全局、功能或选项属性的值。

3.  获取文档的当前设置-粘滞和 printer-粘滞 GPD 或 PPD 功能。

4.  为 GPD 和 GDL 内容创建 GDL 分析器快照以实现完全访问。

 

 




