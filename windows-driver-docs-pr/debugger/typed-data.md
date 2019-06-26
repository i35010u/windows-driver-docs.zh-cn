---
title: 类型化数据
description: 类型化数据
ms.assetid: 44a84dfd-03f8-4d7b-8d71-e4b3ee23d105
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c1c97f1ede75bc278c97f6dc28420bc97aa0107
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368638"
---
# <a name="typed-data"></a>类型化数据


EngExtCpp 扩展框架提供了一些类，以帮助操作目标的内存。 [ **ExtRemoteData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/engextcpp/nl-engextcpp-extremotedata)类描述了一小段目标的内存。 如果此内存的类型已知的因此将它称为*类型的数据*进行了说明[ **ExtRemoteTyped** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/engextcpp/nl-engextcpp-extremotetyped)对象。

可以使用循环访问 Windows 列表[ **ExtRemoteList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/engextcpp/nl-engextcpp-extremotelist)并在列表中的对象的类型已知时，如果[ **ExtRemoteTypedList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/engextcpp/nl-engextcpp-extremotetypedlist).

**请注意**  等中的客户端对象[ **ExtExtension**](https://msdn.microsoft.com/library/windows/hardware/ff543981)，这些类的实例并且只有效时才使用扩展库来执行扩展命令或格式输出的结构。 具体而言，它们不应缓存。 有关在客户端对象的有效的详细信息，请参阅[客户端对象和引擎](client-objects-and-the-engine.md)。

 

### <a name="span-idremotedataspanspan-idremotedataspanremote-data"></a><span id="remote_data"></span><span id="REMOTE_DATA"></span>远程数据

应使用类来处理远程数据[ **ExtRemoteData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/engextcpp/nl-engextcpp-extremotedata)。 此类是包装的目标内存一小部分。 **ExtRemoteData**自动检索内存并封装与引发方法的其他常见请求。

### <a name="span-idremotetypeddataspanspan-idremotetypeddataspanremote-typed-data"></a><span id="remote_typed_data"></span><span id="REMOTE_TYPED_DATA"></span>远程类型化的数据

如果远程数据的类型已知的它应处理使用[ **ExtRemoteTyped** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/engextcpp/nl-engextcpp-extremotetyped)类。 此类是了解符号的类型信息与类型化的数据的增强的远程数据对象。 它将初始化为特定对象的符号或强制转换，此后它可以像使用给定类型的对象。

### <a name="span-idremotelistsspanspan-idremotelistsspanremote-lists"></a><span id="remote_lists"></span><span id="REMOTE_LISTS"></span>远程列表

若要处理远程列表，请使用[ **ExtRemoteList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/engextcpp/nl-engextcpp-extremotelist)类。 此类可用于单向链接或双向链接列表。 如果列表双向链表，假定的上一个指针紧随的下一个指针。 类包含可以循环访问列表并检索向前和向后的节点的方法。 **ExtRemoteList**还可以使用的以 null 结尾或循环列表。

### <a name="span-idremotetypedlistsspanspan-idremotetypedlistsspanremote-typed-lists"></a><span id="remote_typed_lists"></span><span id="REMOTE_TYPED_LISTS"></span>远程类型化的列表

若要处理远程列表的列表中的节点类型已知时，使用[ **ExtRemoteTypedList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/engextcpp/nl-engextcpp-extremotetypedlist)类。 这是增强的版本[ **ExtRemoteList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/engextcpp/nl-engextcpp-extremotelist)。 除了基本的功能**ExtRemoteList**， **ExtRemoteTypedList**自动确定链接偏移量的类型信息。

 

 





