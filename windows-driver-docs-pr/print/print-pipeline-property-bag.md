---
title: 打印管道属性包
description: 打印管道属性包用于在筛选器管道中的筛选器之间传递信息。属性 nameSymbolic nameProperty typeDescriptionPrinterNameXPS \_ FP \_ printer \_ NAMEVT \_ BSTRThe printer name。ProgressReportXPS \_ FP \_ 进度 \_ REPORTVT \_ UNKNOWNA 指向 IUnknown 接口的指针。 调用 QueryInterface 以获取指向 IPrintPipelineProgressReport 接口的指针。PrinterHandleXPS \_ FP \_ PRINTER \_ 处理 VT \_ BYREFThe printer 控点。 筛选器不应关闭此句柄。PerUserPrintTicketXPS \_ FP \_ USER \_ PRINT \_ TICKETVT \_ UNKNOWNA 指向 IUnknown 接口的指针。 调用 QueryInterface 以获取指向 IPrintReadStreamFactory 接口的指针。UserSecurityTokenXPS \_ FP \_ user \_ TOKENVT \_ BYREFA 句柄，筛选器可以使用该句柄模拟提交打印作业的用户帐户。PrintJobIdXPS \_ FP \_ job \_ IDVT \_ UI4The 打印作业标识号。PrintClassFactoryXPS \_ FP \_ PRINT \_ CLASS \_ FACTORYVT \_ UNKNOWNA 指向 IUnknown 接口的指针。 调用 QueryInterface 以获取指向 IPrintClassObjectFactory 接口的指针。IPrintCoreHelper (此属性名称没有符号名称。 ) VT \_ UNKNOWNA 指向 IUnknown 接口的指针。 调用 QueryInterface 以获取指向 IPrintCoreHelper 接口的指针。请注意，此属性仅在使用 unidrvui.dll 作为配置 UI DLL 的 XPSDrv 打印机驱动程序中可用。PrintDeviceCapabilitiesXPS \_ FP \_ PRINTDEVICECAPABILITIES VT \_ UNKNOWNA 指向 IUnknown 接口的指针。 调用 QueryInterface 以获取指向 IPrintReadStreamFactory 接口的指针。允许 XPS 呈现筛选器检索打印筛选器管道属性包中的 PrintDeviceCapabilities XML 文件。
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
ms.openlocfilehash: e4f33ee5f651856feb6b39eccfd6b31454e4f275
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214204"
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
<th>属性名称</th>
<th>符号名称</th>
<th>属性类型</th>
<th>说明</th>
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
<td><p>指向 <strong>IUnknown</strong> 接口的指针。 调用 <strong>QueryInterface</strong> 以获取指向 <a href="/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintpipelineprogressreport" data-raw-source="[IPrintPipelineProgressReport](/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintpipelineprogressreport)">IPrintPipelineProgressReport</a> 接口的指针。</p></td>
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
<td><p>指向 <strong>IUnknown</strong> 接口的指针。 调用 <strong>QueryInterface</strong> 以获取指向 <a href="/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintreadstreamfactory" data-raw-source="[IPrintReadStreamFactory](/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintreadstreamfactory)">IPrintReadStreamFactory</a> 接口的指针。</p></td>
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
<td><p>指向 <strong>IUnknown</strong> 接口的指针。 调用 <strong>QueryInterface</strong> 以获取指向 <a href="/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintclassobjectfactory" data-raw-source="[IPrintClassObjectFactory](/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintclassobjectfactory)">IPrintClassObjectFactory</a> 接口的指针。</p></td>
</tr>
<tr class="even">
<td><p>IPrintCoreHelper</p></td>
<td><p> (此属性名称没有符号名称。 ) </p></td>
<td><p>VT_UNKNOWN</p></td>
<td><p>指向 <strong>IUnknown</strong> 接口的指针。 调用 <strong>QueryInterface</strong> 以获取指向 <a href="/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelper" data-raw-source="[IPrintCoreHelper](/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelper)">IPrintCoreHelper</a> 接口的指针。</p>
<p>请注意，此属性仅在使用 unidrvui.dll 作为配置 UI DLL 的 XPSDrv 打印机驱动程序中可用。</p></td>
</tr>
<tr class="odd">
<td><p>PrintDeviceCapabilities</p></td>
<td><p>XPS_FP_PRINTDEVICECAPABILITIES</p></td>
<td><p>VT_UNKNOWN</p></td>
<td><p>指向 <strong>IUnknown</strong> 接口的指针。 调用 <strong>QueryInterface</strong> 以获取指向 <a href="/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintreadstreamfactory" data-raw-source="[IPrintReadStreamFactory](/windows-hardware/drivers/ddi/filterpipeline/nn-filterpipeline-iprintreadstreamfactory)">IPrintReadStreamFactory</a> 接口的指针。</p>
<p>允许 XPS 呈现筛选器检索打印筛选器管道属性包中的 PrintDeviceCapabilities XML 文件。</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[V4 打印机驱动程序属性包](./v4-driver-property-bags.md)