---
title: 微型端口适配器同步 OID 请求
description: 本主题介绍微型端口适配器同步 OID 请求
ms.assetid: E169972C-2EFF-4005-B279-9EFC53B431E2
keywords: 微型端口适配器同步 OID 请求接口、 微型端口适配器同步 OID 调用，WDK 微型端口适配器同步 Oid，微型端口适配器同步 OID 请求
ms.date: 09/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83ce015cff8e982951eaa75f7e5d09265ba2d88f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526297"
---
# <a name="miniport-adapter-synchronous-oid-requests"></a>微型端口适配器同步 OID 请求

若要支持同步 OID 请求路径，微型端口驱动程序提供[ *MiniportSynchronousOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/0DDF9CF8-91F6-4D7C-A8E8-FC425BF155CB)函数中的入口点[ **NDIS\_微型端口\_驱动程序\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff565958)结构时它们调用[ **NdisMRegisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563654)函数。

微型端口驱动程序，请*同步 OID 请求接口*不同于常规模式和直接 OID 请求接口，微型端口驱动程序无需注册异步*完整*回调函数。 这是因为同步性质的路径。 有关常规中常规、 直接和同步 Oid 之间的差别的详细信息，请参阅[同步 OID 请求接口在 NDIS 6.80](synchronous-oid-request-interface-in-ndis-6-80.md)。

> [!NOTE]
> NDIS 6.80 支持用于同步的 OID 请求接口的特定 Oid。 不支持 NDIS 6.80 和一些 NDIS 6.80 Oid 之前即已存在的 Oid。 若要确定是否可以在同步 OID 请求界面中使用 OID，请参阅 OID 引用页。

若要支持同步 OID 请求接口，使用标准的 OID 请求接口的文档。 下表显示了同步 OID 请求接口中的函数和标准的 OID 请求接口之间的关系。

| 同步 OID 函数 | 标准 OID 函数 |
| --- | --- |
| [*MiniportSynchronousOidRequest*](https://msdn.microsoft.com/library/windows/hardware/0DDF9CF8-91F6-4D7C-A8E8-FC425BF155CB) | [*MiniportOidRequest*](https://msdn.microsoft.com/library/windows/hardware/ff559416) |

