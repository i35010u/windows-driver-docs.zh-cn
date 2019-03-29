---
title: SMBIOS
description: SMBIOS 规范定义数据结构和会提供与系统相关的数据结构的信息。
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 81046d457daa15e0cd9a7c694d42ecd19d621ad9
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464355"
---
# <a name="smbios"></a>SMBIOS

SMBIOS 规范定义数据结构和会提供与系统相关的数据结构的信息。 通过使用最新的 SMBIOS 规范，我们及时了解最新规范中定义的更改。 下表介绍在这些字段中应为哪种类型的信息以及指南建议的 SMBIOS 设置。 具有与每个单独的系统相关的数据填充这些字段允许系统管理员能够远程标识和管理这些系统。 使用这些表中的值生成计算机硬件 Id (CHIDs) 和谨慎，并且认为应授予给这些设置。

若要添加 SMBIOS 以更好地识别设备信息就能实现一致性，我们建议以下内容作为指导时填入 SMBIOS 字段。 下面的 SMBIOS 数据还收集并在各种容量中使用。 填充使用由 BIOS/固件供应商提供的工具之前，应详细规划数据不断进入这些字段。 为 CHID 目标生成的哈希基于填充这些字段的数据。

尽管此信息中列出的类似[Windows 10 驱动程序发布工作流](http://download.microsoft.com/download/B/A/8/BA89DCE0-DB25-4425-9EFF-1037E0BA06F9/windows10_driver_publishing_workflow.docx)下, 表指定其他级别的详细信息的一些字段，提高特异性的级别。

## <a name="recommended-settings-when-moving-to-smbios-30"></a>将移动到 SMBIOS 3.0 时的推荐的设置

<table>
    <tbody>
        <tr>
            <td>字段名称</b></td>
            <td><b>结构名称和类型</b></td>
            <td><b>值</b></td>
            <td><b>Offset</b></td>
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
            <td rowspan="8">Contoso，Inc.制造 2 产品系列："1） a"系列和"2） B"系列。 "A"系列的设备包括 Contoso"A11"和"A13"设备子品牌，其中每个具有不同屏幕大小和都支持以物理方式拆离键盘 （尽管键盘作为一个选项来出售）。 "A11"具有三个模型：1) 基模型 (a110001) 具有高级音频包 (a110002) 2） 的中型模型和具有较高的分辨率 3） 的高端模型触摸屏 (a110003)。 每个模型经历几代基板修订代码 bb01 bb04 通过在内部标识。 每个"A11"模型可以进一步自定义具有不同的存储和内存配置。 若要将不同的生产运行其生产车间，Contoso 使用结合了系列、 产品名称、 市场区域和生产环境运行数的内部标识系统。</td>
            <td>“Contoso”</td>
        </tr>
        <tr>
            <td>系列</td>
            <td>系统信息(类型 1)</td>
            <td>字符串</td>
            <td>1Ah</td>
            <td>64</td>
            <td>"A11"</td>
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
            <td>基板信息 （类型 2）</td>
            <td>字符串</td>
            <td>05h</td>
            <td>32</td>
            <td>"bb03"</td>
        </tr>
        <tr>
            <td>KU 数</td>
            <td>系统信息(类型 1)</td>
            <td>字符串</td>
            <td>19h</td>
            <td>32</td>
            <td>"A11a11001-EU-04"</td>
        </tr>
        <tr>
            <td>序列号</td>
            <td>系统信息(类型 1)</td>
            <td>字符串</td>
            <td>07 h</td>
            <td></td>
            <td>"A1B2C3456789ABC"</td>
        </tr>
        <tr>
            <td>UUID</td>
            <td>系统信息(类型 1)</td>
            <td>变化不定</td>
            <td>08h</td>
            <td>16</td>
            <td>通用的唯一 ID 号<br>请参阅部分 7.2.1。 在中<a href="http://www.dmtf.org/standards/smbios">DMTF SMBIOS 规范 3.1</a>或更高版本。</td>
        </tr>
        <tr>
            <td>机箱类型</td>
            <td>系统机箱(类型 3) </td>
            <td>Byte</td>
            <td>05h</td>
            <td>不可用</td>
            <td>"detachable"</td>
        </tr>
        <tr>
            <td>BIOS 供应商</td>
            <td>BIOS 信息(类型 0)</td>
            <td>Byte</td>
            <td>04h</td>
            <td>字符串</td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>BIOS 版本 </td>
            <td>BIOS 信息(类型 0)</td>
            <td>Byte</td>
            <td>05h</td>
            <td>字符串</td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>主要的 BIOS 版本</td>
            <td>BIOS 信息(类型 0)</td>
            <td>Byte</td>
            <td>14h</td>
            <td>变化不定</td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>BIOS 次要版本</td>
            <td>BIOS 信息(类型 0)</td>
            <td>Byte</td>
            <td>15h</td>
            <td>变化不定</td>
            <td></td>
            <td></td>
        </tr>
    </tbody>
