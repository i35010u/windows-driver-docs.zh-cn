---
title: 切片器设置
description: 配置文件 XML 包含许多需要为特定3D 打印机设备进行调整的设置，以控制向 Windows 中的3D 打印对话框公开的打印功能。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 369ccbe08e3c43a375bda624841adef5c8dc0d3e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788006"
---
# <a name="slicer-settings"></a>切片器设置


配置文件 XML 包含许多需要为特定3D 打印机设备进行调整的设置，以控制向 Windows 中的3D 打印对话框公开的打印功能。 这些设置还控制 Microsoft 3D 切片器 ( # A0 和依存关系) 运行参数。  

## <a name="slicer-settings"></a>切片器设置


<table>

<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>

<thead>
<tr class="header">
<th>设置 (XML 路径) </th>
<th>更改</th>
<th>描述</th>
</tr>
</thead>

<tbody>

<tr>
<td><p>psk3d:Job3DOutputArea\ </p>
<p>psk3d:Job3DOutputAreaWidth</p>
<p>psk3d:Job3DOutputArea\ </p>
<p>psk3d:Job3DOutputAreaDepth</p>
<p>psk3d:Job3DOutputArea\ </p>
<p>psk3d:Job3DOutputAreaHeight</p></td>
<td><p>是</p></td>
<td><p>Microns 中的打印音量，按宽度 (x 最大) 、深度 (y 最大) 和高度 (z 最大) 。</p>
<p>卷应表示物理设备的功能，这是在发布驱动程序时证书阶段中的一个测试，可确保打印机可以使用声明的卷。</p></td>
</tr>


<tr>
<td><p>psk3d:Job3DOutputArea\ </p>
<p>psk3d:Job3DOutputAreaOffsetX</p>
<p>psk3d:Job3DOutputArea\ </p>
<p>psk3d:Job3DOutputAreaOffsetX</p></td>
<td><p>可选</p></td>
<td><p>打印卷相对于 (0，0) 的 X 和 Y 偏移量。 这允许支持3D 打印机，其中 (0，0) 位于平台中心 (典型的增量打印机) 或打印机，其中 (0，0) 不在打印平台的左上角。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3ds:extruders\  </p></td>
<td><p>可选</p></td>
<td><p>打印机中 extruders 的数目。 此设置控制将 XML 中的后续 psk3d：材料 &lt; &gt; 饰部分作为打印功能发送到 "打印" 对话框中的多少个。 如果未指定，驱动程序将采用单个 extruder 打印机。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3d：材料 &lt; 材料&gt;\ </p>
<p>psk： DisplayName</p></td>
<td><p>是</p></td>
<td><p>材料的显示名称。 这可以是显示在用于用户分配的 3D "打印" 对话框中的任何字符串。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3d：材料 &lt; 材料&gt;\ </p>
<p>psk： MaterialColor</p></td>
<td><p>是</p></td>
<td><p>3D 打印对话框中材料呈现的 RGB 或 RGBA 颜色。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3d：材料 &lt; 材料&gt;\ </p>
<p>psk： MaterialType</p></td>
<td><p>预留</p></td>
<td><p>用于3D 打印的打印架构关键字中定义的材料类型 (例如，"psk3d： PLA" ) 。 使用名称和颜色指定的通用材料时，此设置将被弃用。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3d：材料 &lt; 材料&gt;\ </p>
<p>psk3dx:platformtemperature</p></td>
<td><p>是</p></td>
<td><p>打印时应加热打印平台) 温度 (摄氏温度。 值0表示不应加热床。</p>
<p>稍后可通过预命令中的 <em>$platformtemperature $</em> template 引用此值。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3d：材料 &lt; 材料&gt;\ </p>
<p>psk3dx:filamentdiameter</p></td>
<td><p>是</p></td>
<td><p>3D 打印机中加载的 filament 的 microns 直径。 例如，1750是标准的 1.75 mm filament。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3d：材料 &lt; 材料&gt;\ </p>
<p>psk3dx:filamentcalibrationoverride</p></td>
<td><p>可选</p></td>
<td><p>调整 filament 流的一个因素。 它作为传入 filament 跨节 (的比率应用于 filamentdiameter) ，以调整延伸速度。 如果此系数大于1.0，将会拉伸较少的塑料。 这是一个优化参数，应始终接近1.0。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3d：材料 &lt; 材料&gt;\ </p>
<p>psk3dx:extrudertemperature</p></td>
<td><p>是</p></td>
<td><p>当凸出时，extruder/热端应加热到的温度（摄氏度温度）。 可以通过预命令中的 <em>$extrudertemperature $</em> 模板来引用此值。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3d：材料 &lt; 材料&gt;\ </p>
<p>psk3dx:autocenter</p></td>
<td><p>可选</p></td>
<td><p>一个 (0 或 1) 的布尔值，该值指示模型是否应在 XY 平面) 上 (的打印平台上居中。 如果该模型不适合打印音量，该模型也会自动居中。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\  </p>
<p>psk3d：材料 &lt; 材料&gt;\  </p>
<p>psk3dx:SetupCommands\ </p>
<p>psk3dx：命令</p></td>
<td><p>是</p></td>
<td><p>要用作材料设置的命令的列表。 这通常是在预命令期间执行的 G 代码，用于控制喷嘴预加热、填充等。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\  </p>
<p>psk3d：材料 &lt; 材料&gt;\  </p>
<p>psk3dx:SelectCommands\ </p>
<p>psk3dx：命令</p></td>
<td><p>是</p></td>
<td><p>需要在打印时使用的一系列命令。 通常，这是执行的 G 代码： T0/T1 extruder 选择、喷嘴擦除序列、打开/关闭风扇、收回材料、温度等。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\  </p>
<p>psk3d：材料 &lt; 材料&gt;\  </p>
<p>psk3dx:DeselectCommands\ </p>
<p>psk3dx：命令</p></td>
<td><p>是</p></td>
<td><p>在打印过程中发布材料时要发出的命令的列表。 通常，这是执行的 G 代码：收回材料，停止喷嘴，降低温度，等等。</p></td>
</tr>

<tr>
<td><p>psk3dx:customStatus</p></td>
<td><p>可选</p></td>
<td><p>表示初始打印作业状态的字符串，通常为切片阶段。 如果缺少，作业状态将设置为 "打印"。 通常，在呈现筛选器中发生切片时，此值应设置为 "切片"，例如，使用 Microsoft 切片器时。</p></td>
</tr>

<tr>
<td><p>psk3dx:userprompt</p></td>
<td><p>是</p></td>
<td><p>在打印开始之前以用户提示形式显示的消息。 此提示用于阻止 extruder 崩溃进入需要手动删除打印的设备上的现有打印。</p>
<p>对于可以在打印开始或结束时在设备上显示提示的设备，不需要此设置。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： debug \ </p>
<p>psk3dx：日志</p></td>
<td><p>可选</p></td>
<td><p>当存在时，此设置使驱动程序可以对文件进行调试日志记录，使开发人员能够检查 G 代码和固件响应。</p>
<p>还可以通过注册表项全局打开此设置 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Print</p>
<p>StandardGCodeDebugLog = "c:\Path\To\LogFile"</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx：通信 \ </p>
<p>psk3dx：连接 \ </p>
<p>psk3dx： comport</p></td>
<td><p>可选</p></td>
<td><p>串行端口名称的 URI。 当存在时，此设置将替代 COM 端口的驱动程序自动解析 (打印机队列- &gt; 打印机端口名称- &gt; Enum\3DPrinter\Device- &gt; Enum\USB\Serial 设备) 。 这允许暂时打印到没有最终硬件 Id 的设备。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx：通信 \ </p>
<p>psk3dx：连接 \ </p>
<p>psk3dx：波特率</p></td>
<td><p>可选</p></td>
<td><p>连接的设备的串行连接波特率。 典型值为115200或250000。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx：通信 \ </p>
<p>psk3dx：连接 \ </p>
<p>psk3dx： mode</p></td>
<td><p>预留</p></td>
<td><p>此设置控制在连接时重置 (DTR 设置) 。 如果设备无法连接，则使用值1或3。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx：通信 \  </p>
<p>psk3dx：连接 \ </p>
<p>psk3dx：协议</p></td>
<td><p>预留</p></td>
<td><p>此设置非常实验，并控制固件的通信协议。 如果未指定，则驱动程序默认为带有 RepRap/Marlin 校验和的 ASCII G 代码。 如果设置为2，则驱动程序可以发送二进制 G 代码。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx：通信 \ </p>
<p>psk3dx：连接 \ </p>
<p>psk3dx：超时</p></td>
<td><p>预留</p></td>
<td><p>打印机响应的超时值（以毫秒为单位）。 使用 0 (默认值) 无超时值。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： python-customcommands \ </p>
<p>psk3dx:initcommands\ </p>
<p>psk3dx：命令</p></td>
<td><p>是</p></td>
<td><p>切片前发送的命令序列。 这些命令是与切片器并行执行的。 这通常是一系列 G 代码命令，可将打印机从一系列 "校准"、"自动" 和/或 "散热" 到接近的最终温度。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： python-customcommands \ </p>
<p>psk3dx:precommands\ </p>
<p>psk3dx：命令</p></td>
<td><p>是</p></td>
<td><p>要在每个作业开始时发送的一组 G 代码命令，通常用于初始化3D 打印机，例如，将 extruder 上滑并加热到最终温度并填充 extruder。 每个设备都有不同的所需预命令。 每行 G 代码都应出现在子 &lt; command 元素中 &gt; 。 要由引用的设置替换的变量可以声明为名称（以 "$" 字符分隔），例如， &lt; command &gt; M104 <em>S $ extrudertemperature $</em> &lt; /command &gt; 。 有关内置变量，请参阅下一部分。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： python-customcommands \ </p>
<p>psk3dx:postcommands\ </p>
<p>psk3dx：命令</p></td>
<td><p>是</p></td>
<td><p>要在每个作业结束时发送的一组 G 代码命令，通常是为了使3D 打印机处于一种安全状态，例如向下 extruder，然后将部件从 extruder/热端移出，使其从床中轻松删除。 每个设备都有不同的必需 post 命令。</p>
<p>取消作业时也会执行此序列。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： python-customcommands \ </p>
<p>psk3dx:failsafepostcommands\ </p>
<p>psk3dx：命令</p></td>
<td><p>可选</p></td>
<td><p>一组要作为失败安全机制发送的 G 代码命令，例如，切片器错误。 如果缺少，驱动程序将执行 "M110 N0" 后跟 "M104 S0"。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:layerthickness</p></td>
<td><p>是</p></td>
<td><p>Microns 中层的 (z 高度) 的粗细。 应根据计算机的物理分辨率来定义此值，以最大程度地减少定位错误。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:maxlayerthickness</p></td>
<td><p>预留</p></td>
<td><p>Microns 中的最大层厚度。</p>
<p>此设置已保留，将来可能会弃用。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:minlayerthickness</p></td>
<td><p>预留</p></td>
<td><p>Microns 中的最小层厚度。</p>
<p>此设置已保留，将来可能会弃用。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:pathwidth</p></td>
<td><p>是</p></td>
<td><p>Microns 中拉伸刀具路径的 XY 平面)  (宽度。 接近并略大于喷嘴直径的值往往会产生最佳结果。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx： shell</p></td>
<td><p>可选</p></td>
<td><p>Infill 开始之前的插入 shell 的整数。 如果值为1，则只会使一个外围，值为0时，仅 infill (非常粗略的表面完成) 。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:shelloffset</p></td>
<td><p>可选</p></td>
<td><p>Microns 中的外部 shell 的偏移量。 使用此值可以在各部分 (例如，齿轮) 的情况下，优化模型的结果。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:topsurfacelayers</p></td>
<td><p>可选</p></td>
<td><p>要在打印的上部面上填充 orchard 可靠地的整数层数。 值0使稀疏 infill 在顶部可见。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:bottomsurfacelayers</p></td>
<td><p>可选</p></td>
<td><p>要在打印的下半面上填充 orchard 可靠地的整数层数。 值0使稀疏 infill 在底部可见。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx：填充</p></td>
<td><p>预留</p></td>
<td><p>指定稀疏 infill 分式，介于0.0 和1.0 之间（含这两个值）。 0.1 (10% ) 是一个很好的默认值。 如果值为0.0，则只会输出正在打印的内核，而值1.0 将使用固态 infill 模式，而不是稀疏 infill。</p>
<p>此设置已保留，将来可能会弃用。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:fillangle</p></td>
<td><p>可选</p></td>
<td><p>填充图案的初始角度（以度为单位），沿 XY (水平) 平面以顺时针方向从 X 轴向逆时针旋转。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:filloverlap</p></td>
<td><p>预留</p></td>
<td><p>Infill 重叠 (路径宽度的0到1之间，包含) 。</p>
<p>此设置已保留，将来可能会弃用。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx：速度</p></td>
<td><p>是</p></td>
<td><p>打印移动的默认速度，以 microns/秒表示。 这是 X 和 Y 轴速度的2个标准。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:speedouter</p></td>
<td><p>是</p></td>
<td><p>外部外围 (第一 shell) 在 microns/秒的速度。 这可以设置为低于一般速度，以创建更好的打印面。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:speedfirst</p></td>
<td><p>是</p></td>
<td><p>第一层 (在 microns/秒内取代) <strong>speedouter</strong> 的速度。 这可以设置为低于一般速度来创建更好的打印平台 adhesion。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:speedtravel</p></td>
<td><p>是</p></td>
<td><p>不延伸的速度在 microns/秒内移动。 这可以设置为高于一般速度，以最大程度地减少排列，并在 extruder 是限制因素时加快打印速度。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:speedretract</p></td>
<td><p>是</p></td>
<td><p>Filament 在 microns/秒内进行收回和推回的速度。 不同于其他速度设置，这是根据输入 filament 进行测量的，而不是在 X 和 Y 轴上。 因此，此速度大约比上述速度小 20 (具体取决于 filament) 。 但是，它可以高于等效速度，因为在收回过程中不会强制塑拉伸。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx：收回</p></td>
<td><p>是</p></td>
<td><p>要收回的 filament 长度，可在 microns 中再次衡量为输入 filament。 这是进行收回和推送的对称，旨在减少旅行时喷嘴的排列和 oozing。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:supportorientationoptimization</p></td>
<td><p>预留</p></td>
<td><p>一个 (0 或 1) 的布尔值，该值指示是否自动重定向模型以最大程度地减少所需的支持。</p>
<p>此设置已保留，将来可能会弃用。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:supportoverhangangle</p></td>
<td><p>可选</p></td>
<td><p>需要支持的最大延伸角，从水平平面到模型方面的度量，以度为单位。 较小的角创建的支持结构更少。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:supportzgap</p></td>
<td><p>是</p></td>
<td><p>部分和支持之间 microns 的 Z 间距。 此设置可以减少要支持的 adhesion，使支持更易于删除。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:supportxygap</p></td>
<td><p>是</p></td>
<td><p>在 XY 平面中，支持和部件之间的微米间距。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:supportfill</p></td>
<td><p>可选</p></td>
<td><p>稀疏 infill 分数 (0 到1之间的支持，包括) 。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:raftlayers</p></td>
<td><p>可选</p></td>
<td><p>实体筏层的数目。 通常，有2个是足够的。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:raftlayerthickness</p></td>
<td><p>是</p></td>
<td><p>Microns 中筏的 Z 高度 (Z 高度) 。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:raftpathwidth</p></td>
<td><p>是</p></td>
<td><p>Microns 中筏的路径宽度。 这通常是一个较大的值，可容纳打印平台图面上的变体。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:raftfill</p></td>
<td><p>可选</p></td>
<td><p>稀疏 infill 分数 (0 到1之间的支持，包括) 。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:raftoffset</p></td>
<td><p>可选</p></td>
<td><p>Microns 中筏的大小。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:raftzgap</p></td>
<td><p>是</p></td>
<td><p>筏与对象之间 microns 的 Z 间距。 值越高，筏的删除会更容易，但可能会产生不均匀的图面。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:raftspeedfirst</p></td>
<td><p>是</p></td>
<td><p>Microns/秒筏第一层的速度。 这应该与 <strong>speedfirst</strong> 相似或更低，以便增加床 adhesion。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:coolingtime</p></td>
<td><p>可选</p></td>
<td><p>某个层的最小散热时间，以秒为单位。 该层速度会降低，这是因为它的打印时间超过了此秒数。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:mincoolingspeed</p></td>
<td><p>可选</p></td>
<td><p>每秒 microns 的最低冷却速度。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx： print \ </p>
<p>psk3dx： {quality} \ </p>
<p>psk3dx:bridgingspeed</p></td>
<td><p>是</p></td>
<td><p>在 microns 中桥接期间的延伸速度。 此值取决于计算机冷却特征和 filament 类型等因素，通常比正常打印速度慢。</p></td>
</tr>

</tbody>
</table>


**注意** 在打印节点的设置中 (psk3dx： MS3DPrinter \\ psk3dx： print \\ psk3dx： {quality} 中 \) ，{quality} 元素名称将替换为在 PrintTicket 中发送的相应 Psk3d： Quality 打印架构三维关键字设置以及打印作业。 这允许每个质量级别定义自己的一组切片器设置。 如果省略了 PrintTicket，则切片器将使用 \[ \] 用特性标记的质量设置默认值 = "true"，因此只有一个质量级别应始终定义此特性。

<table>

<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>

<thead>
<tr class="header">
<th>设置名</th>
<th>说明</th>
</tr>
</thead>
<tbody>

<tr>
<td><p>$extrudertemperature $</p>
<p>$extruder 2temperature $</p></td>
<td><p>&lt;XML 的材料部分中 psk3dx： extrudertemperature 指定的第一个和第二个 extruder 的温度 &gt; 。 这些变量将被弃用并替换为 $MaterialSetup $。</p></td>
</tr>

<tr>
<td><p>$platformtemperature $</p></td>
<td><p>&lt;列表中最后一材料中的 psk3dx： platformtemperature 条目指定的加热床温度 &gt; 。</p></td>
</tr>

<tr>
<td><p>$MaterialSetup<n>$</p></td>
<td><p>材料设置部分 &lt; psk3dx： SetupCommands &gt; 。 例如 $MaterialSetup $3 表示列表中的第三个材料，通常为第三个 extruder。</p></td>
</tr>

<tr>
<td><p>$rampup $</p></td>
<td><p>这是一个变量，可为0到255，并使用 Z 轴进行缩放，并由 &lt; &gt; 切片器质量设置中的 psk3dx： rampuptarget 控制。</p>
<p>例如，当 Z 轴增加时，命令 "M106 S $ rampup $" 会逐渐变大。 如果将 &lt; psk3dx： rampuptarget &gt; 设置为 500 microns，则在第一层上，该变量的值将为 0; 如果该层为 500 microns 或更高，则为255。</p>
<p>此变量旨在支持在加热的打印床位上更好地打印 adhesion，但可以在任何命令中使用它。</p></td>
</tr>

<tr>
<td><p>;?ack = &lt; 模式&gt;</p></td>
<td><p>此设置指示驱动程序将命令确认模式 (将打印机响应) 从默认的 "确定" 更改为临时内容，例如 ";？ack = 写入文件 "会告诉驱动程序等待确认，此时打印机已准备好写入内部存储。</p></td>
</tr>

<tr>
<td><p>;?err = &lt; 模式&gt;</p></td>
<td><p>此设置指示驱动程序在打印机响应中查找其他错误模式，以及默认的 "错误"。 例如 ";？err = open failed "将告知驱动程序在收到此类响应时失败 (在此示例中，如果内部 SD 卡存储未初始化或完全) ，则硬件将返回此响应。</p></td>
</tr>

<tr>
<td><p>;?wait = &lt; 模式&gt;</p></td>
<td><p>此设置指示驱动程序忽略模式，这通常用于保持活动信号，默认值为 ';？wait = wait。</p></td>
</tr>

</tbody>
</table>




