---
title: 受保护打印的驱动程序支持
description: Windows 8.1 包括对受保护打印的支持，它允许用户指定在打印作业之前在打印机上使用的个人标识号（PIN）。
ms.assetid: 43569030-224F-46C6-963F-FC3BE24A0FB3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e9e154311553c3f4fd7f8e545b8203a66247d38
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652805"
---
# <a name="driver-support-for-protected-printing"></a>受保护打印的驱动程序支持

Windows 8.1 包括对受保护打印的支持，它允许用户指定在打印作业之前在打印机上使用的个人标识号（PIN）。

Windows 8.1 还允许管理员指定默认 PIN，以减少与打印出来但用户从不检索的内容相关的浪费的纸张消耗。 本主题介绍了对受保护打印提供支持的更改，还概述了将此支持添加到 v4 打印驱动程序所需的步骤。

## <a name="print-schema-changes"></a>打印架构更改

Windows 8.1 引入了新的打印架构关键字，你可以在 PrintTicket 和 PrintCapabilities 文档中使用这些关键字来指定受保护的打印。 这些关键字是在新的*printschemakeywordsv11*命名空间中定义的。 下面是此命名空间的 URI： [https://schemas.microsoft.com/windows/2013/05/printing/printschemakeywordsv11](https://schemas.microsoft.com/windows/2013/05/printing/printschemakeywordsv11)。

若要查看如何在 PrintTicket 文件中指定受保护的打印，请参阅[用于固定打印的示例 PrintTicket 文件](sample-printticket-file-for-pin-printing.md)。 若要了解如何在 PrintCapabilities 文件中指定受保护的打印，请参阅[用于 PIN 打印的示例 PrintCapabilities 文件](sample-printcapabilities-file-for-pin-printing.md)。

可在此处下载规范：

[打印架构规范1。1](https://download.microsoft.com/download/1/6/a/16acc601-1b7a-42ad-8d4e-4f0aa156ec3e/print-schema-spec-1-1.zip)

[打印架构规范2。0](https://download.microsoft.com/download/d/e/c/deca6e6b-3e81-48e7-b7ef-6d92a547d03c/print-schema-spec-2-0.zip)

## <a name="driver-changes"></a>驱动程序更改

如果使用的是 v4 驱动程序，则必须对一般打印机说明（GPD）或 PostScript 打印机说明（PPD）文件以及其他与驱动程序相关的代码文件进行更改。 受更改影响的与驱动程序相关的代码文件可按如下方式分类：

- 驱动程序配置文件（GPD 或 PPD）
- XPS 呈现筛选器
- 打印机扩展
- UWP 设备应用

> [!NOTE]
> 只要你在 PTProvider 代码中进行了所需的更改，就可以将 v3 驱动程序与打印架构关键字结合使用来进行保护打印。 但是，进行这些更改的步骤不在本主题的讨论范围内。

以下各节提供了有关如何实现更改的详细信息，这些更改将允许 v4 驱动程序支持受保护的打印。

### <a name="driver-configuration-file"></a>驱动程序配置文件

在 v4 打印驱动程序的数据文件中指示支持打印。 数据文件是 GPD 或 PPD 文件，无论驱动程序使用哪一个。 必须同时指定 MinLength 和 MaxLength 指令，才能启用受保护的打印。 下表描述了必须添加到驱动程序的 GPD 或 PPD 文件的相关关键字。

### <a name="what-to-add-to-a-gpd-file"></a>要添加到 GPD 文件的内容

如果驱动程序使用 GPD 文件，请使用以下语法添加以下新关键字：

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
<th>层次</th>
<th>允许的值</th>
<th>示例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong><em>JobPasscodeMinLength</strong></td>
<td><p>支持的 PIN 数值字符串的最小长度。</p>
<p>此值必须至少为4且不超过15。</p></td>
<td>根</td>
<td>任何<a href="numeric-values.md" data-raw-source="[GPD numeric value](numeric-values.md)">GPD 数值</a></td>
<td></em>JobPasscodeMinLength：4</td>
</tr>
<tr class="even">
<td><strong><em>JobPasscodeMaxLength</strong></td>
<td><p>支持的 PIN 数值字符串的最大长度。</p>
<p>此值必须至少为4且不超过15。 它必须大于或等于<strong></em>JobPasscodeMinLength</strong>值。</p></td>
<td>根</td>
<td>任何<a href="numeric-values.md" data-raw-source="[GPD numeric value](numeric-values.md)">GPD 数值</a></td>
<td>\* JobPasscodeMaxLength：9</td>
</tr>
</tbody>
</table>

## <a name="what-to-add-to-a-ppd-file"></a>要添加到 PPD 文件的内容

如果驱动程序使用 PPD 文件，请使用以下语法添加以下新关键字：

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
<th>层次</th>
<th>允许的值</th>
<th>示例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong><em>MSJobPasscodeMinLength</strong></td>
<td><p>支持的 PIN 数值字符串的最小长度。</p>
<p>此值必须至少为4且不超过15。</p></td>
<td>根</td>
<td><p>"int" （QuotedValue）</p>
<p>换言之，必须用引号表示整数值。</p></td>
<td></em>MSJobPasscodeMinLength： "4"</td>
</tr>
<tr class="even">
<td><strong><em>MSJobPasscodeMaxLength</strong></td>
<td><p>支持的 PIN 数值字符串的最大长度。</p>
<p>此值必须至少为4且不超过15。 它必须大于或等于<b>MSJobPasscodeMinLength</b>值。</p></td>
<td>根</td>
<td><p>"int" （QuotedValue）</p>
<p>换言之，必须用引号表示整数值。</p></td>
<td>\* MSJobPasscodeMaxLength： "9"</td>
</tr>
</tbody>
</table>

### <a name="specifying-hardware-constraints"></a>指定硬件约束

如果设备不支持不带可安装硬件（例如硬盘驱动器）的 PIN 打印，请使用 GPD 或 PPD 文件指定这些约束。 为此，必须编辑 GPD 或 PPD 文件，以显示 JobPasscode 功能和两个 JobPasscode 选项（打开和关闭）。 开启/关闭选项必须将 PrintSchemaKeywordMap 或 MSPrintSchemaKeywordMap 设置为合适的值。

### <a name="software-constraints"></a>软件约束

这些 API 不受支持。

### <a name="hardware-constraints"></a>硬件约束

下表显示了在需要为受保护的打印和硬件约束指定支持时必须使用的关键字的有效值。

File type 关键字有效值 GPD \*Feature JobPasscode \*选项
- OFF
- ON

\*PrintSchemaKeywordMap
- 非
- "On"
- "JobPasscode"

PPD \*功能 JobPasscode \*选项
- OFF
- ON

\*MSPrintSchemaKeywordMap
- 非
- "On"
- "JobPasscode"

### <a name="gpd-and-ppd-file-examples"></a>GPD 和 PPD 文件示例

下面是 GPD 文件的一个示例，它使用可安装的硬件约束指定 JobPasscode。

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

> [!NOTE]
> 必须使用 \*ConcealFromUI 关键字并将其设置为 TRUE，以防止无意中显示受保护的打印选项。 请参阅前面的 GPD 文件示例。

下面是使用可安装硬件约束指定 JobPasscode 的 PPD 文件的示例。

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

如前面的 PPD 文件示例中所示，\*UIConstraints 关键字表示硬件约束。

> [!NOTE]
> Windows 操作系统会自动为受保护的打印功能及其关联选项显示特定于区域设置的字符串。 不能为此功能或其选项指定新的本地化名称。

### <a name="xps-rendering-filters"></a>XPS 呈现筛选器

现有设备的驱动程序将需要更改其呈现代码，以便这些驱动程序可以将 PIN 值的 PrintTicket 表示形式转换为设备理解的值。 通常，这需要将代码添加到现有的 XPS 呈现筛选器，或添加新的 XPS 呈现筛选器以支持受保护的打印。 使用适用于 PCL6 和 PostScript 的标准 XPS 呈现筛选器的驱动程序应为其筛选器管道开发新的流筛选器。 当流通过标准筛选器后，此新流筛选器会将相应的命令注入到其筛选器管道中的预呈现 PDL 流中。

Microsoft 建议在客户端或服务器 PC 上最大程度地减少呈现要求，任何支持 XPS 或 OpenXPS 的新设备都应支持新的关键字，而不需要使用其他转换。

### <a name="printer-extensions"></a>打印机扩展

打印机扩展应能够在其打印首选项 UI 中显示受保护打印的控件。 这可确保桌面应用的用户可以在使用打印机扩展时配置受保护的打印功能。 Microsoft 正在进行一些更改，使[**IPrintSchemaTicket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschematicket)系列的 api 能够支持从打印机扩展进行保护的打印。

### <a name="uwp-device-apps"></a>UWP 设备应用

Microsoft 还进行了更改，使[**IPrintSchemaTicket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschematicket)系列的 api 能够与 UWP 设备应用一起使用，以在其打印首选项 UI 中显示用于受保护打印的控件。
