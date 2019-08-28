---
title: 数据集管理 (DSM) 概述
description: '可以对设备的数据集属性执行管理操作, 如数据集管理 (DSM) 操作。: "？ASQ'
ms.assetid: cc64c7ad-7d1c-45c7-b236-a43e57086f8d
keywords: 存储数据设置管理操作, 数据设置管理操作, DSM 操作
ms.localizationpriority: medium
ms.date: 08/23/2019
ms.openlocfilehash: 8196ac4e1577fbaef1789b42ac2ead6b36bd5295
ms.sourcegitcommit: 238308264c1ee2c74ec0c8c303258dc00c79b902
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2019
ms.locfileid: "70076027"
---
# <a name="data-set-management-dsm-overview"></a>数据集管理 (DSM) 概述

从 Windows 7 开始, 驱动程序可以对设备的数据集执行管理操作。 DSM 操作由 Microsoft 定义。

[DEVICE_DSM_ACTION](device-dsm-action-descriptions.md)常量指定操作。 此常量传入[IOCTL_STORAGE_MANAGE_DATA_SET_ATTRIBUTES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_manage_data_set_attributes)请求的系统缓冲区所包含的[DEVICE_DSM_INPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_manage_data_set_attributes)结构的**操作**成员。 如果该操作需要其他参数, 则参数块会立即遵循 DEVICE_DSM_INPUT 结构, 并且**ParameterBlockOffset**将指定从 DEVICE_DSM_INPUT 结构开始的偏移量, 在该位置的参数块起. 数据集范围 (如果有) 将紧跟在参数块之后, **DataSetRangesOffset**将指定从 DEVICE_DSM_INPUT 结构开始的偏移量, 范围从此处开始。 下图显示了系统缓冲区的结构。

![DSM IOCTL 输入缓冲区](images/dsm_ioctl_inputbuffer.jpg)

如果管理操作将返回 output, 则会在 IOCTL 的*OutputBuffer*中传递一个指向[DEVICE_DSM_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_manage_data_set_attributes_output)结构的指针。 如果该操作将返回其他特定于操作的输出, 则输出块会立即遵循 DEVICE_DSM_OUTPUT 结构, 并且**OutputBlockOffset**将指定从 DEVICE_DSM_OUTPUT 结构开始处的偏移量, 其中参数块开始。 下图显示了输出缓冲区结构。

![DSM IOCTL 输出缓冲区](images/dsm_ioctl_outputbuffer.jpg)

下面介绍了 DSM 的处理流程, 其中*发送方*是操作请求者,*处理程序*处理请求的操作。 请注意, 堆栈中可以有多个*处理程序*。

![DSM 操作流](images/dsm_action_flow.jpg)

1) *发件人*初始化 DSM, 并通过执行以下操作将其发送到堆栈中的第一个*处理程序*:

   - 使用与操作关联的定义来分配和初始化[DEVICE_DSM_DEFINITION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_dsm_definition)结构。
   - 调用[**DeviceDsmGetInputLength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/nf-ntddstor-devicedsmgetinputlength)以确定操作的输入缓冲区所需的大小, 然后为此缓冲区分配内存。
   - 调用[**DeviceDsmInitializeInput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/nf-ntddstor-devicedsminitializeinput)来初始化[DSM_DEVICE_INPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_manage_data_set_attributes)结构, 如果该操作具有参数, 则为参数块。 参数块的格式取决于操作。 有关更多详细信息, 请参阅[DEVICE_DSM_ACTION 说明](device-dsm-action-descriptions.md)。
   - 如果操作具有范围, 请为每个范围调用[**DeviceDsmAddDataSetRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/nf-ntddstor-devicedsmadddatasetrange) , 将[DEVICE_DSM_RANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_data_set_range)结构添加到输入缓冲区。
   - 如果 DSM 有输出, 请调用[**DeviceDsmGetOutputLength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/nf-ntddstor-devicedsmgetoutputlength)来确定操作的输出缓冲区所需的大小, 然后为此缓冲区分配内存。
   - 发送[IOCTL_STORAGE_MANAGE_DATA_SET_ATTRIBUTES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_manage_data_set_attributes)请求, 在 IOCTL 的系统缓冲区中传递已初始化的输入数据, 以及分配的输出缓冲区 (如果有)。

2) *处理程序*通过以下三种方式之一处理 DSM IOCTL 请求:
   1) 处理请求并返回 output (如果有)。
   2) 处理请求并将其转发到堆栈中的下一个较低的驱动程序。
   3) 将请求转发到堆栈中的下一个较低的驱动程序, 而不处理 DSM。

   > [!NOTE]
   > 无论驱动程序是否处理 DSM,*只要*设置了 DEVICE_DSM_ACTION's 的最高有效位 (**DeviceDsmActionFlag_NonDestructive**), 就可以安全地转发请求。 如果*未*设置**DeviceDsmActionFlag_NonDestructive** , 则驱动程序应返回并返回错误。
  
   如果*处理程序*处理 DSM, 它将执行以下步骤:

   - 通过调用[**DeviceDsmValidateInput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/nf-ntddstor-devicedsmvalidateinput)验证输入。
   - 如果输入有效,*处理程序*将提取输入来获取操作。 如果操作具有参数块, 则*处理程序*将调用[**DeviceDsmParameterBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/nf-ntddstor-devicedsmparameterblock)以获取参数块。 如果该操作具有范围数据, 则*处理程序*将调用[**DeviceDsmDataSetRanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/nf-ntddstor-devicedsmdatasetranges)以获取指向数据集范围的块的指针, 然后在块上执行常规处理。 此块位于**DataSetRangesOffset** , 其中包含一个或多个连续条目, 格式为[DEVICE_DSM_RANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_data_set_range)结构。 数据集范围的长度 (以字节为单位) 是在[DEVICE_DSM_INPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_manage_data_set_attributes)的**DataSetRangesLength**成员中设置的。
   - 如果操作需要 output, 则*处理程序*将调用[**DeviceDsmValidateOutputLength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/nf-ntddstor-devicedsmvalidateoutputlength)来验证发送方提供的输出缓冲区。 如果有效, 处理程序将通过调用[**DeviceDsmInitializeOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/nf-ntddstor-devicedsminitializeoutput)初始化输出缓冲区的[DEVICE_DSM_OUTPUT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_device_manage_data_set_attributes_output)部分, 并使用特定于操作的输出 (如果有) 填充输出块。 然后,*处理程序*将完成 ioctl, 并将 ioctl 返回或转发到堆栈中的下一个驱动程序。

3) 一旦对 DSM 进行处理并返回给*发件人*,*发送方*就会通过调用[**DeviceDsmValidateOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/nf-ntddstor-devicedsmvalidateoutput)来验证输出 (如果有)。 如果输出有效, 则*发送方*通过调用[**DeviceDsmOutputBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/nf-ntddstor-devicedsmoutputblock)来提取输出块 (如果有)。

有关每个特定 DSM 操作的详细信息, 请参阅[设备 DSM 操作说明](device-dsm-action-descriptions.md)。
