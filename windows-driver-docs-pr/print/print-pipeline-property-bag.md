---
title: 打印管道属性包
description: 打印管道属性包用于在筛选器管道中的筛选器之间传递信息。属性 nameSymbolic nameProperty typeDescriptionPrinterNameXPS\_FP\_PRINTER\_NAMEVT\_BSTRThe 打印机名称。ProgressReportXPS\_FP\_进度\_REPORTVT\_UNKNOWNA 指向 IUnknown 接口的指针。 调用 QueryInterface 以获取指向 IPrintPipelineProgressReport 接口的指针。PrinterHandleXPS\_FP\_打印机\_处理 VT\_BYREFThe 打印机句柄。 筛选器不应关闭此句柄。PerUserPrintTicketXPS\_FP\_用户\_打印\_TICKETVT\_UNKNOWNA 指向 IUnknown 接口的指针。 调用 QueryInterface 以获取指向 IPrintReadStreamFactory 接口的指针。UserSecurityTokenXPS\_FP\_用户\_TOKENVT\_BYREFA 句柄，筛选器可以使用该句柄模拟提交打印作业的用户帐户。PrintJobIdXPS\_FP\_JOB\_IDVT\_UI4The 打印作业标识号。PrintClassFactoryXPS\_FP\_打印\_类\_FACTORYVT\_UNKNOWNA 指向 IUnknown 接口的指针。 调用 QueryInterface 以获取指向 IPrintClassObjectFactory 接口的指针。IPrintCoreHelper （此属性名称没有符号名称。）VT\_UNKNOWNA 指向 IUnknown 接口的指针。 调用 QueryInterface 以获取指向 IPrintCoreHelper 接口的指针。请注意，此属性仅适用于使用 unidrvui 作为配置 UI DLL 的 XPSDrv 打印机驱动程序。PrintDeviceCapabilitiesXPS\_FP\_PRINTDEVICECAPABILITIES VT\_UNKNOWNA 指向 IUnknown 接口的指针。 调用 QueryInterface 以获取指向 IPrintReadStreamFactory 接口的指针。允许 XPS 呈现筛选器检索打印筛选器管道属性包中的 PrintDeviceCapabilities XML 文件。
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
ms.openlocfilehash: 594163978ec16ae2e95526e2647e2e4662848e7d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842345"
---
# <a name="print-pipeline-property-bag"></a>打印管道属性包

打印管道属性包用于在筛选器管道中的筛选器之间传递信息。

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
<td><p>指向<strong>IUnknown</strong>接口的指针。 调用<strong>QueryInterface</strong>以获取指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintpipelineprogressreport" data-raw-source="[IPrintPipelineProgressReport](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintpipelineprogressreport)">IPrintPipelineProgressReport</a>接口的指针。</p></td>
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
<td><p>指向<strong>IUnknown</strong>接口的指针。 调用<strong>QueryInterface</strong>以获取指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintreadstreamfactory" data-raw-source="[IPrintReadStreamFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintreadstreamfactory)">IPrintReadStreamFactory</a>接口的指针。</p></td>
</tr>
<tr class="odd">
<td><p>UserSecurityToken</p></td>
<td><p>XPS_FP_USER_TOKEN</p></td>
<td><p>VT_BYREF</p></td>
<td><p>一个句柄，筛选器可以使用该句柄模拟提交打印作业的用户帐户。</p></td>
</tr>
<tr class="even">
<td><p>PrintJobId</p></td>
<td><p>XPS_FP_JOB_ID</p></td>
<td><p>VT_UI4</p></td>
<td><p>打印作业标识号。</p></td>
</tr>
<tr class="odd">
<td><p>PrintClassFactory</p></td>
<td><p>XPS_FP_PRINT_CLASS_FACTORY</p></td>
<td><p>VT_UNKNOWN</p></td>
<td><p>指向<strong>IUnknown</strong>接口的指针。 调用<strong>QueryInterface</strong>以获取指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintclassobjectfactory" data-raw-source="[IPrintClassObjectFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintclassobjectfactory)">IPrintClassObjectFactory</a>接口的指针。</p></td>
</tr>
<tr class="even">
<td><p>IPrintCoreHelper</p></td>
<td><p>（此属性名称没有符号名称。）</p></td>
<td><p>VT_UNKNOWN</p></td>
<td><p>指向<strong>IUnknown</strong>接口的指针。 调用<strong>QueryInterface</strong>以获取指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelper" data-raw-source="[IPrintCoreHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelper)">IPrintCoreHelper</a>接口的指针。</p>
<p>请注意，此属性仅适用于使用 unidrvui 作为配置 UI DLL 的 XPSDrv 打印机驱动程序。</p></td>
</tr>
<tr class="odd">
<td><p>PrintDeviceCapabilities</p></td>
<td><p>XPS_FP_PRINTDEVICECAPABILITIES</p></td>
<td><p>VT_UNKNOWN</p></td>
<td><p>指向<strong>IUnknown</strong>接口的指针。 调用<strong>QueryInterface</strong>以获取指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintreadstreamfactory" data-raw-source="[IPrintReadStreamFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintreadstreamfactory)">IPrintReadStreamFactory</a>接口的指针。</p>
<p>允许 XPS 呈现筛选器检索打印筛选器管道属性包中的 PrintDeviceCapabilities XML 文件。</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[V4 打印机驱动程序属性包](https://docs.microsoft.com/windows-hardware/drivers/print/v4-driver-property-bags)
