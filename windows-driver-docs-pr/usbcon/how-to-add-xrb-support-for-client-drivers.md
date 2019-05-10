---
Description: 本主题介绍 USB 客户端驱动程序如何使用 Windows 驱动程序模型 (WDM) 驱动程序例程来分配和设置 URB 格式之前将请求发送到由 Microsoft 提供的 USB 驱动程序堆栈。
title: 分配和构建 URB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d09e3df17b36199ecae09fd6ffcaaaf7a19d763e
ms.sourcegitcommit: 0504cc497918ebb7b41a205f352046a66c0e26a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2019
ms.locfileid: "65405049"
---
# <a name="allocating-and-building-urbs"></a>分配和构建 URB

USB 客户端驱动程序可以使用 Windows 驱动程序模型 (WDM) 驱动程序例程来分配和设置 URB 格式之前将请求发送到由 Microsoft 提供的 USB 驱动程序堆栈。

客户端驱动程序使用 URB 包中的 USB 驱动程序堆栈的较低的驱动程序将处理请求所需的所有信息。 在 Windows 操作系统，URB 中所述[ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)结构。

Microsoft 可提供大量[USB 客户端驱动程序例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#client)。 使用这些例程，USB 客户端驱动程序可以生成 URB 为特定的指定操作的请求，并将其转发下 USB 堆栈。 如果您愿意，您可以设计您的客户端驱动程序支持的操作，而无需构建自己的 URB 请求调用库例程。

## <a name="urb-allocation-in-windows7-and-earlier"></a>在 Windows 7 及更早版本的 URB 分配

若要使用 Windows Driver Kit (WDK) 中包含的 Windows 7 和 Windows 的早期版本的例程发送 USB 请求，客户端驱动程序通常会分配并填充[ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)结构，关联**URB**与新的 IRP，并将其发送到 USB 驱动程序堆栈 IRP 的结构。

对于某些类型的请求，Microsoft 提供的帮助器例程 （通过 Usbd.sys 已导出） 分配和格式[ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)结构。 例如， [ **USBD\_CreateConfigurationRequestEx** ](https://msdn.microsoft.com/library/windows/hardware/ff539029)例程分配的内存**URB**结构，格式为 URB选择配置请求，并返回的地址**URB**到客户端驱动程序的结构。 但是，帮助器例程不能用于所有类型的请求。

Microsoft 还提供了格式 URBs 对于某些类型的请求的宏。 客户端驱动程序必须对这些宏分配[ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)结构通过调用[ **ExAllocatePoolWithTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544520)或分配在堆栈上的结构。 例如，在客户端驱动程序分配**URB**，该驱动程序可以调用[ **UsbBuildSelectConfigurationRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff538968)设置选择配置 URB 的格式请求或以清除配置。

为其他请求的客户端驱动程序必须分配并通过设置的各个成员手动格式化 URB [ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)结构，具体取决于请求类型。

USB 请求完成后，客户端驱动程序必须释放[ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)结构。 如果 URB 在堆栈上分配，超出范围时释放 URB。 如果 URB 中非分页缓冲池分配，必须调用客户端驱动程序[ **ExFreePool** ](https://msdn.microsoft.com/library/windows/hardware/ff544590)释放 URB。

## <a name="urb-allocation-in-windows8"></a>Windows 8 中 URB 分配

Windows 8 的 WDK 提供了一个新的静态库，Usbdex.lib，可以将导出的分配、 格式设置，并释放 URBs 例程。 此外，还有一种将 URB 与 IRP 相关联的新方法。 新的例程可由面向 Windows Vista 和更高版本的 Windows 客户端驱动程序调用。

运行 Windows Vista 及更高版本的客户端驱动程序必须使用新的例程，以使基础的 USB 驱动程序堆栈可以利用某些性能和可靠性的改进。 这些改进适用于 Windows 8，以支持 USB 3.0 设备和主机控制器中引入新的 USB 驱动程序堆栈。 对于 USB 2.0 主机控制器，Windows 将加载早期版本的驱动程序堆栈不支持的改进。 而不考虑基础驱动程序堆栈的版本或在主机控制器支持的协议版本，您必须始终调用新 URB 例程。

在调用任何新的例程之前，请确保您的客户端驱动程序注册与 USB 驱动程序堆栈具有 USBD 句柄。 若要获取 USBD 句柄，请调用[ **USBD\_CreateHandle**](https://msdn.microsoft.com/library/windows/hardware/hh406241)。

以下例程是适用于 Windows 8 的 WDK。 这些例程 Usbdlib.h 中定义。

* [**USBD\_UrbAllocate**](https://msdn.microsoft.com/library/windows/hardware/hh406250)
* [**USBD\_IsochUrbAllocate**](https://msdn.microsoft.com/library/windows/hardware/hh406231)
* [**USBD\_SelectConfigUrbAllocateAndBuild**](https://msdn.microsoft.com/library/windows/hardware/hh406243)
* [**USBD\_SelectInterfaceUrbAllocateAndBuild**](https://msdn.microsoft.com/library/windows/hardware/hh406245)
* [**USBD\_UrbFree**](https://msdn.microsoft.com/library/windows/hardware/hh406252)
* [**USBD\_AssignUrbToIoStackLocation**](https://msdn.microsoft.com/library/windows/hardware/hh406228)

上面的列表中的分配例程返回到新指针[ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923) USB 驱动程序堆栈分配的结构。 具体取决于版本的 Windows，通过加载 USB 驱动程序堆栈**URB**结构可以搭配一个不透明*URB 上下文*。 URB 上下文是信息的 URB 有关块。 不能查看 URB 标头; 的内容信息旨在供在内部 USB 驱动程序堆栈来提高 URB 跟踪和处理。 URB 上下文*仅*由 for Windows 8 的 USB 驱动程序堆栈。
如果 URB 上下文不可用，USB 驱动程序堆栈将使用它来使 URB 处理更安全更有效。 例如，USB 驱动程序堆栈必须确保客户端驱动程序不会不提交 URB，然后尝试重复使用该相同 URB 之前已完成第一个请求。 若要检测这种错误，USB 驱动程序堆栈 URB 上下文中存储状态信息。 不包含状态信息，需要比较与当前正在进行的所有 URBs 传入 URB USB 驱动程序堆栈。 当客户端驱动程序会尝试释放 URB USB 驱动程序堆栈也使用的状态信息。 释放 URB 前, USB 驱动程序堆栈验证以确保 URB 未挂起状态。

URB 上下文提供了正式的机制，用于存储额外 URB 信息。 使用 URB 上下文是为所需或存储的额外信息的保留成员中分配额外的内存比更可取[ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)结构。 USB 驱动程序堆栈分配 URBs 和其关联的 URB 上下文中，非分页池，以便在将来如果需要更大 URB 上下文，唯一需要进行调整将池分配的大小。

## <a name="urb-routine-migration"></a>URB 例程迁移

下表总结了 URB 例程中的更改。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>用例</th>
<th>可用在 WDK 适用于 Windows 7 及更早版本</th>
<th>适用于 Windows 8 的 WDK 中可用</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td></td>
<td>面向 Windows 7 及更早版本的操作系统</td>
<td>面向 Windows Vista 和更高版本的操作系统</td>
</tr>
<tr class="even">
<td>若要创建 URB...</td>
<td>客户端驱动程序分配<a href="https://msdn.microsoft.com/library/windows/hardware/ff538923" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538923)"> <strong>URB</strong> </a>结构和格式根据请求的结构。
<p>客户端驱动程序分配到堆栈上，URB 结构或驱动程序通过调用分配中非分页缓冲池的结构<a href="https://msdn.microsoft.com/library/windows/hardware/ff544520" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithTag&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544520)"> <strong>ExAllocatePoolWithTag</strong></a>。</p></td>
<td>客户端驱动程序调用<a href="https://msdn.microsoft.com/library/windows/hardware/hh406250" data-raw-source="[&lt;strong&gt;USBD_UrbAllocate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406250)"> <strong>USBD_UrbAllocate</strong> </a> ，并接收一个指向新<a href="https://msdn.microsoft.com/library/windows/hardware/ff538923" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538923)"> <strong>URB</strong> </a>结构，它通过 USB 分配驱动程序堆栈。 URB 可能不 URB 上下文中，具体取决于基础的 USB 驱动程序堆栈 USBD 接口版本与相关联。</td>
</tr>
<tr class="odd">
<td>若要创建选择配置请求 URB...</td>
<td>客户端驱动程序调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff539029" data-raw-source="[&lt;strong&gt;USBD_CreateConfigurationRequestEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539029)"> <strong>USBD_CreateConfigurationRequestEx</strong> </a>返回一个指向新 URB 中创建并格式化 USB 驱动程序堆栈的例程。</td>
<td>客户端驱动程序调用<a href="https://msdn.microsoft.com/library/windows/hardware/hh406243" data-raw-source="[&lt;strong&gt;USBD_SelectConfigUrbAllocateAndBuild&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406243)"> <strong>USBD_SelectConfigUrbAllocateAndBuild</strong> </a> ，并接收一个指向新<a href="https://msdn.microsoft.com/library/windows/hardware/ff538923" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538923)"> <strong>URB</strong> </a>结构，它是分配和格式化 （用于选择配置请求） 的 USB 驱动程序堆栈。 URB 可能不 URB 上下文中，具体取决于基础的 USB 驱动程序堆栈 USBD 接口版本与相关联。</td>
</tr>
<tr class="even">
<td>若要创建一个选择接口请求 URB...</td>
<td>客户端驱动程序分配<a href="https://msdn.microsoft.com/library/windows/hardware/ff538923" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538923)"> <strong>URB</strong> </a>结构，并使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff540425" data-raw-source="[&lt;strong&gt;_URB_SELECT_INTERFACE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540425)"> <strong>_URB_SELECT_INTERFACE</strong> </a>结构，用于定义 select 的格式USB 设备的界面命令。</td>
<td>客户端驱动程序调用<a href="https://msdn.microsoft.com/library/windows/hardware/hh406245" data-raw-source="[&lt;strong&gt;USBD_SelectInterfaceUrbAllocateAndBuild&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406245)"> <strong>USBD_SelectInterfaceUrbAllocateAndBuild</strong> </a> ，并接收一个指向新<a href="https://msdn.microsoft.com/library/windows/hardware/ff538923" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538923)"> <strong>URB</strong> </a>结构，其中分配和格式化 （用于选择接口请求） 的 USB 驱动程序堆栈。 URB 可能不 URB 上下文中，具体取决于基础的 USB 驱动程序堆栈 USBD 接口版本与相关联。</td>
</tr>
<tr class="odd">
<td>要与 IRP 关联 URB...</td>
<td>客户端驱动程序通过调用下一步的 IRP 堆栈位置获取指向<a href="https://msdn.microsoft.com/library/windows/hardware/ff549266" data-raw-source="[&lt;strong&gt;IoGetNextIrpStackLocation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549266)"> <strong>IoGetNextIrpStackLocation</strong></a>。 然后客户端驱动程序手动设置<strong>Parameters.Others.Argument1</strong>成员的地址的堆栈位置<a href="https://msdn.microsoft.com/library/windows/hardware/ff538923" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538923)"> <strong>URB</strong> </a>结构。</td>
<td>客户端驱动程序通过调用下一步的 IRP 堆栈位置获取指向<a href="https://msdn.microsoft.com/library/windows/hardware/ff549266" data-raw-source="[&lt;strong&gt;IoGetNextIrpStackLocation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549266)"> <strong>IoGetNextIrpStackLocation</strong></a>。 然后客户端驱动程序调用<a href="https://msdn.microsoft.com/library/windows/hardware/hh406228" data-raw-source="[&lt;strong&gt;USBD_AssignUrbToIoStackLocation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406228)"> <strong>USBD_AssignUrbToIoStackLocation</strong> </a>要关联的堆栈位置 URB。</td>
</tr>
<tr class="even">
<td>若要释放 URB...</td>
<td>如果客户端驱动程序分配到堆栈上的 URB，变量会超出范围后请求已完成。
<p>若要释放 URB 结构的客户端驱动程序或 USB 驱动程序堆栈中，非分页池分配客户端驱动程序调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff544590" data-raw-source="[&lt;strong&gt;ExFreePool&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544590)"> <strong>ExFreePool</strong></a>。</p></td>
<td>客户端驱动程序调用<a href="https://msdn.microsoft.com/library/windows/hardware/hh406252" data-raw-source="[&lt;strong&gt;USBD_UrbFree&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406252)"> <strong>USBD_UrbFree</strong></a>。</td>
</tr>
</tbody>
</table>

## <a name="related-topics"></a>相关主题

[将请求发送到 USB 设备](communicating-with-a-usb-device.md)  
