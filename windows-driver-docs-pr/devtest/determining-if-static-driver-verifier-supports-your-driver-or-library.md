---
title: 确定静态驱动程序验证程序是否支持你的驱动程序或库
description: 静态驱动程序验证器 (SDV) 可以支持 WDM、KMDF、NDIS 和 Storport 驱动程序和库。 若要确定是否支持并正确配置了驱动程序或库，请阅读本部分中所述的超出要求。
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 04bfc8f5c286d2ea80fb44e83e0539c26461d9f7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817821"
---
# <a name="determining-if-static-driver-verifier-supports-your-driver-or-library"></a>确定静态驱动程序验证程序是否支持你的驱动程序或库

静态驱动程序验证器 (SDV) 完全支持 WDM、KMDF、NDIS 和 Storport 驱动程序和库，并对其他驱动程序的支持有限。 若要确定是否支持并正确配置了驱动程序或库，请阅读本部分中所述的超出要求。

## <a name="driver-or-library-requirements"></a>驱动程序或库要求

如果驱动程序或库满足以下条件之一，则可以在 SDV 分析工具中运行完整的一组规则 **，而** 不会链接到 [下面列出的任何类框架库](#class-framework-libraries)。

- 有一个 WDM 驱动程序或库。
- 你有一个链接到 WdfLdr 或 WdfDriverEntry 的驱动程序或库。
- 你有一个链接到 NDIS .lib 的驱动程序或库。
- 你有一个链接到 Storport .lib 的驱动程序或库。

如果你的驱动程序在上述条件以外，则 SDV 会将驱动程序视为 "通用"，并运行有限的一组检查。

此外，请注意，由 SDV 验证的库必须是内核模式驱动程序库，而不是一般 C 或 c + + 库。  

静态驱动程序验证程序支持通过这些条件的驱动程序或库，即使驱动程序或库链接到多个 [实用程序库](#utility-libraries)。

此外，若要执行分析，SDV 要求：

- 驱动程序已 [使用函数角色类型声明](using-function-role-type-declarations.md)至少声明了一个入口点。
- 驱动程序在 Visual Studio 中使用 MSBuild) 正确生成和链接 (。
- 如果驱动程序或库使用 KMDF，则驱动程序或库使用 KDMF 版本1.7 或更高版本。
- 如果驱动程序或库使用 NDIS，则使用 NDIS 版本6.0、6.1、6.20、6.30 或6.40。 请注意，此列表可能会更改。
- 该驱动程序不会合并驱动程序模型 (例如，KMDF 与 WDM，或 KMDF 和 NDIS) 。

其他因素影响了静态分析结果的质量和准确性。 这些因素包括：

- SDV 未处理的实用工具库的使用。
- 驱动程序的大小，尤其是在超过100K 的代码行时。
- 使用特定于语言的功能，如虚函数和指针算法。

## <a name="visual-studio-project-requirements"></a>Visual Studio 项目要求

若要使用静态驱动程序验证程序，Visual Studio 项目必须具有以下设置：

- UseDebugLibraries = false
- 平台 = Win32 (x86) 或 x64

## <a name="class-framework-libraries"></a>类框架库

如果有 WDM 驱动程序或库，并且想要运行 SDV，则驱动程序或库不得链接到以下类框架库之一。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">1394bus</td>
<td align="left">fltMgr</td>
<td align="left">rdbss</td>
<td align="left">usbrpm</td>
</tr>
<tr class="even">
<td align="left">acpi .lib</td>
<td align="left">FsDepends</td>
<td align="left">RNDISMP</td>
<td align="left">videoprt</td>
</tr>
<tr class="odd">
<td align="left">armppm</td>
<td align="left">fwpkclnt</td>
<td align="left">RNDISMP6</td>
<td align="left">vwififlt</td>
</tr>
<tr class="even">
<td align="left">ataport</td>
<td align="left">hidclass</td>
<td align="left">RNDISMPX</td>
<td align="left">看门程序</td>
</tr>
<tr class="odd">
<td align="left">ath_hwpci .lib</td>
<td align="left">hidparse</td>
<td align="left">rpcxdr</td>
<td align="left">win32k.sys</td>
</tr>
<tr class="even">
<td align="left">athhal</td>
<td align="left">hwpolicy</td>
<td align="left">Saha</td>
<td align="left">winhv</td>
</tr>
<tr class="odd">
<td align="left">battc</td>
<td align="left">ipmidrv_hrmcust .lib</td>
<td align="left">scsiport</td>
<td align="left">WMBBCLASS</td>
</tr>
<tr class="even">
<td align="left">BdaSup</td>
<td align="left">irt30.sys</td>
<td align="left">smclib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">bdl</td>
<td align="left">irt30.sys</td>
<td align="left">Soft1667FaultInjectionLimpetPool</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">btampm</td>
<td align="left">ks</td>
<td align="left">SoftFCKernel</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">bthport</td>
<td align="left">ksecdd</td>
<td align="left">SoftFCLimpetPool</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">BTHPRINT</td>
<td align="left">ksmartcpu</td>
<td align="left">SoftSATAKernel</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">classpnp</td>
<td align="left">mcd</td>
<td align="left">SoftStorageLimpetPool</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">clfs</td>
<td align="left">mpio</td>
<td align="left">srvnet</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">cng .lib</td>
<td align="left">mrxsmb</td>
<td align="left">storvsp</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">crashdmp</td>
<td align="left">msnfsflt</td>
<td align="left">stream .lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">csr_vfp_avdtp .lib</td>
<td align="left">msrpc</td>
<td align="left">磁带 .lib</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">diskdump</td>
<td align="left">mup .lib</td>
<td align="left">tbs .lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">drmk</td>
<td align="left">ndistapi</td>
<td align="left">tcpip .lib</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">dumpata</td>
<td align="left">netio</td>
<td align="left">tdi .lib</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">dumpfve</td>
<td align="left">ntasn1k</td>
<td align="left">termdd.sys</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">dxapi</td>
<td align="left">并行 .lib</td>
<td align="left">USBCAMD</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">dxg</td>
<td align="left">pciidex</td>
<td align="left">USBCAMD2</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">dxgkrnl</td>
<td align="left">portcls</td>
<td align="left">usbd</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">dxgmms1</td>
<td align="left">protogon</td>
<td align="left">usbport</td>
<td align="left"></td>
</tr>
</tbody>
</table>

## <a name="utility-libraries"></a>实用工具库

如果驱动程序或库符合 [驱动程序或库要求](#driver-or-library-requirements)，则静态驱动程序验证程序支持具有指向多个实用工具库的链接的驱动程序或库。

| 文件名           |
|---------------------|
| BufferOverflowK |
| hal .lib             |
| ntoskrnl.exe        |
| ntstrsafe.h 而       |
| rtlver          |
| sehupd          |
| wdm .lib             |
| wmilib          |
| wdmsec          |

## <a name="static-driver-verifier-and-microsoft-class-framework-libraries"></a>静态驱动程序验证程序和 Microsoft 类框架库

如果使用的是必须链接到 [类框架](#class-framework-libraries) 库中的类框架库的 WDM 驱动程序，则驱动程序将无法通过静态驱动程序验证程序条件。 但是，还可以使用某些通用规则，例如 [NullCheck 规则](./nullcheck.md) 来执行某些级别的静态验证。
