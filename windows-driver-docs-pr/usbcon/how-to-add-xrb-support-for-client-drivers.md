---
Description: 本主题介绍在将请求发送到 Microsoft 提供的 USB 驱动程序堆栈之前，USB 客户端驱动程序如何使用 Windows 驱动模型（WDM）驱动程序例程来分配 URB 并设置其格式。
title: 分配和构建 URB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 936cae4b8e442700432ea58b487b813342922f90
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844996"
---
# <a name="allocating-and-building-urbs"></a>分配和构建 URB

在将请求发送到 Microsoft 提供的 USB 驱动程序堆栈之前，USB 客户端驱动程序可以使用 Windows 驱动模型（WDM）驱动程序例程来分配 URB 并设置其格式。

客户端驱动程序使用 URB 对 USB 驱动程序堆栈中较低驱动程序所需的所有信息进行打包，以处理该请求。 在 Windows 操作系统中， [**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)结构中描述了 URB。

Microsoft[为 USB 客户端驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#client)提供了一个例程库。 通过使用这些例程，USB 客户端驱动程序可以为某些指定的操作生成 URB 请求，并将其沿 USB stack 向下转发。 如果需要，可以将客户端驱动程序设计为调用受支持操作的库例程，而不是生成你自己的 URB 请求。

## <a name="urb-allocation-in-windows7-and-earlier"></a>Windows 7 和更早版本中的 URB 分配

若要通过使用 windows 7 和更早版本的 windows 驱动程序工具包（WDK）中包含的例程来发送 USB 请求，客户端驱动程序通常会分配并填充[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)结构，将**URB**结构与新的 IRP 关联，并将 irp 发送到到 USB 驱动程序堆栈。

对于某些类型的请求，Microsoft 提供了可分配和格式化[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)结构的帮助程序例程（由 Usbd 导出）。 例如， [**USBD\_CreateConfigurationRequestEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createconfigurationrequestex)例程为**URB**结构分配内存，为选择配置请求设置 URB 的格式，并将**URB**结构的地址返回到客户端驱动程序。 但是，帮助程序例程不能用于所有类型的请求。

Microsoft 还提供了一些宏，用于为某些类型的请求设置 URBs 的格式。 对于这些宏，客户端驱动程序必须通过调用[**ExAllocatePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)或在堆栈上分配结构来分配[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)结构。 例如，在客户端驱动程序分配了**URB**之后，驱动程序可以调用[**UsbBuildSelectConfigurationRequest**](https://docs.microsoft.com/previous-versions/ff538968(v=vs.85))来格式化选择配置请求的 URB 或清除配置。

对于其他请求，客户端驱动程序必须通过设置[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)结构的各个成员（具体取决于请求类型），手动分配 URB 并设置其格式。

当 USB 请求完成时，客户端驱动程序必须释放[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)结构。 如果在堆栈上分配 URB，则当 URB 超出范围时，将释放该。 如果 URB 是在非分页池中分配的，则客户端驱动程序必须调用[**ExFreePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)以释放 URB。

## <a name="urb-allocation-in-windows8"></a>Windows 8 中的 URB 分配

适用于 Windows 8 的 WDK 提供了一个新的静态库 Usbdex，用于导出用于分配、格式化和释放 URBs 的例程。 此外，还提供了一种将 URB 与 IRP 关联的新方法。 对于面向 Windows Vista 和更高版本的 Windows 的客户端驱动程序，可以调用新的例程。

在 Windows Vista 和更高版本上运行的客户端驱动程序必须使用新例程，以便基础 USB 驱动程序堆栈可以利用某些性能和可靠性改进。 这些改进适用于 Windows 8 中引入的新 USB 驱动程序堆栈，以支持 USB 3.0 设备和主机控制器。 对于 USB 2.0 主机控制器，Windows 将加载早期版本的驱动程序堆栈，该版本不支持改进。 无论底层驱动程序堆栈的版本还是主机控制器支持的协议版本，都必须始终调用新的 URB 例程。

在调用任何新例程之前，请确保你有一个用于客户端驱动程序的 USBD 句柄，并使用 USB 驱动程序堆栈进行注册。 若要获取 USBD 句柄，请调用[**USBD\_CreateHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle)。

适用于 Windows 8 的 WDK 提供以下例程。 这些例程是在 Usbdlib 中定义的。

* [**USBD\_UrbAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate)
* [**USBD\_IsochUrbAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_isochurballocate)
* [**USBD\_SelectConfigUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)
* [**USBD\_SelectInterfaceUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)
* [**USBD\_UrbFree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urbfree)
* [**USBD\_AssignUrbToIoStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_assignurbtoiostacklocation)

前面列表中的分配例程返回指向新的[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)结构的指针，该结构由 USB 驱动程序堆栈分配。 根据 Windows 加载的 USB 驱动程序堆栈的版本，可以将**URB**结构与不透明的*URB 上下文*配对。 URB 上下文是有关 URB 的信息块。 你无法查看 URB 标头的内容;此信息旨在供 USB 驱动程序堆栈内部使用以改进 URB 跟踪和处理。 URB 上下文*仅*用于 Windows 8 的 USB 驱动程序堆栈。
如果 URB 上下文可用，则 USB 驱动程序堆栈将使用它来使 URB 处理更安全、更有效。 例如，USB 驱动程序堆栈必须确保客户端驱动程序不会提交 URB，然后在第一个请求完成之前尝试再次使用同一个 URB。 若要检测此类错误，USB 驱动程序堆栈会将状态信息存储在 URB 上下文中。 如果没有状态信息，USB 驱动程序堆栈就必须将传入的 URB 与所有当前正在进行的 URBs 进行比较。 当客户端驱动程序尝试释放 URB 时，USB 驱动程序堆栈也使用状态信息。 在发布 URB 之前，USB 驱动程序堆栈会验证状态，以确保 URB 不处于挂起状态。

URB 上下文为存储额外的 URB 信息提供了一种官方机制。 如果使用 URB 上下文，则最好是根据需要分配额外的内存，或在[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)结构的保留成员中存储额外的信息。 USB 驱动程序堆栈在非分页池中分配 URBs 及其关联的 URB 上下文，因此，如果需要更大的 URB 上下文，则所需的唯一调整将是池分配的大小。

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
<th>适用于适用于 Windows 7 和更早版本的 WDK</th>
<th>适用于 Windows 8 的 WDK</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td></td>
<td>面向操作系统的 Windows 7 和更早版本</td>
<td>面向 Windows Vista 和更高版本的操作系统</td>
</tr>
<tr class="even">
<td>若要创建 URB 。</td>
<td>客户端驱动程序根据请求分配<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)"><strong>URB</strong></a>结构并设置结构的格式。
<p>客户端驱动程序在堆栈上分配 URB 结构，或通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithTag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)"><strong>ExAllocatePoolWithTag</strong></a>，驱动程序在非分页池分配结构。</p></td>
<td>客户端驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate" data-raw-source="[&lt;strong&gt;USBD_UrbAllocate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate)"><strong>USBD_UrbAllocate</strong></a> ，并收到指向新<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)"><strong>URB</strong></a>结构的指针，该结构由 USB 驱动程序堆栈分配。 根据基础 USB 驱动程序堆栈的 USBD 接口版本，URB 可能与 URB 上下文相关联。</td>
</tr>
<tr class="odd">
<td>为选择配置请求创建 URB 。</td>
<td>客户端驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createconfigurationrequestex" data-raw-source="[&lt;strong&gt;USBD_CreateConfigurationRequestEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createconfigurationrequestex)"><strong>USBD_CreateConfigurationRequestEx</strong></a>例程，该例程返回指向由 USB 驱动程序堆栈创建和格式化的新 URB 的指针。</td>
<td>客户端驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild" data-raw-source="[&lt;strong&gt;USBD_SelectConfigUrbAllocateAndBuild&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)"><strong>USBD_SelectConfigUrbAllocateAndBuild</strong></a> ，并收到指向新<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)"><strong>URB</strong></a>结构的指针，该结构是通过 USB 驱动程序堆栈分配和格式化的（对于选择配置请求）。 根据基础 USB 驱动程序堆栈的 USBD 接口版本，URB 可能与 URB 上下文相关联。</td>
</tr>
<tr class="even">
<td>为选择接口请求创建 URB 。</td>
<td>客户端驱动程序分配一个<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)"><strong>URB</strong></a>结构，并使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_select_interface" data-raw-source="[&lt;strong&gt;_URB_SELECT_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_select_interface)"><strong>_URB_SELECT_INTERFACE</strong></a>结构定义用于 USB 设备的选择接口命令的格式。</td>
<td>客户端驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild" data-raw-source="[&lt;strong&gt;USBD_SelectInterfaceUrbAllocateAndBuild&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)"><strong>USBD_SelectInterfaceUrbAllocateAndBuild</strong></a> ，并接收指向新的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)"><strong>URB</strong></a>结构的指针，该结构是通过 USB 驱动程序堆栈分配并格式化的（对于选择接口请求）。 根据基础 USB 驱动程序堆栈的 USBD 接口版本，URB 可能与 URB 上下文相关联。</td>
</tr>
<tr class="odd">
<td>若要将 URB 与 IRP 关联 。</td>
<td>客户端驱动程序通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation" data-raw-source="[&lt;strong&gt;IoGetNextIrpStackLocation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)"><strong>IoGetNextIrpStackLocation</strong></a>获取指向下一个 IRP 堆栈位置的指针。 然后，客户端驱动程序将<strong>参数.</strong>堆栈位置的 Argument1 成员手动设置为<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)"><strong>URB</strong></a>结构的地址。</td>
<td>客户端驱动程序通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation" data-raw-source="[&lt;strong&gt;IoGetNextIrpStackLocation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)"><strong>IoGetNextIrpStackLocation</strong></a>获取指向下一个 IRP 堆栈位置的指针。 然后，客户端驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_assignurbtoiostacklocation" data-raw-source="[&lt;strong&gt;USBD_AssignUrbToIoStackLocation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_assignurbtoiostacklocation)"><strong>USBD_AssignUrbToIoStackLocation</strong></a> ，将 URB 与堆栈位置相关联。</td>
</tr>
<tr class="even">
<td>若要释放 URB 。</td>
<td>如果客户端驱动程序在堆栈上分配了 URB，则在请求完成后，该变量将超出范围。
<p>若要释放客户端驱动程序或在非分页池中分配的 USB 驱动程序堆栈的 URB 结构，客户端驱动程序将调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool" data-raw-source="[&lt;strong&gt;ExFreePool&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)"><strong>ExFreePool</strong></a>。</p></td>
<td>客户端驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urbfree" data-raw-source="[&lt;strong&gt;USBD_UrbFree&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urbfree)"><strong>USBD_UrbFree</strong></a>。</td>
</tr>
</tbody>
</table>

## <a name="related-topics"></a>相关主题

[向 USB 设备发送请求](communicating-with-a-usb-device.md)  
