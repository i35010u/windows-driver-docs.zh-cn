---
title: 查询实现的功能（功能索引 0）
description: 此函数返回此接口版本支持的函数。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d3e5fba8801775d9616dfa2b5d35c08029e5c302
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830945"
---
# <a name="query-implemented-functions-function-index-0"></a>查询实现的功能（功能索引 0）


此函数返回此接口版本支持的函数。 每个 DSM 的函数 0 \_ 是一个查询函数，它返回支持的函数索引集，并且始终是必需的。 有关函数0的定义，请参阅 \_ [ACPI 6.0 规范](https://uefi.org/specifications)中的 9.14.1 "DSM (设备特定的方法) " 部分。

## <a name="arguments-arg-3"></a>参数 (ARG 3) 


无。

## <a name="returns"></a>返回


此函数返回一个 ACPI 缓冲区，其中包含以下字节值，顺序如下：0xFF、0xFF、0xFF、& 0xFF。

## <a name="related-topics"></a>相关主题


[\_用于字节寻址的支持能源的函数类 (函数接口 1) 的 DSM 接口 ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

