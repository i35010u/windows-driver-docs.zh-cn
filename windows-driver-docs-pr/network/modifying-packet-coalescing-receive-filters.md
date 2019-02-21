---
title: 修改数据包合并接收筛选器
description: 修改数据包合并接收筛选器
ms.assetid: 082A969F-2977-482A-B060-ED8D353EC2E9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be351199b52214ac3c72f8b07518bdecc2813a8a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540950"
---
# <a name="modifying-packet-coalescing-receive-filters"></a>修改数据包合并接收筛选器


若要修改支持数据包合并的微型端口驱动程序上的接收筛选器，基础协议或筛选器驱动程序，请执行以下步骤：

1.  若要获取所有数据包合并接收的列表的已下载到微型端口驱动程序筛选器，基础驱动程序将发出的 OID 方法请求[OID\_接收\_筛选器\_枚举\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569787)。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_接收\_筛选器\_信息\_数组**](https://msdn.microsoft.com/library/windows/hardware/ff567179)结构。

    **请注意**过量的驱动程序或应用程序时初始化[ **NDIS\_接收\_筛选器\_信息\_数组**](https://msdn.microsoft.com/library/windows/hardware/ff567179)结构，它必须设置**QueueId**成员添加到 NDIS\_默认\_接收\_队列\_id。

    从 OID 方法请求的成功返回后[OID\_接收\_筛选器\_枚举\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569787)，则**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含的指针的已更新[ **NDIS\_接收\_筛选器\_INFO\_数组**](https://msdn.microsoft.com/library/windows/hardware/ff567179)后跟一个或多个结构[ **NDIS\_接收\_筛选器\_信息** ](https://msdn.microsoft.com/library/windows/hardware/ff567176)结构。 每个**NDIS\_接收\_筛选器\_信息**结构指定的筛选器，在网络适配器上设置的标识符 (ID)。

2.  若要获取特定的数据包的参数合并接收已下载到微型端口驱动程序的基础驱动程序问题 OID 方法请求的筛选器[OID\_接收\_筛选器\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569792). **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181)结构。 过量的驱动程序或应用程序初始化**NDIS\_接收\_筛选器\_参数**结构通过设置**FilterId**成员为非零 ID其参数位于要返回的筛选器值。

    通过 OID 方法请求成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含指向缓冲区的指针。 此缓冲区已格式化为包含以下信息：

    -   [ **NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181) NDIS 接收筛选器指定的参数的结构。

    -   一个数组[ **NDIS\_接收\_筛选器\_字段\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567169)结构指定的筛选器测试条件中的一个字段网络数据包标头。

3.  基础驱动程序将修改要添加、 删除或更改的测试条件的筛选器集的接收筛选器。 通过添加、 删除或修改单个的驱动程序实现这[ **NDIS\_接收\_筛选器\_字段\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567169)从结构指定的字段参数数组[ **NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181)结构。

    基础驱动程序完成后对测试条件进行修改，它必须更新的成员[ **NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181)结构，以反映对接收筛选器所做的更改。 例如，基础驱动程序必须更新**FieldParametersArrayNumElements**成员，以包含新的数组中的元素数。

    有关详细信息，请参阅[指定一个数据包合并接收筛选器](specifying-a-packet-coalescing-receive-filter.md)。

4.  基础驱动程序发出的 OID 方法请求[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)微型端口驱动程序下载已修改的接收筛选器。

    有关详细信息，请参阅[设置数据包合并接收筛选器](setting-a-packet-coalescing-receive-filter.md)。









