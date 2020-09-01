---
title: 在 NDIS 接口提供程序中处理 OID 查询和设置请求
description: 在 NDIS 接口提供程序中处理 OID 查询和设置请求
ms.assetid: 9ce51fc8-426f-4d36-8ee7-0a93b7b8439c
keywords:
- NDIS 网络接口 WDK，接口提供程序
- 网络接口 WDK，接口提供程序
- 接口提供程序 WDk 网络接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90228236868abb8cd00cfad5d35609b73eeb2800
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211093"
---
# <a name="handling-oid-query-and-set-requests-in-an-ndis-interface-provider"></a>在 NDIS 接口提供程序中处理 OID 查询和设置请求





NDISIF 接口定义了多个接口参数 (包括可以查询或设置的与 RFC 2863 中的信息相对应的统计计数器) 。 NDIS 通过接口提供程序在调用 [**NdisIfRegisterProvider**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterprovider) 函数时定义的入口点来访问这些接口参数。 有关注册为接口提供程序的详细信息，请参阅 [注册为接口提供程序](registering-as-an-interface-provider.md)。

接口参数由对象标识符 (Oid) 标识。 某些 Oid 特定于接口提供程序。

以下主题介绍如何处理查询和设置接口参数的请求：

[处理接口对象查询请求](handling-an-interface-object-query-request.md)

[处理接口对象设置请求](handling-an-interface-object-set-request.md)

 

