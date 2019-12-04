---
title: SMBIOS
description: SMBIOS 规范定义将进入与系统相关的数据结构的数据结构和信息。
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 178f51631fc6bc95ef96fc98b98ce3fdebc6685f
ms.sourcegitcommit: 1585a52e762226b01c7369371727746487cc57bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2019
ms.locfileid: "74796663"
---
# <a name="smbios"></a>SMBIOS

SMBIOS 规范定义将进入与系统相关的数据结构的数据结构和信息。 使用最新的 SMBIOS 规范，我们跟上规范中定义的最新更改保持最新。 下表描述了建议的 SMBIOS 设置，以及这些字段中应包含的信息类型的指导。 如果将这些字段填充到与每个单独系统相关的数据，系统管理员就能够远程标识和管理这些系统。 计算机硬件 Id （CHIDs）是使用这些表中的值生成的，并且应考虑到设置这些值。

若要将一致性添加到 SMBIOS 以更好地标识设备信息，我们建议在填充 SMBIOS 字段时将以下内容作为指导。 下面的 SMBIOS 数据也将在各种容量中收集和使用。 在使用 BIOS/固件供应商提供的工具进行填充之前，应详细规划进入这些字段的数据。 为子目标生成的哈希基于填充这些字段的数据。

尽管此信息类似于[Windows 10 驱动程序发布工作流](https://download.microsoft.com/download/B/A/8/BA89DCE0-DB25-4425-9EFF-1037E0BA06F9/windows10_driver_publishing_workflow.docx)中所列的信息，但下表为某些字段规定了额外的详细信息级别，从而提高了相应的程度。

## <a name="recommended-settings-when-moving-to-smbios-30"></a>移动到 SMBIOS 3.0 时的推荐设置

<table>
    <tbody>
        <tr>
            <td>字段名称</b></td>
            <td><b>结构名称和类型</b></td>
            <td><b>值</b></td>
            <td><b>抵销</b></td>
            <td><b>长度</b></td>
            <td><b>示例方案</b></td>
            <td><b>示例</b></td>
        </tr>
        <tr>
            <td>制造商</td>
            <td>系统信息(类型 1)</td>
            <td>字符串</td>
            <td>04h</td>
            <td>32</td>
            <td rowspan="8">Contoso，Inc. 2 产品线：1） "A" 系列和2） "B" 系列。 "A" 系列设备包括 Contoso "A11" 和 "A13" 设备子品牌，其中每个设备都具有不同的屏幕尺寸，并支持可物理分离的键盘（尽管键盘作为选项出售）。 "A11" 有三个模型：1）基础模型（a110001）2）使用高级音频包（a110002）和3）的中型模型具有较高分辨率的触摸面板（a110003）。 每个模型都已经历几个基板版本的生成，这些版本由代码 bb01 到 bb04 内部标识。 可以通过不同的存储和内存配置进一步自定义每个 "A11" 模型。 为了将不同的生产运行分到不同的生产车间，Contoso 使用了一种内部标识系统，该系统将系列、产品名称、市场区域和生产运行号结合起来。</td>
            <td>“Contoso”</td>
        </tr>
        <tr>
            <td>系列</td>
            <td>系统信息(类型 1)</td>
            <td>字符串</td>
            <td>1Ah</td>
            <td>64</td>
            <td>A11</td>
        </tr>
        <tr>
            <td>产品名称</td>
            <td>系统信息(类型 1)</td>
            <td>字符串</td>
            <td>05h</td>
            <td>64</td>
            <td>"A11 a110001"</td>
        </tr>
        <tr>
            <td>基板产品</td>
            <td>基板信息（类型2）</td>
            <td>字符串</td>
            <td>05h</td>
            <td>32</td>
            <td>"bb03"</td>
        </tr>
        <tr>
            <td>KU 编号</td>
            <td>系统信息(类型 1)</td>
            <td>字符串</td>
            <td>19h</td>
            <td>32</td>
            <td>"A11a11001-04"</td>
        </tr>
        <tr>
            <td>序列号</td>
            <td>系统信息(类型 1)</td>
            <td>字符串</td>
            <td>07h</td>
            <td></td>
            <td>"A1B2C3456789ABC"</td>
        </tr>
        <tr>
            <td>UUID</td>
            <td>系统信息(类型 1)</td>
            <td>变化不定</td>
            <td>08h</td>
            <td>16</td>
            <td>通用唯一 ID 号<br>请参阅7.2.1 部分。 在<a href="https://www.dmtf.org/standards/smbios">DMTF SMBIOS 规范 3.1</a>或更高版本中。</td>
        </tr>
        <tr>
            <td>机箱类型</td>
            <td>系统机箱(类型 3) </td>
            <td>字节</td>
            <td>05h</td>
            <td>N/A</td>
            <td>可拆分</td>
        </tr>
        <tr>
            <td>BIOS 供应商</td>
            <td>BIOS 信息(类型 0)</td>
            <td>字节</td>
            <td>04h</td>
            <td>字符串</td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>BIOS 版本 </td>
            <td>BIOS 信息(类型 0)</td>
            <td>字节</td>
            <td>05h</td>
            <td>字符串</td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>BIOS 主要版本</td>
            <td>BIOS 信息(类型 0)</td>
            <td>字节</td>
            <td>14h</td>
            <td>变化不定</td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>BIOS 次要版本</td>
            <td>BIOS 信息(类型 0)</td>
            <td>字节</td>
            <td>15h</td>
            <td>变化不定</td>
            <td></td>
            <td></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> 从**BIOS**开始的 SMBIOS 字段可能被视为可选或建议。 它们用于构建**计算机硬件 ID （子）** ，并确保生成的子中的其他唯一性级别。

<table>
    <tbody>
        <tr>
            <td><b>字段名称</b></td>
            <td><b>DTMF.org 说明</b></td>
            <td><b>Microsoft 说明</b></td>
            <td><b>字段格式</b></td>
            <td><b>层次结构</b></td>
        </tr>
        <tr>
            <td>制造商</td>
            <td>以 null 结尾的字符串的数目。</td>
            <td>"<b>制造商</b>" 字段中的值标识将设备推销给最终用户的公司品牌名称。 （例如，设备上的品牌名称或徽标 imprinted）</td>
            <td><b>制造商</b>字段字符串的格式与最终用户识别为公司品牌的格式匹配。</td>
            <td>"<b>制造商</b>" 字段是最终用户的第一层指标，表示公司销售的所有设备的分组。 此字段应极少发生更改。</td>
        </tr>
        <tr>
            <td>系列</td>
            <td>以 null 结尾的字符串的数目。</td>[https://blogs.technet.microsoft.com/askperf/2008/11/18/disabling-unnecessary-services-a-word-to-the-wise/](&gt;) <td>"系列" 字段中的值标识公司的子品牌名称，该名称特定于一组类似设备，该名称特定于将设备推销给最终用户的一系列类似设备。 <b>系列</b>值不包括按组件、设备生成、制造年份、SKU 或其他因素的方差。 "<b>系列</b>" 值通常不够具体，不能指示实际设备，而是产品线推销给最终用户。</td>
            <td><b>系列</b>字段字符串的格式与最终用户将标识为公司的子品牌名称（特定于产品线）的格式匹配。 <b>系列</b>字段字符串不应包含<b>制造商</b>名称。</td>
            <td>"<b>系列</b>" 字段是最终用户的二级指标，表示一组类似的设备，称为 "产品系列"。 此字段在产品系列的生命周期中应保持一致。</td>
        </tr>
        <tr>
            <td>产品名称</td>
            <td>以 null 结尾的字符串的数目。</td>
            <td>"<b>产品名称</b>" 字段中的值标识公司的特定设备型号，而不枚举配置方差。 （例如，处理器、内存和存储差异）通常，某些<b>产品名称</b>特定于特定<b>系列</b>中的模型，但通常不会超过数十个。</td>
            <td><b>Product name</b>字段字符串的格式与最终用户看到的设备型号名称或标识符值匹配。 建议包括系列字段的完整值，后跟一个空格，然后是模型名称/标识符值。</td>
            <td>"<b>产品名称</b>" 字段是最终用户的第三级指标，表示设备的特定型号。 <b>产品名称</b>可能持续于<b>系列</b>的生存期内，因为硬件的多个修订版或硬件修订版不会推销为最终用户的新产品。</td>
        </tr>
        <tr>
            <td>基板产品</td>
            <td>以 null 结尾的字符串的数目。</td>
            <td>"<b>基板 product</b> " 字段中的值用于标识基板，并应在同一<b>家族</b>和<b>产品名称</b>中准确反映不同设备上的基板之间的差异。 在设备模型中的底板发生更改时，此值必须更改，并且可以将其用作服务的资源标识符。</td>
            <td>"<b>基板产品</b>" 字段字符串的格式可由 "公司" 设置，并且不需要与最终用户营销信息一致。</td>
            <td><b>基板 product</b>字段是设备到公司的第四个级别的指标，不会推销给最终用户。 </td>
        </tr>
        <tr>
            <td>序列号</td>
            <td>以 null 结尾的字符串的数目。</td>
            <td>此结构中的信息定义了整个系统的属性，并将其与系统 MIF 的组件 ID 组相关联。 SMBIOS 实现与单个系统实例相关联，并且包含一个且仅包含一个系统信息（类型1）结构。</td>
            <td><b>序列号</b>字段字符串的格式与设备外部的序列号匹配。</td>
            <td>"<b>序列号</b>" 字段是从公司分配的序列号的指示器，可在设备外部访问。 "<b>序列号</b>" 字段是设备的第六级指示器。</td>
        </tr>
        <tr>
            <td>UUID</td>
            <td>UUID 是在时间和空间之间唯一设计的标识符。 它不需要中央注册过程。 UUID 长度为128位。 格式在 RFC4122 中进行了介绍。</td>
            <td>此结构中的值是规范文档中定义的全局唯一值。 此值用于与此特定计算机关联。</td>
            <td>字段格式遵循最新的 DTMF.org SMBIOS 规范文档来满足通用唯一性。</td>
            <td>"UUID" 字段不会推销给最终用户，被视为此设备的第七个级别的指标。</td>
        </tr>
        <tr>
            <td>SKU 号</td>
            <td>以 null 结尾的字符串的数目。 此文本字符串标识用于销售的特定计算机配置。 有时也将它称为产品 ID 或采购订单号。 此编号通常会在现有字段中找到，但是没有标准格式。 通常，对于给定 OEM 的给定系统板，会有数十个独特的处理器、内存、硬盘驱动器和光驱配置。</td>
            <td>" <b>SKU 编号</b>" 字段中的值用可以由公司确定的格式标识设备。 此字段可能包含由生产运行、装运区域、零售商、配置差异决定的设备的变体。 （例如，处理器、内存和存储差异）此值可用作用于维护的资产标识符，如果公司未使用此值，则可以将其留空。</td>
            <td><b>SKU 编号</b>字段字符串的格式可由公司设置，而不需要与最终用户营销信息保持一致。</td>
            <td><b>SKU 编号</b>字段是设备到公司的第五个级别的指标，不会推销给最终用户。</td>
        </tr>
        <tr>
            <td>机箱类型</td>
            <td>N/A</td>
            <td>在下面的<b>箱类型</b>表中定义</td>
            <td>N/A</td>
            <td>N/A</td>
        </tr>
        <tr>
            <td>BIOS 供应商</td>
            <td>BIOS 供应商名称的字符串编号</td>
            <td>在 DMTF SMBIOS 规范3.1 或更高版本中定义</td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>BIOS 版本</td>
            <td>BIOS 版本的字符串编号。 此值是可以包含核心和 OEM 版本信息的自由格式字符串。</td>
            <td>在 DMTF SMBIOS 规范3.1 或更高版本中定义</td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>BIOS 主要版本</td>
            <td>标识系统 BIOS 的主要版本，例如，对于修订版10.22，值为0Ah，对于修订版2.1 为02h。 每次释放给定系统的系统 BIOS 更新时，都将更新此字段或系统 BIOS 次要发行版字段或两者。 如果系统不支持使用此字段，则此字段和系统 BIOS 次要发行版字段的值都为 FFh。</td>
            <td>在 DMTF SMBIOS 规范3.1 或更高版本中定义</td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>BIOS 次要版本</td>
            <td>标识系统 BIOS 的次版本，例如，对于修订版10.22，值为16h，对于修订版2.1 为01h。</td>
            <td>在 DMTF SMBIOS 规范3.1 或更高版本中定义</td>
            <td></td>
            <td></td>
        </tr>
    </tbody>
</table>

下表描述了 "**机箱类型**" 字段的设置。

<table>
    <tbody>
        <tr>
            <td><b>机箱类型</b></td>
            <td><b>字节值</b></td>
            <td><b>OHR FFC/FFSC</b></td>
            <td><b>Microsoft 说明</b></td>
        </tr>
        <tr>
            <td>桌面</td>
            <td>03h</td>
            <td>桌面/标准版</td>
            <td><b>桌面</b>指的是塔式机箱中的客户系统，而不是可移植的客户系统。 它不包含集成的显示和输入。</td>
        </tr>
        <tr>
            <td>笔记本</td>
            <td>0Ah</td>
            <td>笔记本/标准版</td>
            <td><b>笔记本</b>是指具有 clamshell 外形规格并具有不可分离键盘的客户系统。 识别<b>笔记本</b>时，不使用可移植（08h）或便携式计算机（09h）。 </td>
        </tr>
        <tr>
            <td>一体</td>
            <td>0Dh</td>
            <td>桌面/AiO</td>
            <td><b>"一体式"</b>指的是将触摸屏与单个机箱中的其他硬件组件集成的客户系统。</td>
        </tr>
        <tr>
            <td>Tablet</td>
            <td>1Eh</td>
            <td>平板电脑/标准版</td>
            <td><b>Tablet</b>表示将显示器、充电电源和其他组件合并到单个机箱中的客户系统，并使用触控作为输入的主要方式。 它不包含实际连接的键盘。 如果客户系统的外形规格不允许键盘以物理方式连接到机箱，但将蓝牙或其他无线键盘作为可选附件出售给最终用户，则会将 "<b>机箱类型</b>" 字段标识为<b>平板电脑</b>。</td>
        </tr>
        <tr>
            <td>变形本</td>
            <td>1Fh</td>
            <td>笔记本/可转换</td>
            <td><b>可转换</b>是指将显示器、充电电源和点设备组合到单个机箱中的客户系统（任何运动：翻转、swivels、翻转）显示为向前或远离连接的键盘。</td>
        </tr>
        <tr>
            <td>可分离电脑</td>
            <td>20h</td>
            <td>平板电脑/标准版</td>
            <td>可<b>分离</b>表示将显示器、充电电源和指针设备组合到一个机箱中的客户系统，以及一个可分离的键盘。 如果客户系统的外形规格允许键盘（不包括蓝牙或其他无线键盘）以物理方式连接到机箱，但会将物理键盘作为可选附件出售给最终用户，则会将 "<b>机箱类型</b>" 字段标识为可<b>分离</b>。</td>
        </tr>
    </tbody>
</table>

## <a name="related-resources"></a>相关资源

[Windows 10 驱动程序发布工作流](https://download.microsoft.com/download/B/A/8/BA89DCE0-DB25-4425-9EFF-1037E0BA06F9/windows10_driver_publishing_workflow.docx) 

[SMBIOS DMTF 规范](https://www.dmtf.org/standards/smbios)
