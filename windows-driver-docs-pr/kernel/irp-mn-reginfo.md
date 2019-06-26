---
title: IRP_MN_REGINFO
description: 支持 Microsoft Windows 98 和 Microsoft Windows 2000 的 WMI 的驱动程序必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: db93b64b-a2e4-429d-850e-921fb438467c
keywords:
- IRP_MN_REGINFO 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: d8a50e6b4bb3555aa71ea2efd2476a93112cf28d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370821"
---
# <a name="irpmnreginfo"></a>IRP\_MN\_REGINFO


支持 Microsoft Windows 98 和 Microsoft Windows 2000 的 WMI 的驱动程序必须处理此 IRP。 (也支持 Windows XP 的驱动程序还必须处理[ **IRP\_MN\_REGINFO\_EX** ](irp-mn-reginfo-ex.md) IRP。)驱动程序可以处理 WMI Irp 通过调用[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)或通过处理 IRP 本身，如中所述[处理 WMI 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_系统\_控件**](irp-mj-system-control.md)时发送
---------

在 Windows 98 和 Windows 2000 中，WMI 将发送查询或更新驱动程序的注册信息后，驱动程序已调用此 IRP [ **IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)。 Windows XP 及更高版本，WMI 将发送**IRP\_MN\_REGINFO\_EX**改为请求。

WMI 将此 IRP 发送在 IRQL = 被动\_级别在系统线程的上下文中。

## <a name="input-parameters"></a>输入参数


**Parameters.WMI.ProviderId**指向应该对请求进行响应的驱动程序的设备对象。 此指针位于 IRP 中的驱动程序的 I/O 堆栈位置。

**Parameters.WMI.DataPath**设置为**WMIREGISTER**查询注册信息或**WMIUPDATE**进行更新。

