---
title: 双向请求和响应架构
description: 双向请求和响应架构提供一组 XML 格式的查询和响应，这些查询和响应可用于应用程序和打印机之间的双向通信。
ms.assetid: C005D90D-DCDB-410C-BD6F-83111849547E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a593d030c6109b5553975700e728cde159b2caec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841646"
---
# <a name="bidirectional-request-and-response-schemas"></a>双向请求和响应架构


双向请求和响应架构提供一组 XML 格式的查询和响应，这些查询和响应可用于应用程序和打印机之间的双向通信。 使用这些查询，应用程序可以检索按照[双向通信架构](bidirectional-communication-schema.md)存储的任何打印机配置和状态数据。 它们还可以设置任何可写打印机属性。 可以使用[**IBidiSpl2：： SendRecvXMLStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstream)或[**IBidiSpl2：： SendRecvXMLString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstring)函数与打印机通信。

有多个请求架构和相应的响应架构。 以下主题中介绍了每个的正式定义以及每个的示例：

[获取请求和响应架构](get-request-and-response-schemas.md)

[EnumSchema 请求和响应架构](enumschema-request-and-response-schemas.md)

[设置请求和响应架构](set-request-and-response-schemas.md)

[GetWithArgument 请求和响应架构](getwithargument-request-and-response-schemas.md)

任何请求或响应的根元素都标识其类型。 &lt;EnumSchema&gt; 请求和响应用于检索可访问的打印机属性的列表。 &lt;获取&gt; 并 &lt;集&gt; 请求允许多个查询。 &lt;集&gt; "query" 只是要设置的属性的标识以及要写入的值。

每个 &lt;查询&gt; 都有一个 schema = 属性，该属性指向要读取/写入的属性或属性值。 这些架构的值 = 属性是双向通信架构树中的路径。

例如，每个 &lt;获取&gt; 响应会重复原始查询集，并向每个查询添加结果。 每个 &lt;设置&gt; 响应都重复一组原始的 "查询"，但对于成功的查询没有更多的内容。 如果 &lt;获取&gt; 或 &lt;&gt; 请求的查询失败，则结果为错误消息。

有关构造请求的详细信息，请参阅[构造双向通信架构查询](constructing-a-bidi-communication-schema-query.md)。

有关双向通信架构的详细信息，请参阅[双向通信架构层次结构](bidirectional-communication-schema-hierarchy.md)和[双向通信架构参考](https://docs.microsoft.com/windows-hardware/drivers/print/bidi-communications-schema-reference)主题。

 

 




