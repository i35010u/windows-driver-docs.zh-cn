---
title: 类型化数据
description: 类型化数据
ms.assetid: 44a84dfd-03f8-4d7b-8d71-e4b3ee23d105
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4faba91f927d2c6bdb77b3de86989abaf4edef32
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209843"
---
# <a name="typed-data"></a>类型化数据


EngExtCpp 扩展框架提供了几个类来帮助操作目标的内存。 [**ExtRemoteData**](/windows-hardware/drivers/ddi/engextcpp/nl-engextcpp-extremotedata)类描述目标内存的一小部分。 如果此内存的类型已知，则将其称为 *类型化数据* ，并由 [**ExtRemoteTyped**](/windows-hardware/drivers/ddi/engextcpp/nl-engextcpp-extremotetyped) 对象进行描述。

可以使用 [**ExtRemoteList**](/windows-hardware/drivers/ddi/engextcpp/nl-engextcpp-extremotelist) 循环访问 Windows 列表，如果列表中对象的类型为已知，则为 [**ExtRemoteTypedList**](/windows-hardware/drivers/ddi/engextcpp/nl-engextcpp-extremotetypedlist)。

**注意**   与[**ExtExtension**](/previous-versions/ff543981(v=vs.85))中的客户端对象一样，这些类的实例仅在扩展库用于执行扩展命令或设置输出的结构的格式时才有效。 具体而言，不应缓存这些项。 有关客户端对象何时有效的详细信息，请参阅 [客户端对象和引擎](client-objects-and-the-engine.md)。

 

### <a name="span-idremote_dataspanspan-idremote_dataspanremote-data"></a><span id="remote_data"></span><span id="REMOTE_DATA"></span>远程数据

应使用 [**ExtRemoteData**](/windows-hardware/drivers/ddi/engextcpp/nl-engextcpp-extremotedata)类处理远程数据。 此类是一个围绕目标内存的小部分的包装。 **ExtRemoteData** 会自动检索内存，并通过引发方法包装其他常见请求。

### <a name="span-idremote_typed_dataspanspan-idremote_typed_dataspanremote-typed-data"></a><span id="remote_typed_data"></span><span id="REMOTE_TYPED_DATA"></span>远程类型化数据

如果远程数据的类型已知，则应使用 [**ExtRemoteTyped**](/windows-hardware/drivers/ddi/engextcpp/nl-engextcpp-extremotetyped) 类进行处理。 此类是一个增强的远程数据对象，它理解从符号类型信息中键入的数据。 它通过符号或强制转换初始化为特定对象，之后它可以像给定类型的对象一样使用。

### <a name="span-idremote_listsspanspan-idremote_listsspanremote-lists"></a><span id="remote_lists"></span><span id="REMOTE_LISTS"></span>远程列表

若要处理远程列表，请使用 [**ExtRemoteList**](/windows-hardware/drivers/ddi/engextcpp/nl-engextcpp-extremotelist) 类。 此类可用于单向链接列表或双重链接列表。 如果列表是双向链接的，则假定上一个指针紧跟在下一个指针后面。 类包含可循环访问列表并同时检索节点的方法。 **ExtRemoteList** 也可与 null 终止或循环列表一起使用。

### <a name="span-idremote_typed_listsspanspan-idremote_typed_listsspanremote-typed-lists"></a><span id="remote_typed_lists"></span><span id="REMOTE_TYPED_LISTS"></span>远程类型列表

若要在列表中的节点类型已知时处理远程列表，请使用 [**ExtRemoteTypedList**](/windows-hardware/drivers/ddi/engextcpp/nl-engextcpp-extremotetypedlist) 类。 这是 [**ExtRemoteList**](/windows-hardware/drivers/ddi/engextcpp/nl-engextcpp-extremotelist)的增强版本。 除了 **ExtRemoteList**的基本功能， **ExtRemoteTypedList** 还自动确定来自类型信息的链接偏移量。

 

