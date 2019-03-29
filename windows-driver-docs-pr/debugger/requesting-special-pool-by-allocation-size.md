---
title: 按分配大小请求特殊池
description: 按分配大小请求特殊池
ms.assetid: 040d1a1a-1849-4253-8d4b-6c57a8643225
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7196325fc1c0558a210e2827cb0d211b703c7613
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577534"
---
# <a name="requesting-special-pool-by-allocation-size"></a>按分配大小请求特殊池


## <span id="ddk_requesting_special_pool_for_allocations_of_a_specified_size_dtools"></span><span id="DDK_REQUESTING_SPECIAL_POOL_FOR_ALLOCATIONS_OF_A_SPECIFIED_SIZE_DTOOLS"></span>


你可以请求特殊池分配指定的大小范围内。

在 Windows Vista 和更高版本的 Windows 中，还可以使用命令行来请求特殊标记，池的池。 有关信息，请参阅[ **GFlags 命令**](gflags-commands.md)。

**请注意**  此方法是很少用于诊断驱动程序错误，因为它会影响所有内核池请求指定的大小，而不考虑哪些驱动程序或内核模块请求分配。

 

### <a name="span-idtorequestspecialpoolbyallocationsizespanspan-idtorequestspecialpoolbyallocationsizespanto-request-special-pool-by-allocation-size"></a><span id="to_request_special_pool_by_allocation_size"></span><span id="TO_REQUEST_SPECIAL_POOL_BY_ALLOCATION_SIZE"></span>若要请求特殊池的分配大小

1.  选择**系统注册表**选项卡或**内核标志**选项卡。

    在 Windows Vista 和更高版本的 Windows 上，此选项才可用两个选项卡。 在早期版本的 Windows，它是仅适用于**系统注册表**选项卡。

2.  在中**内核特殊池标记**部分中，单击**Hex**，然后键入一个数字以十六进制格式表示一系列的大小。 将通过特殊的池分配此大小范围内的所有分配。 此数字必须小于页面\_大小。

3.  单击 **“应用”**。

    下面的屏幕截图显示了输入为十六进制值的分配大小。

    ![屏幕截图，显示输入为十六进制值的分配大小](images/gflags-specialpool-size.png)

 

 





