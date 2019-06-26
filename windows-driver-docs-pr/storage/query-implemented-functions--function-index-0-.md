---
title: 查询实现的功能（功能索引 0）
description: 此函数返回此接口版本所支持的函数。
ms.assetid: AFF735D7-BB3F-4532-8BF4-F616C081921C
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a160821f8b3b4bba5ab1c0e886f461ebe5edc724
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368959"
---
# <a name="query-implemented-functions-function-index-0"></a>查询实现的功能（功能索引 0）


此函数返回此接口版本所支持的函数。 函数的每个\_DSM 是返回集支持的函数的索引，并始终是必需的查询函数。 有关函数 0 的定义，请参阅部分 9.14.1，"\_DSM （设备特定的方法）"中[ACPI 6.0 规范](https://uefi.org/specifications)。

## <a name="arguments-arg-3"></a>自变量 (ARG 3)


无。

## <a name="returns"></a>返回


此函数将返回一个包含订单中的以下字节值的 ACPI 缓冲区：0xFF，0xff 内，0xff 内，和 0xFF。

## <a name="related-topics"></a>相关主题


[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

