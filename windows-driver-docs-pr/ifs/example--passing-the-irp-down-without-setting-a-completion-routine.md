---
title: 示例将 IRP 向下传递而不设置完成例程
description: 示例将 IRP 向下传递而不设置完成例程
ms.assetid: d18d3ead-2cec-4ea6-ac4c-b809ba985f23
keywords:
- IRP 调度例程 WDK 文件系统，并将 IRP 向下传递
- 将 Irp 向下传递设备堆栈 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1131329767e984830a50e2f7949a1e4465ce719
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841425"
---
# <a name="example-passing-the-irp-down-without-setting-a-completion-routine"></a>示例：将 IRP 向下传递而不设置完成例程


## <span id="ddk_example_passing_the_irp_down_without_setting_a_completion_routine_"></span><span id="DDK_EXAMPLE_PASSING_THE_IRP_DOWN_WITHOUT_SETTING_A_COMPLETION_ROUTINE_"></span>


若要将 IRP 向下传递到较低级别的驱动程序而不设置完成例程，调度例程必须执行以下操作：

-   调用[**IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)以删除当前的 irp 堆栈位置，以便在执行 IRP 上的完成处理时，I/o 管理器不会查找完成例程。

-   调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) ，将 IRP 向下传递到下一个较低级别的驱动程序。

下面的代码示例演示了此方法：

```cpp
IoSkipCurrentIrpStackLocation ( Irp ); 
return IoCallDriver ( NextLowerDriverDeviceObject, Irp ); 
```

或等效：

```cpp
IoSkipCurrentIrpStackLocation ( Irp ); 
status = IoCallDriver ( NextLowerDriverDeviceObject, Irp ); 
/* log or debugprint the status value here */
return status; 
```

在这些示例中，调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)的第一个参数是指向下一级筛选器驱动程序的设备对象的指针。 第二个参数是指向 IRP 的指针。

### <a name="span-idadvantages_of_this_approachspanspan-idadvantages_of_this_approachspanspan-idadvantages_of_this_approachspanadvantages-of-this-approach"></a><span id="Advantages_of_This_Approach"></span><span id="advantages_of_this_approach"></span><span id="ADVANTAGES_OF_THIS_APPROACH"></span>此方法的优点

上面所示的方法（调用[**IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)）简单有效，应在驱动程序将 IRP 向下传递到驱动程序堆栈的所有情况下使用，而无需注册完成例程。

### <a name="span-iddisadvantages_of_this_approachspanspan-iddisadvantages_of_this_approachspanspan-iddisadvantages_of_this_approachspandisadvantages-of-this-approach"></a><span id="Disadvantages_of_This_Approach"></span><span id="disadvantages_of_this_approach"></span><span id="DISADVANTAGES_OF_THIS_APPROACH"></span>此方法的缺点

调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)后，传递到**IoCallDriver**的 IRP 指针将不再有效，因此无法安全地取消引用。 如果在由较低级别的驱动程序处理 IRP 之后，驱动程序需要执行进一步的处理或清理，则必须先设置完成例程，然后再将 IRP 发送到驱动程序堆栈。 有关编写和设置完成例程的详细信息，请参阅[使用完成例程](using-irp-completion-routines.md)。

如果为 IRP 调用[**IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) ，则不能为其设置完成例程。

 

 