</table>

**请注意**SMBIOS 字段开头**BIOS**可能被视为可选或建议。 使用这些构建**计算机的硬件 ID (CHID)** ，并确保更高级别的中生成 CHID 的唯一性。

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
            <td>以 null 结尾的字符串数。</td>
            <td>中的值<b>制造商</b>字段标识设备销售给最终用户在其下需要的公司品牌名称。 （例如，品牌名称或徽标印刷在设备上）</td>
            <td>格式<b>制造商</b>字段字符串是以匹配最终用户标识为公司的品牌。</td>
            <td><b>制造商</b>字段是向最终用户，表示由该公司销售的所有设备的分组的第一级别指标。 此字段应很少，如果曾有过更改。</td>
        </tr>
        <tr>
            <td>系列</td>
            <td>以 null 结尾的字符串数。</td>&gt; <td>Familyf 字段中的值，标识公司子品牌名称，作为产品系列，设备销售给最终用户在其下需要知道特定于类似的设备的分组。 <b>系列</b>值不包括由组件、 设备生成、 生产的年度、 SKU 或其他因素的方差。 <b>系列</b>值通常不是足够明确，以便指示实际设备，但被标记为最终用户而不是产品系列。</td>
            <td>格式<b>系列</b>字段字符串是以匹配最终用户标识为公司的子品牌名称，特定于产品系列。 <b>系列</b>字段字符串不应包含<b>制造商</b>名称。</td>
            <td><b>系列</b>字段是向最终用户的第二级别指标，表示一组类似的设备称为产品系列。 此字段应保持一致的产品系列生命周期。</td>
        </tr>
        <tr>
            <td>产品名称</td>
            <td>以 null 结尾的字符串数。</td>
            <td>中的值<b>产品名称</b>字段标识公司的特定型号的设备，而无需枚举配置变体。 （例如，处理器、 内存和存储的变体）有多个通常<b>产品名称</b>特定模型中特定于<b>系列</b>，尽管通常不超过一打或使。</td>
            <td>格式<b>产品名称</b>字段字符串将与最终用户看到作为设备模型的名称或标识符值匹配。 建议是包含后跟一个空格和模型名称/标识符值系列字段的完整值。</td>
            <td><b>产品名称</b>字段是向最终用户，表示设备的特定模型的第三级指示器。 一个<b>产品名称</b>的生存期内可能持续<b>系列</b>、 通过多个修订或其中硬件修订不被最终用户的新产品的硬件代次。</td>
        </tr>
        <tr>
            <td>基板产品</td>
            <td>以 null 结尾的字符串数。</td>
            <td>中的值<b>基板产品</b>字段标识基板，并且应在相同的不同设备上准确反映中功能的主板的方差<b>系列</b>和<b>产品名称</b>. 设备模型更改且基板可能用作维护资产标识符时，必须更改此值。</td>
            <td>格式<b>基板产品</b>可以通过公司，设置字段字符串，它不需要为市场营销信息的最终用户与对齐。</td>
            <td><b>基板产品</b>字段是公司设备的第四级指标，并向最终用户不被标记。 </td>
        </tr>
        <tr>
            <td>序列号</td>
            <td>以 null 结尾的字符串数。</td>
            <td>此结构中的信息定义整个系统的属性，用于与系统的 MIF 组件 ID 组相关联。 SMBIOS 实现与单个系统实例相关联，并包含一个且只有一个系统信息 (类型 1) 结构。</td>
            <td>格式<b>序列号</b>字段字符串将匹配的外部环的设备上的序列号。</td>
            <td><b>序列号</b>域是指示器的公司中分配的序列号，它可在外部的设备上访问。 <b>序列号</b>字段是设备的第六个级别指标。</td>
        </tr>
        <tr>
            <td>UUID</td>
            <td>UUID 是设计的标识符是唯一在之间的时间和空间。 它要求任何中心的注册过程。 UUID 为 128 位的长度。 RFC4122 描述了格式。</td>
            <td>此结构中的值是一个全局唯一值的规范文档中定义。 此值被用于与此特定计算机相关联。</td>
            <td>字段格式遵循最新的 DTMF.org SMBIOS 规范文档，以满足通用的唯一性。</td>
            <td>UUID 字段不被标记为最终用户，并被视为此设备的第七个级别指示器。</td>
        </tr>
        <tr>
            <td>SKU 号</td>
            <td>以 null 结尾的字符串数。 此文本字符串标识特定计算机配置的销售。 有时也将它称为产品 ID 或采购订单号。 此编号通常会在现有字段中找到，但是没有标准格式。 通常，对于给定 OEM 的给定系统板，会有数十个独特的处理器、内存、硬盘驱动器和光驱配置。</td>
            <td>中的值<b>SKU 编号</b>字段用于标识一种格式，也可由公司中的设备。 此字段可能包含由运行时，发货区域、 零售商、 配置的方差的生产设备的差异。 （例如，处理器、 内存和存储的变体）此值可以用作维护资产标识符，如果它不由公司，它可能留空。</td>
            <td>格式<b>SKU 编号</b>可以通过公司，设置字段字符串，它不需要为市场营销信息的最终用户与对齐。</td>
            <td><b>SKU 编号</b>字段是公司的设备的第五级指标和不被标记为最终用户。</td>
        </tr>
        <tr>
            <td>机箱类型</td>
            <td>不可用</td>
            <td>在中定义<b>机箱类型</b>下表</td>
            <td>不可用</td>
            <td>不可用</td>
        </tr>
        <tr>
            <td>BIOS 供应商</td>
            <td>BIOS 供应商的名称的字符串数</td>
            <td>DMTF SMBIOS 规范 3.1 或更高版本中定义</td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>BIOS 版本</td>
            <td>字符串 BIOS 版本的数。 此值是一个自由格式字符串可能包含核心应用程序和 OEM 版本信息。</td>
            <td>DMTF SMBIOS 规范 3.1 或更高版本中定义</td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>主要的 BIOS 版本</td>
            <td>标识的主要版本，如系统 bios 的值是 0Ah 修订版 10.22 和 02 h 的修订版本 2.1。 发布给定系统的系统 BIOS 更新每次都会更新此字段和/或系统 BIOS 次要版本字段。 如果系统不支持使用此字段，值为 FFh 此字段和系统 BIOS 次要版本字段。</td>
            <td>DMTF SMBIOS 规范 3.1 或更高版本中定义</td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>BIOS 次要版本</td>
            <td>标识的次要版本，如系统 bios 的值是 16 小时的修订 10.22 和 01 h 的修订版本 2.1。</td>
            <td>DMTF SMBIOS 规范 3.1 或更高版本中定义</td>
            <td></td>
            <td></td>
        </tr>
    </tbody>
