---
title: 受保护打印的驱动程序支持
description: Windows 8.1 包括用于受保护的打印，允许用户指定的个人标识号 (PIN)，然后使用在打印机正在打印的作业之前的支持。
ms.assetid: 43569030-224F-46C6-963F-FC3BE24A0FB3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 020d4c1c358dd11d929f85390d18f2d5e2a556c4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356064"
---
# <a name="driver-support-for-protected-printing"></a>受保护打印的驱动程序支持


Windows 8.1 包括用于受保护的打印，允许用户指定的个人标识号 (PIN)，然后使用在打印机正在打印的作业之前的支持。

Windows 8.1 还允许管理员指定默认 PIN 以减少浪费纸张消耗相关的打印输出但永远不会由用户检索内容。 本主题介绍了更改，可以为受保护的打印提供支持，还概述了将此支持添加到 v4 打印驱动程序所需的步骤。

## <a name="print-schema-changes"></a>打印架构更改

Windows 8.1 引入了可用于在 PrintTicket 和 PrintCapabilities 文档指定受保护的打印的新打印架构关键字。 在新定义这些关键字*printschemakeywordsv11*命名空间。 下面是此命名空间的 URI:

*http://schemas.microsoft.com/windows/2013/05/printing/printschemakeywordsv11*

若要查看如何在 PrintTicket 文件中指定受保护的打印，请参阅[的 PIN 打印示例 PrintTicket 文件](sample-printticket-file-for-pin-printing.md)。 若要了解如何在 PrintCapabilities 文件中指定受保护的打印，请参阅[的 PIN 打印示例 PrintCapabilities 文件](sample-printcapabilities-file-for-pin-printing.md)。

可以在此处下载规范：

