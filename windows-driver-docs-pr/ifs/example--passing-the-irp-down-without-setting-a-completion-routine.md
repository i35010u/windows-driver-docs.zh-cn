---
title: 向下传递 IRP，而无需设置完成例程的示例
description: 向下传递 IRP，而无需设置完成例程的示例
ms.assetid: d18d3ead-2cec-4ea6-ac4c-b809ba985f23
keywords:
- IRP 调度例程 WDK 文件系统中，向下传递 IRP
- 将 Irp 传递下设备堆栈 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9481232d077b660dda31d845885bcad57ad53a7f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386092"
---
# <a name="example-passing-the-irp-down-without-setting-a-completion-routine"></a>例如：向下传递 IRP，不需设置完成例程


## <span id="ddk_example_passing_the_irp_down_without_setting_a_completion_routine_"></span><span id="DDK_EXAMPLE_PASSING_THE_IRP_DOWN_WITHOUT_SETTING_A_COMPLETION_ROUTINE_"></span>


若要传递到较低级别的驱动程序 IRP 而无需设置完成例程，调度例程必须执行以下操作：

-   调用[ **IoSkipCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)若要删除当前 IRP 堆栈的位置，以便在完成例程执行完成处理 IRP 上时将不查找 I/O 管理器。

-   调用[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)要传递到下一步的较低级驱动程序 IRP。

下面的代码示例说明了这种方法：

```cpp
IoSkipCurrentIrpStackLocation ( Irp ); 
return IoCallDriver ( NextLowerDriverDeviceObject, Irp ); 
```

或者，也可以说：

```cpp
IoSkipCurrentIrpStackLocation ( Irp ); 
status = IoCallDriver ( NextLowerDriverDeviceObject, Irp ); 
/* log or debugprint the status value here */
return status; 
```

在这些示例中，对的调用中的第一个参数[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)指向下一个较低级别筛选器驱动程序的设备对象的指针。 第二个参数是指向 IRP。

### <a name="span-idadvantagesofthisapproachspanspan-idadvantagesofthisapproachspanspan-idadvantagesofthisapproachspanadvantages-of-this-approach"></a><span id="Advantages_of_This_Approach"></span><span id="advantages_of_this_approach"></span><span id="ADVANTAGES_OF_THIS_APPROACH"></span>此方法的优点

如上所示的方法 (调用[ **IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)) 简单且有效，因此应在所有情况下，其中该驱动程序将驱动程序堆栈的下层 IRP 传递而无需注册完成例程。

### <a name="span-iddisadvantagesofthisapproachspanspan-iddisadvantagesofthisapproachspanspan-iddisadvantagesofthisapproachspandisadvantages-of-this-approach"></a><span id="Disadvantages_of_This_Approach"></span><span id="disadvantages_of_this_approach"></span><span id="DISADVANTAGES_OF_THIS_APPROACH"></span>这种方法的缺点

之后[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)调用时，传递给 IRP 指针**IoCallDriver**不再有效，不能安全地取消引用。 如果该驱动程序需要对其执行进一步处理或清理 IRP 处理的较低级驱动程序后，它必须发送驱动程序堆栈的下层 IRP 之前设置完成例程。 有关编写和设置完成例程的详细信息，请参阅[使用完成例程](using-irp-completion-routines.md)。

如果您调用[ **IoSkipCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)的 IRP，您不能完成例程为其设置。

 

 




