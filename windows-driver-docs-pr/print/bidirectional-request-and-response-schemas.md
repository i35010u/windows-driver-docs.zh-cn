---
title: 双向请求和响应架构
description: 双向请求和响应架构提供一组 XML 格式的查询和响应，这些查询和响应可用于应用程序和打印机之间的双向通信。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1e223bd1cc4effd7d19504c0e9c9c8f3ea889fc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797797"
---
# <a name="bidirectional-request-and-response-schemas"></a>双向请求和响应架构


双向请求和响应架构提供一组 XML 格式的查询和响应，这些查询和响应可用于应用程序和打印机之间的双向通信。 使用这些查询，应用程序可以检索按照 [双向通信架构](bidirectional-communication-schema.md)存储的任何打印机配置和状态数据。 它们还可以设置任何可写打印机属性。 可以使用 [**IBidiSpl2：： SendRecvXMLStream**](/windows-hardware/drivers/ddi/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstream) 或 [**IBidiSpl2：： SendRecvXMLString**](/windows-hardware/drivers/ddi/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstring) 函数与打印机通信。

有多个请求架构和相应的响应架构。 以下主题中介绍了每个的正式定义以及每个的示例：

[获取请求和响应架构](get-request-and-response-schemas.md)

[EnumSchema 请求和响应架构](enumschema-request-and-response-schemas.md)

[设置请求和响应架构](set-request-and-response-schemas.md)

[GetWithArgument 请求和响应架构](getwithargument-request-and-response-schemas.md)

任何请求或响应的根元素都标识其类型。 &lt;EnumSchema &gt; 请求和响应用于检索可访问的打印机属性的列表。 &lt;Get &gt; 和 &lt; Set &gt; 请求允许多个查询。 &lt;集 &gt; "query" 只是要设置的属性的标识以及要写入的值。

每个 &lt; 查询 &gt; 都有一个 schema = 属性，该属性指向要读取/写入的属性或属性值。 这些架构的值 = 属性是双向通信架构树中的路径。

例如，每个 &lt; Get &gt; 响应会重复一组原始查询，并向每个查询添加结果。 每个 &lt; Set &gt; 响应都重复一组原始的 "查询"，但对于成功的查询没有更多的内容。 如果获取或设置请求的任何查询均失败 &lt; &gt; ，则 &lt; &gt; 结果为错误消息。

有关构造请求的详细信息，请参阅 [构造双向通信架构查询](constructing-a-bidi-communication-schema-query.md)。

有关双向通信架构的详细信息，请参阅 [双向通信架构层次结构](bidirectional-communication-schema-hierarchy.md) 和 [双向通信架构参考](./bidi-communications-schema-reference.md) 主题。

 