</table>


下表描述的设置**机箱类型**字段。

<table>
    <tbody>
        <tr>
            <td><b>机箱类型</b></td>
            <td><b>字节值</b></td>
            <td><b>OHR FFC/FFSC</b></td>
            <td><b>Microsoft 说明</b></td>
        </tr>
        <tr>
            <td>桌面设备</td>
            <td>03 h</td>
            <td>桌面/标准版</td>
            <td><b>桌面</b>意味着 tower 用例中的客户系统并不是可移植的客户系统。 它不包括集成的显示器和输入。</td>
        </tr>
        <tr>
            <td>笔记本</td>
            <td>0Ah</td>
            <td>Notebook/标准版</td>
            <td><b>Notebook</b>意味着客户系统采用蛤外观造型和具有非可拆分的键盘。 可移植 (08 h) 或便携式计算机 (09 h) 将不被用于标识时<b>Notebook</b>。 </td>
        </tr>
        <tr>
            <td>-一体</td>
            <td>0Dh</td>
            <td>Desktop/AiO</td>
            <td><b>一体</b>意味着与单一机箱中的其他硬件组件集成触摸屏的客户系统。</td>
        </tr>
        <tr>
            <td>Tablet</td>
            <td>1Eh</td>
            <td>平板电脑/标准版</td>
            <td><b>平板电脑</b>意味着客户系统，将显示、 可再充电的电源和其他组件合并到单个机箱，并且利用触控作为其主要输入方式。 它不包括以物理方式附加的键盘。 在其中客户系统的外形规格不允许使用键盘来以物理方式连接到机箱，但 Bluetooth 或其他无线键盘作为可选附件出售给最终用户的情况下<b>机箱类型</b>字段将被视为<b>平板电脑</b>。</td>
        </tr>
        <tr>
            <td>变形本</td>
            <td>1Fh</td>
            <td>Notebook/可转换为</td>
            <td><b>可转换为</b>意味着客户系统，它将显示、 可再充电的电源和点设备到单一机箱合并具有可调整 (任何动作： 翻转、 旋转、 打开) 显示朝前或背向附加键盘。</td>
        </tr>
        <tr>
            <td>可分离电脑</td>
            <td>20h</td>
            <td>平板电脑/标准版</td>
            <td><b>可拆分</b>意味着将显示、 可再充电的电源和指针设备组合成单个机箱拆离键盘以及客户系统。 在其中客户系统的外形规格使得键盘，不包括 Bluetooth 打印机或其他无线键盘以物理方式连接到机箱，但实际键盘作为可选附件形式出售给最终用户的情况下<b>机箱类型</b>字段将被视为<b>Detachable</b>。</td>
        </tr>
    </tbody>
</table>


## <a name="related-resources"></a>相关资源

[发布工作流的 Windows 10 驱动程序](http://download.microsoft.com/download/B/A/8/BA89DCE0-DB25-4425-9EFF-1037E0BA06F9/windows10_driver_publishing_workflow.docx) 

[SMBIOS DMTF 规定](http://www.dmtf.org/standards/smbios)                                                 



