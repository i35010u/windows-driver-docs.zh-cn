---
title: RSS 哈希函数
description: RSS 哈希函数
ms.assetid: e7698573-c3d1-4ac6-a985-93cf7fc6e585
keywords:
- 接收方缩放 WDK 网络，哈希
- RSS WDK 网络、 哈希
- 哈希 WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3559780bdce1a6a0896cd6e599afac6c4a22d121
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359100"
---
# <a name="rss-hashing-functions"></a>RSS 哈希函数


## <a name="overview"></a>概述

一个 NIC 或其微型端口驱动程序使用 RSS 哈希函数来计算 RSS 哈希值。

过量驱动程序设置哈希类型、 函数和表，要将连接分配到的 Cpu。 有关详细信息，请参阅[RSS 配置](rss-configuration.md)。

哈希函数可以是以下值之一：

- **NdisHashFunctionToeplitz**
- **NdisHashFunctionReserved1**
- **NdisHashFunctionReserved2**
- **NdisHashFunctionReserved3**

>[!NOTE]
> 目前， **NdisHashFunctionToeplitz**是唯一的哈希函数提供给微型端口驱动程序。 其他哈希函数仅供 NDIS。 

微型端口驱动程序应识别的哈希函数和值，它在每个使用该值[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构之前，驱动程序指示接收到的数据。 有关详细信息，请参阅[接收数据，该值指示 RSS](indicating-rss-receive-data.md)。

## <a name="examples"></a>示例

以下四个伪代码示例演示如何计算**NdisHashFunctionToeplitz**哈希值。 这些示例表示四个可能的哈希类型可供**NdisHashFunctionToeplitz**。 有关哈希类型的详细信息，请参阅[RSS 哈希算法类型](rss-hashing-types.md)。

若要简化示例，一种通用的算法，处理输入的字节流是必需的。 更高版本中的四个示例定义了特定格式的字节流。

基础驱动程序提供了一个密钥 (K) 到微型端口驱动程序中使用哈希计算。 关键是 40 个字节 (320 bits)。 有关密钥的详细信息，请参阅[RSS 配置](rss-configuration.md)。

给定包含输入的数组*n*个字节的字节流定义，如下所示：

```c++
input[0] input[1] input[2] ... input[n-1]
```

输入的最左侧字节\[0\]，并输入的最高有效位\[0\]是最左边的位。 输入的最右侧的字节\[n-1\]，并输入的最高有效位\[n-1\]是最右边的位。

根据上述定义，用于处理常规输入的字节流的伪代码定义，如下所示：

```c++
ComputeHash(input[], n)

result = 0
For each bit b in input[] from left to right
{
if (b == 1) result ^= (left-most 32 bits of K)
shift K left 1 bit position
}

return result
```

伪代码包含项的窗体@n-m。 这些条目标识 TCP 数据包中的每个元素的字节的范围。

### <a name="example-hash-calculation-for-ipv4-with-the-tcp-header"></a>对 IPv4 与 TCP 标头示例哈希计算

数据包的 SourceAddress、 DestinationAddress、 SourcePort 和 DestinationPort 字段连接到的字节数组，保留在包中发生的顺序：

```c++
Input[12] = @12-15, @16-19, @20-21, @22-23
Result = ComputeHash(Input, 12)
```

### <a name="example-hash-calculation-for-ipv4-only"></a>示例仅使用 IPv4 的哈希计算

将数据包的 SourceAddress 和 DestinationAddress 字段连接到的字节数组。

```c++
Input[8] = @12-15, @16-19
Result = ComputeHash(Input, 8) 
```

### <a name="example-hash-calculation-for-ipv6-with-the-tcp-header"></a>IPv6 使用 TCP 标头的示例哈希计算

将数据包的 SourceAddress、 DestinationAddress、 SourcePort 和 DestinationPort 字段连接到的字节数组，保留在包中发生的顺序。

```c++
Input[36] = @8-23, @24-39, @40-41, @42-43
Result = ComputeHash(Input, 36)
```

### <a name="example-hash-calculation-for-ipv6-only"></a>仅 IPv6 示例哈希计算

将数据包的 SourceAddress 和 DestinationAddress 字段连接到的字节数组。

```c++
Input[32] = @8-23, @24-39
Result = ComputeHash(Input, 32)
```

 

 