[打印架构规范 1.1](http://download.microsoft.com/download/1/6/a/16acc601-1b7a-42ad-8d4e-4f0aa156ec3e/print-schema-spec-1-1.zip)

[打印架构规范 2.0](http://download.microsoft.com/download/d/e/c/deca6e6b-3e81-48e7-b7ef-6d92a547d03c/print-schema-spec-2-0.zip)


## <a name="driver-changes"></a>驱动程序更改


如果正在使用 v4 驱动程序，您必须对通用打印机说明 (GPD) 或 PostScript 打印机说明 (PPD) 文件和其他驱动程序相关的代码文件进行更改。 受更改影响的驱动程序相关的代码文件可以进行分类，如下所示：

-   驱动程序配置文件 （GPD 或 PPD）
-   XPS 呈现筛选器
-   打印机扩展
-   UWP 设备应用

**请注意**  可用于的 v3 驱动程序的打印架构关键字用于受保护的打印，只要在 PTProvider 代码中进行必要的更改。 但超出了本主题的范围是进行这些更改的步骤。

 

以下部分提供有关如何实现将允许您 v4 驱动程序以支持受保护的打印的更改的详细信息。

**驱动程序配置文件**

V4 打印驱动程序指示对在数据文件中的受保护打印支持。 数据文件是 GPD 或 PPD 文件-您的驱动程序使用任何一个。 必须指定 MinLength 和 MaxLength 指令来启用受保护的打印。 下表描述了你必须将它们添加到您的驱动程序 GPD 或 PPD 文件的相关关键字。

**要添加到 GPD 文件的内容**。 如果您的驱动程序使用 GPD 文件，添加以下新关键字使用以下语法：

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>关键字</th>
<th>描述</th>
<th>级别</th>
<th>允许的值</th>
<th>示例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong><em>JobPasscodeMinLength</strong></td>
<td><p>受支持的 PIN 数字字符串的最小长度。</p>
<p>此值必须至少为 4 且不大于 15。</p></td>
<td>根</td>
<td>任何<a href="numeric-values.md" data-raw-source="[GPD numeric value](numeric-values.md)">GPD 数字值</a></td>
<td></em>JobPasscodeMinLength:4</td>
</tr>
<tr class="even">
<td><strong><em>JobPasscodeMaxLength</strong></td>
<td><p>受支持的 PIN 数字字符串的最大长度。</p>
<p>此值必须至少为 4 且不大于 15。 它必须是大于或等于 <strong></em>JobPasscodeMinLength</strong>值。</p></td>
<td>根</td>
<td>任何<a href="numeric-values.md" data-raw-source="[GPD numeric value](numeric-values.md)">GPD 数字值</a></td>
<td>*JobPasscodeMaxLength:9</td>
</tr>
</tbody>
</table>

 

**要添加到 PPD 文件的内容**。 如果您的驱动程序使用 PPD 文件，添加以下新关键字使用以下语法：

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>关键字</th>
<th>描述</th>
<th>级别</th>
<th>允许的值</th>
<th>示例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong><em>MSJobPasscodeMinLength</strong></td>
<td><p>受支持的 PIN 数字字符串的最小长度。</p>
<p>此值必须至少为 4 且不大于 15。</p></td>
<td>根</td>
<td><p>"int"(QuotedValue)</p>
<p>换而言之，必须用引号表示的整数值。</p></td>
<td></em>MSJobPasscodeMinLength: ”4”</td>
</tr>
<tr class="even">
<td><strong><em>MSJobPasscodeMaxLength</strong></td>
<td><p>受支持的 PIN 数字字符串的最大长度。</p>
<p>此值必须至少为 4 且不大于 15。 它必须是大于或等于 <strong></em>MSJobPasscodeMinLength</strong>值。</p></td>
<td>根</td>
<td><p>"int"(QuotedValue)</p>
<p>换而言之，必须用引号表示的整数值。</p></td>
<td>*MSJobPasscodeMaxLength: ”9”</td>
</tr>
</tbody>
</table>

 

**指定硬件约束**。 如果你有不支持无需任何可安装的硬件 （例如硬盘驱动器） 的 PIN 打印设备，指定使用 GPD 或 PPD 文件这些约束。 若要执行此操作，必须编辑你的 GPD 或 PPD 文件以显示 JobPasscode 功能和这两个 JobPasscode 选项 （打开或关闭）。 ON/OFF 选项必须设置 PrintSchemaKeywordMap 或 MSPrintSchemaKeywordMap 为适当的值。

**软件约束**。 这些 API 不受支持。

下表显示了是否想要指定对受保护的打印和硬件约束支持的关键字，则必须使用有效的值。

文件类型有效关键字值 GPD\*功能 JobPasscode\*选项
-   OFF
-   ON

\*PrintSchemaKeywordMap
-   "关闭"状态
-   "On"
-   "JobPasscode"

PPD\*功能 JobPasscode\*选项
-   OFF
-   ON

\*MSPrintSchemaKeywordMap
-   "关闭"状态
-   "On"
-   "JobPasscode"

 

**GPD 和 PPD 文件示例**

下面是与可安装的硬件约束指定 JobPasscode GPD 文件的示例。

```GDP
*%
*GPDSpecVersion: "1.0"
*GPDFileVersion: "1.0"

*Include:        "StdNames.gpd"
*Include:        "MSxpsinc.gpd"
*ResourceDLL:    "unires.dll"

*GPDFileName:    "FAsmpl.gpd"
*ModelName:      "Fabrikam JobPasscode Sample"
*MasterUnits:    PAIR(1200, 1200)
*PrinterType:    PAGE
*MaxCopies:      999

*JobPasscodeMinLength: 4
*JobPasscodeMaxLength: 15

*%******************************************************************************
*%                             JobPasscode
*%******************************************************************************
*Feature: JobPasscode
{
    *Name: ”Job Passcode”
    *DefaultOption: OFF
    *ConcealFromUI: TRUE
    *PrintSchemaKeywordMap: “JobPasscode”

    *Option: OFF
    {
     *PrintSchemaKeywordMap: “Off”
        *Name: ”Off”
    }

    *Option: ON
    {
     *PrintSchemaKeywordMap: “On”
        *Name: ”On”
    }
}

*Feature:PrinterHardDisk
{
    *rcNameID: RESDLL.PCL5ERES.430
    *FeatureType: PRINTER_PROPERTY
    *DefaultOption: FALSE
    *Option: FALSE
    {
     *DisabledFeatures: LIST(JobPasscode)
        *rcNameID: RESDLL.PCL5ERES.444
    }
    *Option: TRUE
    {
        *rcNameID: RESDLL.PCL5ERES.443
    }
}
```

**请注意**  必须使用\*ConcealFromUI 关键字并设置它为 TRUE，以防止受保护的打印选项从被无意中所示。 请参阅前面的 GPD 文件示例。

 

下面是与可安装的硬件约束指定 JobPasscode PPD 文件的示例。

```PPD
*MSJobPasscodeMinLength: "4"
*MSJobPasscodeMaxLength: "15"

*OpenGroup: InstallableOptions/Installable Options

*% ===== Optional Hard Disk =====
*OpenUI *HardDisk/Printer Hard Disk: Boolean
*DefaultHardDisk:  False
*HardDisk False/Not Installed: ""
*HardDisk True/Installed: ""
*CloseUI: *HardDisk

*CloseGroup: InstallableOptions

*% ===== JobPasscode Feature =====
*OpenUI *JobPasscode: PickOne
*DefaultJobPasscode: On
*JobPasscode On: ""
*CloseUI: *JobPasscode

*MSPrintSchemaKeywordMap: JobPasscode  *JobPasscode
*MSPrintSchemaKeywordMap: JobPasscode  On *JobPasscode On

*UIConstraints: *HardDisk False *JobPasscode
```

正如您在前面的 PPD 文件示例，可以看到\*UIConstraints 关键字表示硬件约束。

**请注意**  Windows 操作系统会自动显示受保护的打印功能和其关联的选项的特定于区域设置的字符串。 不能指定此功能或其选项的新本地化的名称。

 

**XPS 呈现筛选器**

现有设备的驱动程序将需要对其呈现代码的更改，以便这些驱动程序可以转换为 PrintTicket 值的表示形式的 PIN 值设备能够理解。 一般情况下，这将要求添加到现有的 XPS 呈现筛选器，代码或添加新的 XPS 呈现筛选器以支持受保护的打印。 使用标准的 XPS 呈现筛选器来 PCL6 和 PostScript 驱动程序应开发其筛选器管道的新流筛选器。 此新流筛选器将把相应命令插入其筛选器管道，在预呈现的 PDL 流之后流通过标准筛选器。

Microsoft 建议是，为了尽量减少在客户端或服务器 PC 上的呈现要求，支持 XPS 或 OpenXPS 任何新设备应支持新关键字而无需使用其他转换。

**打印机扩展**

打印机扩展应该能够在其打印首选项用户界面中显示为受保护的打印控件。 这可确保使用打印机扩展时，桌面应用程序的用户可以配置受保护的打印功能。 Microsoft 正在进行更改，这样[ **IPrintSchemaTicket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprintschematicket)系列的 Api 以支持受保护的打印从打印机扩展。

**UWP 的设备应用程序**

Microsoft 还将更改，以允许[ **IPrintSchemaTicket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprintschematicket)受保护的系列的 Api 来使用 UWP 设备应用，显示的控件在其打印首选项用户界面中的进行打印。

 

 




