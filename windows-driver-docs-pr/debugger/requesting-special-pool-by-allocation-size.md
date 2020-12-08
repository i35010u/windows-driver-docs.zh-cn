---
title: 按分配大小请求特殊池
description: 按分配大小请求特殊池
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcd371003292d9b332f25c9d81cf800eac2773cd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824280"
---
# <a name="requesting-special-pool-by-allocation-size"></a>按分配大小请求特殊池


## <span id="ddk_requesting_special_pool_for_allocations_of_a_specified_size_dtools"></span><span id="DDK_REQUESTING_SPECIAL_POOL_FOR_ALLOCATIONS_OF_A_SPECIFIED_SIZE_DTOOLS"></span>


可以请求特定大小范围内的分配的特殊池。

在 Windows Vista 和更高版本的 Windows 中，还可以使用命令行来请求按池标记的特殊池。 有关信息，请参阅 [**GFlags 命令**](gflags-commands.md)。

**注意**   此方法对于诊断驱动程序错误很少有用，因为它会影响指定大小的所有内核池请求，而不管请求分配的是哪个驱动程序或内核模块。

 

### <a name="span-idto_request_special_pool_by_allocation_sizespanspan-idto_request_special_pool_by_allocation_sizespanto-request-special-pool-by-allocation-size"></a><span id="to_request_special_pool_by_allocation_size"></span><span id="TO_REQUEST_SPECIAL_POOL_BY_ALLOCATION_SIZE"></span>请求分配大小的特殊池

1.  选择 " **系统注册表** " 选项卡或 " **内核标志** " 选项卡。

    在 Windows Vista 和更高版本的 Windows 上，此选项在两个选项卡上都可用。 在早期版本的 Windows 上，它仅在 " **系统注册表** " 选项卡上可用。

2.  在 " **内核特殊池标记** " 部分中，单击 " **Hex**"，然后以十六进制格式键入一个表示大小范围的数字。 将从特殊池分配此大小范围内的所有分配。 此数字必须小于页面 \_ 大小。

3.  单击“应用” 。

    以下屏幕截图显示了以十六进制值的形式输入的分配大小。

    ![屏幕截图，显示输入为十六进制值的分配大小](images/gflags-specialpool-size.png)

 

 





