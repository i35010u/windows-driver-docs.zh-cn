---
title: WDI 消息结构
description: 本部分介绍 WDI 命令消息的结构
ms.assetid: 09663C5F-A458-479F-B450-A994486A6C18
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ca9f38b751258d438daf81d66f9c979e0dce47c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841707"
---
# <a name="wdi-message-structure"></a>WDI 消息结构


所有 WDI 命令消息必须以[**WDI\_消息开头\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_message_header)结构。 命令头后跟零个或多个类型-长度-值（TLV）结构。

为从主机发送到 Wi-fi 设备的消息定义的命令消息 Id 记录在[WDI 任务 oid](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-task-oids)、 [WDI 属性 Oid](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-property-oids)和[WDI 状态指示](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-status-indications)中。

## <a name="tlvs"></a>TLVs


下表中定义了 TLVs 的结构。 TLVs 中的数据以小字节序字节顺序排序。

| 字段                      | 在任务栏的搜索框中键入     | 描述                                                                                                                                   |
|----------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| 在任务栏的搜索框中键入                       | UINT16   | TLV 结构的类型。 如果不触发错误，则必须跳过无法识别的 TLV 类型。                                              |
| 值缓冲区的长度 | UINT16   | 值缓冲区的大小（以字节为单位）。                                                                                                        |
| Value                      | 字节\[\] | 负载缓冲区，可包含结构、结构列表或其他 TLVs。 数据大小必须与预期长度完全匹配。 |

 

有两种类型的 TLV 组：静态大小的 TLV 列表和多个 TLV 组。

## <a name="statically-sized-tlv-lists"></a>静态大小的 TLV 列表


静态大小的 TLV 列表包含多个静态大小的成员。 它们类似于标准 C 样式数组。

在此示例中， [**WDI\_TLV\_单播\_算法\_列表**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-unicast-algorithm-list)定义为 WDI\_算法\_对的列表。

|        |                                    |
|--------|------------------------------------|
| 在任务栏的搜索框中键入   | WDI\_TLV\_单播\_算法\_列表 |
| 长度 | N \* sizeof （WDI\_算法\_对）      |
| Value  | WDI\_算法\_对\[N\]              |

 

使用数组表示法在 TLV 引用主题中指定此用法。

## <a name="multi-tlv-groups"></a>多 TLV 组


如果事先不知道给定对象的大小，则使用多个 TLV 组。 此使用模式指定给定缓冲区中应有 N 个不同的大小不定大小的 TLVs。 条目数（N）提前未知，并由给定缓冲区中匹配 TLVs 的数目推断。

在此示例中，父缓冲区是[**WDI\_消息\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_message_header)，用于定义 TLV 缓冲区的末尾。 请注意， [**WDI\_TLV\_BSS\_项**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-bss-entry)可能会在父缓冲区中的其他不同 TLV 类型之间交错。

| 偏移量                         | 字段                       | 在任务栏的搜索框中键入                |
|--------------------------------|-----------------------------|---------------------|
| 0                              | WDI\_消息\_标头        | 消息标头      |
| sizeof （WDI\_MESSAGE\_标头）   | TLV ₀（WDI\_TLV\_BSS\_条目） | WDI\_BSS\_条目     |
| TLV ₀ + L ₀ + sizeof （TLV 标头） | TLV ₁（WDI\_TLV\_BSS\_条目） | WDI\_BSS\_条目     |
| TLV ₁ + L ₁ + sizeof （TLV 标头） | TLV ₂（WDI\_TLV\_BSS\_条目） | WDI\_BSS\_条目     |
| TLV ₂ + L ₂ + sizeof （TLV 标头） | TLV ₃（其他\_TLV\_类型）     | 其他某些 TLV 类型 |
| TLV ₃ + L ₃ + sizeof （TLV 标头） | TLV ₄（WDI\_TLV\_BSS\_条目） | WDI\_BSS\_条目     |

 

对于包含其他 TLVs 的 TLVs，TLV 引用主题具有*多个 tlv 实例允许*列。 如果选中此列，则允许指定的 TLV 多次出现。 有关此示例的示例，请参阅[**WDI\_TLV\_连接\_参数**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-connect-parameters)。

 

 





