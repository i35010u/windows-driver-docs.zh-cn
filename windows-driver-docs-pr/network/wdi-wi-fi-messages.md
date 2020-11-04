---
title: WDI 消息结构
description: 本部分介绍 WDI 命令消息的结构
ms.assetid: 09663C5F-A458-479F-B450-A994486A6C18
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e91dd5679798d294bb0876e28ccdeb86946ea44
ms.sourcegitcommit: ec7bebe3f94536455e62b372c2a28fe69d1717f7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2020
ms.locfileid: "93349655"
---
# <a name="wdi-message-structure"></a>WDI 消息结构


所有 WDI 命令消息必须以 [**WDI \_ 消息 \_ 标头**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_message_header) 结构开头。 命令头后跟零个或多个类型-长度-值 (TLV) 结构。

为从主机发送到 Wi-Fi 设备的消息定义的命令消息 Id 记录在 [WDI 任务 oid](./oid-wdi-task-change-operation-mode.md)、 [WDI 属性 Oid](./oid-wdi-abort-task.md)和 [WDI 状态指示](./ndis-status-wdi-indication-action-frame-received.md)中。

## <a name="tlvs"></a>TLVs


下表中定义了 TLVs 的结构。 TLVs 中的数据以小字节序字节顺序排序。

| 字段                      | 类型     | 描述                                                                                                                                   |
|----------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| 类型                       | UINT16   | TLV 结构的类型。 如果不触发错误，则必须跳过无法识别的 TLV 类型。                                              |
| 值缓冲区的长度 | UINT16   | 值缓冲区的大小（以字节为单位）。                                                                                                        |
| 值                      | 位\[\] | 负载缓冲区，可包含结构、结构列表或其他 TLVs。 数据大小必须与预期长度完全匹配。 |

 

有两种类型的 TLV 组：静态大小的 TLV 列表和多个 TLV 组。

## <a name="statically-sized-tlv-lists"></a>静态大小的 TLV 列表


静态大小的 TLV 列表包含多个静态大小的成员。 它们类似于标准 C 样式数组。

在此示例中， [**WDI \_ TLV \_ 单播 \_ 算法 \_ 列表**](./wdi-tlv-unicast-algorithm-list.md) 定义为 WDI \_ 算法对的列表 \_ 。

**类型** ： WDI \_ TLV \_ 单播 \_ 算法 \_ 列表

**长度** ： N \* sizeof (WDI \_ 算法 \_ 对) 

**值** ： WDI \_ 算法 \_ 对 \[ N\]


 

使用数组表示法在 TLV 引用主题中指定此用法。

## <a name="multi-tlv-groups"></a>多 TLV 组


如果事先不知道给定对象的大小，则使用多个 TLV 组。 此使用模式指定给定缓冲区中应有 N 个不同的大小不定大小的 TLVs。  (N) 的条目数事先未知，并由给定缓冲区中匹配 TLVs 的数目推断。

在此示例中，父缓冲区是 [**WDI \_ 消息 \_ 标头**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_message_header)，用于定义 TLV 缓冲区的末尾。 请注意， [**WDI \_ TLV \_ BSS \_ 项**](./wdi-tlv-bss-entry.md) 可能会在父缓冲区中的其他不同 TLV 类型之间交错。

| Offset                         | 字段                       | 类型                |
|--------------------------------|-----------------------------|---------------------|
| 0                              | WDI \_ 消息 \_ 标头        | 消息标头      |
| sizeof (WDI \_ 消息 \_ 标头)    | TLV ₀ (WDI \_ tlv \_ BSS \_ 条目)  | WDI \_ BSS \_ 条目     |
| TLV ₀ + L ₀ + sizeof (TLV 标头)  | TLV ₁ (WDI \_ tlv \_ BSS \_ 条目)  | WDI \_ BSS \_ 条目     |
| TLV ₁ + L ₁ + sizeof (TLV 标头)  | TLV ₂ (WDI \_ tlv \_ BSS \_ 条目)  | WDI \_ BSS \_ 条目     |
| TLV ₂ + L ₂ + sizeof (TLV 标头)  | TLV ₃ (其他 \_ tlv \_ 类型)      | 其他某些 TLV 类型 |
| TLV ₃ + L ₃ + sizeof (TLV 标头)  | TLV ₄ (WDI \_ tlv \_ BSS \_ 条目)  | WDI \_ BSS \_ 条目     |

 

对于包含其他 TLVs 的 TLVs，TLV 引用主题具有 *多个 tlv 实例允许* 列。 如果选中此列，则允许指定的 TLV 多次出现。 有关这种情况的示例，请参阅 [**WDI \_ TLV \_ CONNECT \_ PARAMETERS**](./wdi-tlv-connect-parameters.md)。