**Parameters.WMI.BufferSize**指示在非分页缓冲区的最大大小**Parameters.WMI.Buffer**。 大小必须大于或等于的总和 (**sizeof**(**WMIREGINFO**) + (*GuidCount* \* **sizeof**(**WMIREGGUID**))，其中*GuidCount*是数据块的数量和事件阻止注册的驱动程序，以及空间的静态实例名称，如果有的话。

## <a name="output-parameters"></a>输出参数


如果该驱动程序通过调用来处理 WMI Irp [ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)，WMI 获取驱动程序的数据块的注册信息通过调用其[ *DpWmiQueryReginfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_reginfo_callback)例程。

否则，该驱动程序会填写[ **WMIREGINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-wmireginfow)结构，在**Parameters.WMI.Buffer** ，如下所示：

-   集**BufferSize**以字节为单位的大小**WMIREGINFO**结构加上关联的注册数据。

-   如果该驱动程序处理 WMI 请求代表另一个驱动程序，设置**NextWmiRegInfo**以字节为单位的偏移量，从这开始**WMIREGINFO**到另一个开头**WMIREGINFO**结构，其中包含来自其他驱动程序的注册信息。

-   集**RegistryPath**到传递给驱动程序的注册表路径[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程。

-   如果**Parameters.WMI.Datapath**设置为**WMIREGISTER**，设置**MofResourceName**从开头的偏移量到**WMIREGINFO**为计数的 Unicode 字符串，包含其图像文件中的驱动程序的 MOF 资源的名称。

-   集**GuidCount**对数据块事件块以注册或更新的数目。

-   写入的数组[ **WMIREGGUID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-wmiregguidw)结构，一个用于每个数据块或驱动程序，在公开的事件块**WmiRegGuid**。

在每个驱动程序填充**WMIREGGUID**结构，如下所示：

-   集**Guid**到用于标识块的 GUID。

-   集**标志**提供实例名称和其他特性块的有关信息。 例如，如果正在使用静态实例名称注册一个块，该驱动程序设置**标志**与相应 WMIREG\_标志\_实例\_*XXX*标志.

如果正在使用静态实例名称，该驱动程序注册了块：

-   集**InstanceCount**为的实例数。

-   将以下成员之一设置为静态实例命名数据块的字节偏移量：
    -   如果驱动程序设置**标志**与 WMIREG\_标志\_实例\_列表中，设置**InstanceNameList**到一组静态实例名称字符串的偏移量。 WMI 实例在后续请求中通过指定索引到此列表中。
    -   如果驱动程序设置**标志**与 WMIREG\_标志\_实例\_基本名称，它会设置**BaseNameOffset**为偏移量为基名称字符串。 WMI 使用此字符串来生成块的静态实例名称。
    -   如果驱动程序设置**标志**与 WMIREG\_标志\_实例\_PDO，它会设置**Pdo**为指向 PDO 的偏移量传递给驱动程序的[*AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程。 WMI 使用 PDO 的设备实例路径来生成块的静态实例名称。
-   实例名称字符串、 基名称字符串或指针写入所指示的偏移量处的 PDO **InstanceNameList**， **BaseName**，或**Pdo**分别。

如果该驱动程序处理 WMI 注册代表另一个驱动程序 （如 miniclass 或微型端口驱动程序），它使用其他驱动程序的注册信息的另一个 WMIREGINFO 结构中填充，并将其在写入**NextWmiRegInfo**在以前的结构。

如果在缓冲区**Parameters.WMI.Buffer**太小，若要接收的所有数据，驱动程序所需的大小以字节为单位的形式写入到 ULONG **Parameters.WMI.Buffer**和 IRP 将失败并返回状态\_缓冲区\_过\_小。

## <a name="io-status-block"></a>I/O 状态块


如果该驱动程序通过调用来处理 IRP [ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)，WMI 集**Irp-&gt;IoStatus.Status**并**Irp-&gt;IoStatus.Information** I/O 状态块中。

否则，该驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功或相应的错误状态，如下所示：

状态\_缓冲区\_过\_小

如果成功，驱动程序设置**Irp-&gt;IoStatus.Information**写入的缓冲区的字节数**Parameters.WMI.Buffer**。

<a name="operation"></a>操作
---------

驱动程序可以处理 WMI Irp 通过调用[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)或通过处理 IRP 本身，如中所述[处理 WMI 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)。

如果驱动程序通过调用来处理 WMI Irp [ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)，例程调用的驱动程序[ *DpWmiQueryReginfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_reginfo_callback)例程。

如果驱动程序处理**IRP\_MN\_REGINFO**请求本身，才应该这样做**Parameters.WMI.ProviderId**指向同一个设备对象与指针，驱动程序传递给[ **IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)。 否则，该驱动程序必须将请求转发到下一步低驱动程序。

在处理请求之前, 驱动程序必须检查**Parameters.WMI.DataPath**以确定是否 WMI 查询注册信息 (**WMIREGISTER**) 或请求更新 (**WMIUPDATE**)。

WMI 驱动程序调用后，会发送与 WMIREGISTER 此 IRP **IoWMIRegistrationControl**与 WMIREG\_操作\_注册或 WMIREG\_操作\_重新注册。 在响应中，驱动程序应在缓冲区中填充**Parameters.WMI.Buffer**以下：

-   一个[ **WMIREGINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-wmireginfow)结构，指示驱动程序的注册表路径、 其 MOF 资源和块数，若要注册的名称。

-   一个[**WMIREGGUID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-wmiregguidw)注册每个块的结构。 如果块是要注册与静态实例名称，该驱动程序设置相应 WMIREG\_标志\_实例\_*XXX*标志中**WMIREGGUID**该块的结构。

-   任何字符串 WMI 需要生成静态实例名称。

WMI 将发送具有此 IRP **WMIUPDATE**驱动程序调用后**IoWmiRegistrationControl**与 WMIREG\_操作\_更新\_GUID。 在响应中，驱动程序应在缓冲区中填充**Parameters.WMI.Buffer**与 WMIREGINFO 结构，如下所示：

-   若要删除一个块，驱动程序设置 WMIREG\_标志\_删除\_中的 GUID 其**WMIREGGUID**结构。

-   若要添加或更新 （例如，若要更改其静态实例名称） 的块，驱动程序将清除 WMIREG\_标志\_删除\_GUID，并为块提供新的或更新的注册值。

-   若要注册新的或现有块与静态实例名称，该驱动程序设置相应 WMIREG\_标志\_实例\_*XXX*并提供 WMI 生成静态实例所需的任何字符串名称。

驱动程序可以使用相同**WMIREGINFO**结构以删除，请添加或更新为其最初用于注册的所有更改的标志和数据块来更新其块的块。 如果**WMIREGGUID**在此类**WMIREGINFO**结构完全匹配**WMIREGGUID**时它首次注册该块，则传递由驱动程序，WMI 将跳过处理参与更新块。

WMI 不会发送**IRP\_MN\_REGINFO**请求后一个驱动程序调用[ **IoWMIRegistrationControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)与 WMIREG\_操作\_取消注册，因为 WMI 不要求驱动程序从任何进一步的信息。 驱动程序通常注销响应其块[ **IRP\_MN\_删除\_设备**](irp-mn-remove-device.md)请求。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h 中 （包括 wdm.h 中、 Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[*DpWmiQueryReginfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_reginfo_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)

[**WMILIB\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/ns-wmilib-_wmilib_context)

[**WMIREGGUID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-wmiregguidw)

[**WMIREGINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-wmireginfow)

[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)

[**IRP\_MN\_REGINFO\_EX**](irp-mn-reginfo-ex.md)

 

 




