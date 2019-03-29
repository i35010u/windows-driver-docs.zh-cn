---
title: 双向请求和响应架构
description: 双向请求和响应架构提供一组 XML 格式的查询和响应，可用于应用程序与打印机之间的双向通信。
ms.assetid: C005D90D-DCDB-410C-BD6F-83111849547E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f3579ceb8517082c1bf90c9271f143e1054f45e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563519"
---
# <a name="bidirectional-request-and-response-schemas"></a>双向请求和响应架构


双向请求和响应架构提供一组 XML 格式的查询和响应，可用于应用程序与打印机之间的双向通信。 使用这些查询，应用程序可以检索存储根据所使用的任何打印机配置和状态数据[双向通信架构](bidirectional-communication-schema.md)。 他们还可以设置任何可写打印机属性。 你可以使用[ **IBidiSpl2::SendRecvXMLStream** ](https://msdn.microsoft.com/library/windows/hardware/dd144983)或[ **IBidiSpl2::SendRecvXMLString** ](https://msdn.microsoft.com/library/windows/hardware/dd144984)函数与进行通信打印机。

有几个请求架构和相应的响应架构。 每个，正式定义，并举例说明每个，以下主题中的位置：

[获取请求和响应架构](get-request-and-response-schemas.md)

[EnumSchema 请求和响应架构](enumschema-request-and-response-schemas.md)

[设置请求和响应架构](set-request-and-response-schemas.md)

[GetWithArgument 请求和响应架构](getwithargument-request-and-response-schemas.md)

任何请求或响应的根元素标识它的类型。 &lt;EnumSchema&gt;请求和响应用于检索一组可访问打印机属性。 &lt;获取&gt;并&lt;设置&gt;请求允许多个查询。 一个&lt;设置&gt;"查询"指的是要将组和要向其中写入的值的属性。

每个&lt;查询&gt;具有架构 = 指向的属性或正被读取/写入属性值的属性。 这些架构的值 = 属性都是双向通信架构的树中的路径。

例如，每个&lt;获取&gt;响应重复查询的原始集并将结果添加到每个。 每个&lt;设置&gt;响应重复的"查询"，原始集，但不是提供详细的查询，会成功。 如果任何任意一个查询将失败&lt;获取&gt;或&lt;设置&gt;请求，结果是一条错误消息。

有关构造请求的详细信息，请参阅[构造 Bidi 通信架构查询](constructing-a-bidi-communication-schema-query.md)。

有关双向通信架构的详细信息，请参阅[双向通信架构层次结构](bidirectional-communication-schema-hierarchy.md)并[Bidi 通信架构参考](https://msdn.microsoft.com/library/windows/hardware/ff545175)主题。

 

 




