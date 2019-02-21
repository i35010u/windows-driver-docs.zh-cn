---
title: WDI 消息结构
description: 本部分介绍 WDI 命令消息的结构
ms.assetid: 09663C5F-A458-479F-B450-A994486A6C18
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16859876b0bf381c6b46f36d6d0aa7e54643b90a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555594"
---
# <a name="wdi-message-structure"></a>WDI 消息结构


WDI 命令的所有消息必须都开头[ **WDI\_消息\_标头**](https://msdn.microsoft.com/library/windows/hardware/dn926074)结构。 命令标头后跟零个或多个类型-长度-值 (TLV) 结构。

为从主机到 Wi-fi 设备发送的消息记录在定义的命令消息 Id [WDI 任务 Oid](https://msdn.microsoft.com/library/windows/hardware/dn926082)， [WDI 属性 Oid](https://msdn.microsoft.com/library/windows/hardware/dn926079)，并[WDI 状态指示](https://msdn.microsoft.com/library/windows/hardware/dn926080)。

## <a name="tlvs"></a>TLVs


下表中定义的 TLVs 结构。 TLVs 中的数据是按 little-endian 字节顺序。

| 字段                      | 在任务栏的搜索框中键入     | 描述                                                                                                                                   |
|----------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| 在任务栏的搜索框中键入                       | UINT16   | TLV 结构的类型。 无法识别的 TLV 类型必须跳过不触发错误。                                              |
| 值缓冲区的长度 | UINT16   | 以字节为单位的值缓冲区的大小。                                                                                                        |
| 值                      | 字节\[\] | 有效负载缓冲区，其中可能包含一个结构、 结构、 列表或其他 TLVs。 数据大小必须完全符合预期的长度。 |

 

有两种类型的 TLV 分组： 静态大小的 TLV 列表和多 TLV 组。

## <a name="statically-sized-tlv-lists"></a>以静态方式调整大小 TLV 列表


以静态方式调整大小 TLV 列表包含以静态方式调整大小的几个成员。 它们类似于标准的 C 样式数组。

在此示例中， [ **WDI\_TLV\_单播\_算法\_列表**](https://msdn.microsoft.com/library/windows/hardware/dn898073)定义为一系列 WDI\_ALGO\_对.

|        |                                    |
|--------|------------------------------------|
| 在任务栏的搜索框中键入   | WDI\_TLV\_单播\_算法\_列表 |
| 长度 | N \* sizeof(WDI\_ALGO\_PAIRS)      |
| 值  | WDI\_ALGO\_PAIRS\[N\]              |

 

使用数组表示法的 TLV 参考主题中指定此用法。

## <a name="multi-tlv-groups"></a>多 TLV 组


如果事先不知道给定对象的大小，使用多 TLV 组。 此使用模式指定 N 不同大小不定的 TLVs 会给定缓冲区中。 项数 (N) 不知道提前，并推断匹配 TLVs 中给定的缓冲区数。

在此示例中，是父缓冲区[ **WDI\_消息\_标头**](https://msdn.microsoft.com/library/windows/hardware/dn926074)，用于定义 TLV 缓冲区的末尾。 请注意， [ **WDI\_TLV\_BSS\_条目**](https://msdn.microsoft.com/library/windows/hardware/dn926162)可能会混杂在父缓冲区中的其他不同 TLV 类型之间。

| 偏移量                         | 字段                       | 在任务栏的搜索框中键入                |
|--------------------------------|-----------------------------|---------------------|
| 0                              | WDI\_消息\_标头        | 消息标头      |
| sizeof(WDI\_MESSAGE\_HEADER)   | TLV₀ (WDI\_TLV\_BSS\_条目) | WDI\_BSS\_条目     |
| TLV₀ + L₀ + sizeof （TLV 标头） | TLV₁ (WDI\_TLV\_BSS\_条目) | WDI\_BSS\_条目     |
| TLV₁ + L₁ + sizeof （TLV 标头） | TLV₂ (WDI\_TLV\_BSS\_条目) | WDI\_BSS\_条目     |
| TLV₂ + L₂ + sizeof （TLV 标头） | TLV₃ (的社会\_TLV\_类型)     | 某些其他 TLV 类型 |
| TLV₃ + L₃ + sizeof （TLV 标头） | TLV₄ (WDI\_TLV\_BSS\_条目) | WDI\_BSS\_条目     |

 

对于包含其他 TLVs TLVs，具有 TLV 参考主题*允许多个 TLV 实例*列。 如果选中此列，则允许指定的 TLV 出现多次。 此示例，请参阅[ **WDI\_TLV\_CONNECT\_参数**](https://msdn.microsoft.com/library/windows/hardware/dn926266)。

 

 





