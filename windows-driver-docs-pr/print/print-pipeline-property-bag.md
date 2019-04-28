---
title: 打印管道属性包
description: 使用打印的管道属性包中的筛选器管道的筛选器之间传递信息。属性 nameSymbolic nameProperty typeDescriptionPrinterNameXPS\_FP\_打印机\_NAMEVT\_BSTRThe 打印机名称。ProgressReportXPS\_FP\_进度\_REPORTVT\_UNKNOWNA IUnknown 接口指针。 调用 QueryInterface 来获取 IPrintPipelineProgressReport 接口的指针。PrinterHandleXPS\_FP\_打印机\_句柄 VT\_BYREFThe 打印机句柄。 筛选器不应关闭此句柄。PerUserPrintTicketXPS\_FP\_用户\_打印\_TICKETVT\_UNKNOWNA IUnknown 接口指针。 调用 QueryInterface 来获取 IPrintReadStreamFactory 接口的指针。UserSecurityTokenXPS\_FP\_用户\_TOKENVT\_BYREFA 处理筛选器可用于模拟提交打印作业的用户帐户。PrintJobIdXPS\_FP\_作业\_IDVT\_UI4The 打印作业的标识号。PrintClassFactoryXPS\_FP\_打印\_类\_FACTORYVT\_UNKNOWNA IUnknown 接口指针。 调用 QueryInterface 来获取 IPrintClassObjectFactory 接口的指针。IPrintCoreHelper （没有任何符号名称，此属性名称。）VT\_UNKNOWNA IUnknown 接口指针。 调用 QueryInterface 来获取 IPrintCoreHelper 接口的指针。请注意，此属性仅用作配置 UI DLL unidrvui.dll 的 XPSDrv 打印机驱动程序中可用。PrintDeviceCapabilitiesXPS\_FP\_PRINTDEVICECAPABILITIES VT\_UNKNOWNA IUnknown 接口指针。 调用 QueryInterface 来获取 IPrintReadStreamFactory 接口的指针。允许 XPS 呈现筛选器，以从打印筛选器管道属性包检索 PrintDeviceCapabilities XML 文件。
MS-HAID:
- filterpipeline\_f3fbd165-3f72-41cc-91b8-aa8b36823da9.xml
- print.print\_pipeline\_property\_bag
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 5a0fb200-a2c2-41f0-8dcf-6eb3361c148e
keywords:
- 打印管道属性包打印设备
topic_type:
- apiref
api_name:
- Print Pipeline Property Bag
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23ae404f052d7ea69152dacfcf9203fde5c9679f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340887"
---
# <a name="print-pipeline-property-bag"></a>打印管道属性包

使用打印的管道属性包中的筛选器管道的筛选器之间传递信息。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性名</th>
<th>符号名称</th>
<th>属性类型</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PrinterName</p></td>
<td><p>XPS_FP_PRINTER_NAME</p></td>
<td><p>VT_BSTR</p></td>
<td><p>打印机名称。</p></td>
</tr>
<tr class="even">
<td><p>ProgressReport</p></td>
<td><p>XPS_FP_PROGRESS_REPORT</p></td>
<td><p>VT_UNKNOWN</p></td>
<td><p>一个指向<strong>IUnknown</strong>接口。 调用<strong>QueryInterface</strong>若要获取的指针<a href="https://msdn.microsoft.com/library/windows/hardware/ff554314" data-raw-source="[IPrintPipelineProgressReport](https://msdn.microsoft.com/library/windows/hardware/ff554314)">IPrintPipelineProgressReport</a>接口。</p></td>
</tr>
<tr class="odd">
<td><p>PrinterHandle</p></td>
<td><p>XPS_FP_PRINTER_HANDLE</p></td>
<td><p>VT_BYREF</p></td>
<td><p>打印机句柄。 筛选器不应关闭此句柄。</p></td>
</tr>
<tr class="even">
<td><p>PerUserPrintTicket</p></td>
<td><p>XPS_FP_USER_PRINT_TICKET</p></td>
<td><p>VT_UNKNOWN</p></td>
<td><p>一个指向<strong>IUnknown</strong>接口。 调用<strong>QueryInterface</strong>若要获取的指针<a href="https://msdn.microsoft.com/library/windows/hardware/ff554338" data-raw-source="[IPrintReadStreamFactory](https://msdn.microsoft.com/library/windows/hardware/ff554338)">IPrintReadStreamFactory</a>接口。</p></td>
</tr>
<tr class="odd">
<td><p>UserSecurityToken</p></td>
<td><p>XPS_FP_USER_TOKEN</p></td>
<td><p>VT_BYREF</p></td>
<td><p>筛选器可用于模拟的用户帐户提交打印作业的一个句柄。</p></td>
</tr>
<tr class="even">
<td><p>PrintJobId</p></td>
<td><p>XPS_FP_JOB_ID</p></td>
<td><p>VT_UI4</p></td>
<td><p>打印作业的标识号。</p></td>
</tr>
<tr class="odd">
<td><p>PrintClassFactory</p></td>
<td><p>XPS_FP_PRINT_CLASS_FACTORY</p></td>
<td><p>VT_UNKNOWN</p></td>
<td><p>一个指向<strong>IUnknown</strong>接口。 调用<strong>QueryInterface</strong>若要获取的指针<a href="https://msdn.microsoft.com/library/windows/hardware/ff551955" data-raw-source="[IPrintClassObjectFactory](https://msdn.microsoft.com/library/windows/hardware/ff551955)">IPrintClassObjectFactory</a>接口。</p></td>
</tr>
<tr class="even">
<td><p>IPrintCoreHelper</p></td>
<td><p>（没有任何符号名称，此属性名称。）</p></td>
<td><p>VT_UNKNOWN</p></td>
<td><p>一个指向<strong>IUnknown</strong>接口。 调用<strong>QueryInterface</strong>若要获取的指针<a href="https://msdn.microsoft.com/library/windows/hardware/ff552960" data-raw-source="[IPrintCoreHelper](https://msdn.microsoft.com/library/windows/hardware/ff552960)">IPrintCoreHelper</a>接口。</p>
<p>请注意，此属性仅用作配置 UI DLL unidrvui.dll 的 XPSDrv 打印机驱动程序中可用。</p></td>
</tr>
<tr class="odd">
<td><p>PrintDeviceCapabilities</p></td>
<td><p>XPS_FP_PRINTDEVICECAPABILITIES</p></td>
<td><p>VT_UNKNOWN</p></td>
<td><p>一个指向<strong>IUnknown</strong>接口。 调用<strong>QueryInterface</strong>若要获取的指针<a href="https://msdn.microsoft.com/library/windows/hardware/ff554338" data-raw-source="[IPrintReadStreamFactory](https://msdn.microsoft.com/library/windows/hardware/ff554338)">IPrintReadStreamFactory</a>接口。</p>
<p>允许 XPS 呈现筛选器，以从打印筛选器管道属性包检索 PrintDeviceCapabilities XML 文件。</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[V4 打印机驱动程序属性包](https://docs.microsoft.com/windows-hardware/drivers/print/v4-driver-property-bags)
