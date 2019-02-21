---
title: 确定是否 Static Driver Verifier 支持驱动程序或库
description: Static Driver Verifier (SDV) 可以支持 WDM、 KMDF、 NDIS 和 Storport 驱动程序和库。 若要确定驱动程序或库是否受支持，并正确配置，阅读通过在本部分中所述的要求。
ms.assetid: 29E93E9E-7F87-4706-97AD-DB9A32EDD388
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fe67c93afa12172b53cca50763f77eb2f3d6f87
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542413"
---
# <a name="determining-if-static-driver-verifier-supports-your-driver-or-library"></a>确定是否 Static Driver Verifier 支持驱动程序或库


Static Driver Verifier (SDV) 完全支持 WDM、 KMDF、 NDIS 和 Storport 驱动程序和库，并为其他驱动程序提供有限支持。 若要确定驱动程序或库是否受支持，并正确配置，阅读通过在本部分中所述的要求。

## <a name="driver-or-library-requirements"></a>驱动程序或库要求


如果驱动程序或库满足以下条件之一，则您可运行 SDV 分析工具规则的完整集：

-   必须 WDM 驱动程序或库，并且在驱动程序或库未链接到一个类的框架 （即，由 Microsoft 提供库）。 有关详细信息，请参阅[framework 类库](#class-framework-libraries)。
-   你具有的驱动程序或库链接到 WdfLdr.lib 或 WdfDriverEntry.lib。
-   你具有的驱动程序或库链接到 NDIS.lib。
-   你具有的驱动程序或库链接到 Storport.lib。

Static Driver Verifier 支持驱动程序或库，通过这些条件，即使驱动程序或库链接到多个[实用工具库](#utility-libraries)。

此外，若要执行分析，SDV 要求：

-   该驱动程序已声明至少一个入口点[使用函数角色类型声明](using-function-role-type-declarations.md)。
-   该驱动程序生成并链接正确 （在 Visual Studio 中使用 MSBuild)。
-   如果驱动程序或库使用 KMDF，驱动程序或库使用 KDMF 1.7 或更高版本。
-   如果所使用 NDIS 驱动程序或库，它使用 NDIS 版本 6.0、 6.1、 6.20、 6.30 或 6.40。 请注意，此列表可能会发生更改。
-   该驱动程序不能合并 （例如，使用 WDM、 KMDF 或 KMDF 和 NDIS） 驱动程序模型。

还有其他一些因素的影响的质量和静态分析结果的准确性。 这些因素包括：

-   尚未处理的 SDV 的实用程序库的使用。
-   该驱动程序，尤其当它有超过 100 万行的代码的大小。
-   使用特定于语言的功能，如虚拟函数和指针算法。

## <a name="visual-studio-project-requirements"></a>Visual Studio 项目要求


若要使用 Static Driver Verifier，Visual Studio 项目必须具有以下设置：

-   UseDebugLibraries = false
-   平台 = Win32 (x86) 或 x64

## <a name="class-framework-libraries"></a>Framework 类库


如果你具有 WDM 驱动程序或库，并想要再次运行 SDV，驱动程序或库不将必须链接到一个以下 framework 类库中。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">1394bus.lib</td>
<td align="left">fltMgr.lib</td>
<td align="left">rdbss.lib</td>
<td align="left">usbrpm.lib</td>
</tr>
<tr class="even">
<td align="left">acpi.lib</td>
<td align="left">FsDepends.lib</td>
<td align="left">RNDISMP.lib</td>
<td align="left">videoprt.lib</td>
</tr>
<tr class="odd">
<td align="left">armppm.lib</td>
<td align="left">fwpkclnt.lib</td>
<td align="left">RNDISMP6.lib</td>
<td align="left">vwififlt.lib</td>
</tr>
<tr class="even">
<td align="left">ataport.lib</td>
<td align="left">hidclass.lib</td>
<td align="left">RNDISMPX.lib</td>
<td align="left">watchdog.lib</td>
</tr>
<tr class="odd">
<td align="left">ath_hwpci.lib</td>
<td align="left">hidparse.lib</td>
<td align="left">rpcxdr.lib</td>
<td align="left">win32k.lib</td>
</tr>
<tr class="even">
<td align="left">athhal.lib</td>
<td align="left">hwpolicy.lib</td>
<td align="left">Saha.lib</td>
<td align="left">winhv.lib</td>
</tr>
<tr class="odd">
<td align="left">battc.lib</td>
<td align="left">ipmidrv_hrmcust.lib</td>
<td align="left">scsiport.lib</td>
<td align="left">WMBBCLASS.lib</td>
</tr>
<tr class="even">
<td align="left">BdaSup.lib</td>
<td align="left">irt30.lib</td>
<td align="left">smclib.lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">bdl.lib</td>
<td align="left">irt30.lib</td>
<td align="left">Soft1667FaultInjectionLimpetPool.lib</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">btampm.lib</td>
<td align="left">ks.lib</td>
<td align="left">SoftFCKernel.lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">bthport.lib</td>
<td align="left">ksecdd.lib</td>
<td align="left">SoftFCLimpetPool.lib</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">BTHPRINT.lib</td>
<td align="left">ksmartcpu.lib</td>
<td align="left">SoftSATAKernel.lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">classpnp.lib</td>
<td align="left">mcd.lib</td>
<td align="left">SoftStorageLimpetPool.lib</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">clfs.lib</td>
<td align="left">mpio.lib</td>
<td align="left">srvnet.lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">cng.lib</td>
<td align="left">mrxsmb.lib</td>
<td align="left">storvsp.lib</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">crashdmp.lib</td>
<td align="left">msnfsflt.lib</td>
<td align="left">stream.lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">csr_vfp_avdtp.lib</td>
<td align="left">msrpc.lib</td>
<td align="left">tape.lib</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">diskdump.lib</td>
<td align="left">mup.lib</td>
<td align="left">tbs.lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">drmk.lib</td>
<td align="left">ndistapi.lib</td>
<td align="left">tcpip.lib</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">dumpata.lib</td>
<td align="left">netio.lib</td>
<td align="left">tdi.lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">dumpfve.lib</td>
<td align="left">ntasn1k.lib</td>
<td align="left">termdd.lib</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">dxapi.lib</td>
<td align="left">parallel.lib</td>
<td align="left">USBCAMD.lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">dxg.lib</td>
<td align="left">pciidex.lib</td>
<td align="left">USBCAMD2.lib</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">dxgkrnl.lib</td>
<td align="left">portcls.lib</td>
<td align="left">usbd.lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">dxgmms1.lib</td>
<td align="left">protogon.lib</td>
<td align="left">usbport.lib</td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

## <a name="utility-libraries"></a>实用程序库


Static Driver Verifier 支持的驱动程序或库，其中链接到多个实用程序库，如果驱动程序或库符合[驱动程序或库要求](#driver-or-library-requirements)。

|                     |
|---------------------|
| BufferOverflowK.lib |
| hal.lib             |
| ntoskrnl.lib        |
| ntstrsafe.lib       |
| rtlver.lib          |
| sehupd.lib          |
| wdm.lib             |
| wmilib.lib          |
| wdmsec.lib          |

 

 

 





