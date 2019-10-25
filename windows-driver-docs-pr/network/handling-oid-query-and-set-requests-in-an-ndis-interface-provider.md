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
ms.openlocfilehash: 97a517111c9f25105ae97a5c3aeecf1fda78b4e8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842577"
---
# <a name="handling-oid-query-and-set-requests-in-an-ndis-interface-provider"></a>在 NDIS 接口提供程序中处理 OID 查询和设置请求





NDISIF 接口定义了多个可以查询或设置的接口参数（包括统计计数器），这些参数对应于 RFC 2863 中的信息。 NDIS 通过接口提供程序在调用[**NdisIfRegisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterprovider)函数时定义的入口点来访问这些接口参数。 有关注册为接口提供程序的详细信息，请参阅[注册为接口提供程序](registering-as-an-interface-provider.md)。

接口参数由对象标识符（Oid）标识。 某些 Oid 特定于接口提供程序。

以下主题介绍如何处理查询和设置接口参数的请求：

[处理接口对象查询请求](handling-an-interface-object-query-request.md)

[处理接口对象集请求](handling-an-interface-object-set-request.md)

 

 





