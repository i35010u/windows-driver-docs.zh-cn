---
title: 切片器设置
description: 配置文件 XML 包含大量需要特定 3D 打印机设备来控制打印功能公开给 Windows 中的 3D 打印对话框进行调整的设置。
ms.assetid: 9203AABB-48D9-47A6-A2B1-7A878BF82FD1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53fba2c8daaad75fe8bd354aae08588a91d39e8f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324703"
---
# <a name="slicer-settings"></a>切片器设置


配置文件 XML 包含大量需要特定 3D 打印机设备来控制打印功能公开给 Windows 中的 3D 打印对话框进行调整的设置。 这些设置还控制 Microsoft 3D 切片器 （MS3DPrinterRenderFilter.DLL 和依赖项） 正在运行参数。  

## <a name="slicer-settings"></a>切片器设置


<table>

<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>

<thead>
<tr class="header">
<th>设置 (XML Path)</th>
<th>“更改”</th>
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
<td><p>打印微米，定义的宽度 (最大 x)、 深度 (y 最大值) 和高度 (z 最大值) 中的卷。</p>
<p>卷应表示为一个发布该驱动程序时确保打印机可以使用声明的批量的认证阶段中的测试的物理设备的功能。</p></td>
</tr>


<tr>
<td><p>psk3d:Job3DOutputArea\ </p>
<p>psk3d:Job3DOutputAreaOffsetX</p>
<p>psk3d:Job3DOutputArea\ </p>
<p>psk3d:Job3DOutputAreaOffsetX</p></td>
<td><p>可选</p></td>
<td><p>相对于打印的量的 X 和 Y 偏移量 （0，0）。 这样 3D 打印机支持其中 （0，0） 是在平台上 （一般用于增量打印机） 或打印机的中心位置 （0，0） 不在前端的左上角的打印平台。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3ds:extruders\  </p></td>
<td><p>可选</p></td>
<td><p>在打印机中 extruders 数。 此设置控制多少个后续 psk3d:Material&lt;Mat&gt; XML 中的各节将发送到打印对话框中即打印功能。 如果未指定，则驱动程序将假定单一 extruder 打印机。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3d:Material&lt;Material&gt;\ </p>
<p>psk:DisplayName</p></td>
<td><p>是</p></td>
<td><p>材料的显示名称。 这可以是任何用户分配的 3D 打印对话框中显示的字符串。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3d:Material&lt;Material&gt;\ </p>
<p>psk:MaterialColor</p></td>
<td><p>是</p></td>
<td><p>3D 打印对话框中的材料呈现的 RGB 或 RGBA 颜色。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3d:Material&lt;Material&gt;\ </p>
<p>psk:MaterialType</p></td>
<td><p>保留</p></td>
<td><p>材料，打印架构关键字用于 3D 打印 (例如，"psk3d:PLA") 中定义的类型。 支持指定的名称和颜色的泛型材料已弃用此设置。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3d:Material&lt;Material&gt;\ </p>
<p>psk3dx:platformtemperature</p></td>
<td><p>是</p></td>
<td><p>打印平台应在打印期间激烈到温度 （摄氏度）。 值为 0 表示平台应不激烈。</p>
<p>此值可以通过更高版本引用<em>$platformtemperature$</em>预命令中的模板。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3d:Material&lt;Material&gt;\ </p>
<p>psk3dx:filamentdiameter</p></td>
<td><p>是</p></td>
<td><p>在 3D 打印机中加载中 filament 微米直径。 例如，1750年是标准 1.75 mm filament。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3d:Material&lt;Material&gt;\ </p>
<p>psk3dx:filamentcalibrationoverride</p></td>
<td><p>可选</p></td>
<td><p>调整 filament 流因子。 为传入 filament 交叉部分 （基于 filamentdiameter） 来调整的延伸速度的比率值应用该策略。 如果这一因素大于 1.0，则将延伸较少塑料。 这是一个优化的参数，应始终为 1.0 附近。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3d:Material&lt;Material&gt;\ </p>
<p>psk3dx:extrudertemperature</p></td>
<td><p>是</p></td>
<td><p>温度以摄氏度热 extruder/最终应为热，当拉伸。 此值可以通过引用<em>$extrudertemperature$</em>预命令中的模板。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\ </p>
<p>psk3d:Material&lt;Material&gt;\ </p>
<p>psk3dx:autocenter</p></td>
<td><p>可选</p></td>
<td><p>一个布尔值 （0 或 1），该值指示模型是否应该居中 （在 XY 平面） 打印的平台上。 模型还自动-居中如果不适合打印的卷中。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\  </p>
<p>psk3d:Material&lt;Material&gt;\  </p>
<p>psk3dx:SetupCommands\ </p>
<p>psk3dx:command</p></td>
<td><p>是</p></td>
<td><p>要用作材料设置的命令的列表。 这是通常 G 代码执行过程前命令，以控制 nozzle 预加热，填充，依次类推。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\  </p>
<p>psk3d:Material&lt;Material&gt;\  </p>
<p>psk3dx:SelectCommands\ </p>
<p>psk3dx:command</p></td>
<td><p>是</p></td>
<td><p>命令发出时材料需要在打印时使用的列表。 这是通常 G 代码执行：T0/T1 extruder 选择，nozzle 擦除序列中，打开风扇上/关闭/逐步、 收回材料、 温度和等等。</p></td>
</tr>

<tr>
<td><p>psk3d:Job3DMaterials\  </p>
<p>psk3d:Material&lt;Material&gt;\  </p>
<p>psk3dx:DeselectCommands\ </p>
<p>psk3dx:command</p></td>
<td><p>是</p></td>
<td><p>要在打印期间释放材料时发出的命令列表。 这是通常 G 代码执行： 收回材料，停好 nozzle、 减少温度，等等。</p></td>
</tr>

<tr>
<td><p>psk3dx:customStatus</p></td>
<td><p>可选</p></td>
<td><p>表示初始打印作业状态，通常在切片阶段的字符串。 如果缺失，作业状态将设置为"打印"。 通常此值应设置为"Slicing"时进行切片发生在呈现器的筛选器，例如，使用 Microsoft 切片器时。</p></td>
</tr>

<tr>
<td><p>psk3dx:userprompt</p></td>
<td><p>是</p></td>
<td><p>打印开始之前显示用户提示一条消息。 此提示用于防止 extruder 撞到现有设备需要手动删除打印首页上打印。</p>
<p>对于可以显示提示的开头或末尾打印设备本身的设备，此设置不是必需的。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:debug\ </p>
<p>psk3dx:log</p></td>
<td><p>可选</p></td>
<td><p>当存在时，此设置将启用驱动程序调试日志记录到文件中，允许开发人员检查 G 代码，并使用固件响应。</p>
<p>此设置可以还启用全局通过注册表项 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Print</p>
<p>StandardGCodeDebugLog="c:\Path\To\LogFile"</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:communication\ </p>
<p>psk3dx:connection\ </p>
<p>psk3dx:comport</p></td>
<td><p>可选</p></td>
<td><p>为串行端口名称的 URI。 当存在时，此设置将替代驱动程序自动解决问题所用的 COM 端口 (打印机队列-&gt;打印机端口名称-&gt; Enum\3DPrinter\Device-&gt; Enum\USB\Serial 设备)。 这样，暂时打印到的设备，但没有最终硬件 Id。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:communication\ </p>
<p>psk3dx:connection\ </p>
<p>psk3dx:baudrate</p></td>
<td><p>可选</p></td>
<td><p>已连接的设备的串行连接的波特率。 典型值为 115200 或 250000。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:communication\ </p>
<p>psk3dx:connection\ </p>
<p>psk3dx:mode</p></td>
<td><p>保留</p></td>
<td><p>此设置控制重置连接时的行为 （DTR 设置）。 如果设备无法连接，请使用值 1 或 3。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:communication\  </p>
<p>psk3dx:connection\ </p>
<p>psk3dx:protocol</p></td>
<td><p>保留</p></td>
<td><p>此设置是高度实验性并控制使用固件的通信协议。 如果未指定，该驱动程序默认与 ASCII G 代码 RepRap/Marlin 校验和。 如果设置为 2，则可以将驱动程序发送二进制 G 代码。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:communication\ </p>
<p>psk3dx:connection\ </p>
<p>psk3dx:timeout</p></td>
<td><p>保留</p></td>
<td><p>以毫秒为单位的打印机响应超时。 使用无超时值为 0 （默认值）。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:customcommands\ </p>
<p>psk3dx:initcommands\ </p>
<p>psk3dx:command</p></td>
<td><p>是</p></td>
<td><p>切片之前发送的命令序列。 与切片器同时执行这些命令。 这通常是一系列的主页，校准、 自动级别和/或温度的打印机接近最终温度的上升 G 代码命令。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:customcommands\ </p>
<p>psk3dx:precommands\ </p>
<p>psk3dx:command</p></td>
<td><p>是</p></td>
<td><p>要发送的每个作业开始时通常用于初始化 3D 打印机，例如寻址以及注册到最后一个温度 extruder 加热和填充 extruder G 代码命令集。 每个设备都有不同所需的预命令。 每个 G 代码行应出现在子&lt;命令&gt;元素。 可以将引用的设置要替换的变量声明为 $ 字符分隔的名称&lt;命令&gt;M104 <em>S$ extrudertemperature$</em>&lt;/command&gt;. 请参阅下一部分，内置变量。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:customcommands\ </p>
<p>psk3dx:postcommands\ </p>
<p>psk3dx:command</p></td>
<td><p>是</p></td>
<td><p>组 G 代码命令发送的每个作业结束时通常以使 3D 打印机保持安全状态，如散热下 extruder 和将离开热 extruder/部分移到其中很容易地从平台删除结束。 每个设备都有不同所需的后命令。</p>
<p>取消作业时，也会执行此序列。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:customcommands\ </p>
<p>psk3dx:failsafepostcommands\ </p>
<p>psk3dx:command</p></td>
<td><p>可选</p></td>
<td><p>G 代码命令为切片器出错时失败安全机制，例如，发送一组。 如果缺少，该驱动程序将执行"M104 S0"后跟"M110 N0"。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:layerthickness</p></td>
<td><p>是</p></td>
<td><p>微米中的层的粗细 （z 高度）。 此值应根据计算机物理分辨率，以尽量减少定位错误定义。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:maxlayerthickness</p></td>
<td><p>保留</p></td>
<td><p>最大层中微米的粗细。</p>
<p>此设置保留，并且可能在将来已弃用。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:minlayerthickness</p></td>
<td><p>保留</p></td>
<td><p>最小层中微米的粗细。</p>
<p>此设置保留，并且可能在将来已弃用。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:pathwidth</p></td>
<td><p>是</p></td>
<td><p>在微米拉伸 toolpath 宽度 （以 XY 平面中）。 关闭并会稍微更大的值比 nozzle 直径往往会产生最佳结果。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:shells</p></td>
<td><p>可选</p></td>
<td><p>嵌入 shell infill 开始前的整数。 如果值为 1 使只有一个单一周边环境并且值为 0 仅 infill （很粗糙表面光洁度）。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:shelloffset</p></td>
<td><p>可选</p></td>
<td><p>在微米外部 shell 的偏移量。 使用此值来优化上部分 （例如，齿轮） 之间具有非常牢牢固定的模型的结果。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:topsurfacelayers</p></td>
<td><p>可选</p></td>
<td><p>层以固定填充打印的上部曲面上的整数。 值为 0 将使稀疏 infill 从上可见。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:bottomsurfacelayers</p></td>
<td><p>可选</p></td>
<td><p>层来填充固定在较低的打印面上的整数。 值为 0 将使稀疏 infill 从下可见。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:fill</p></td>
<td><p>保留</p></td>
<td><p>指定稀疏 infill 分数，介于 0.0 和 1.0 （含) 之间。 0.1 （10%)是很好的默认值。 值为 0.0 会导致打印 shell 并且值为 1.0 而不是稀疏 infill 将 solid infill 模式。</p>
<p>此设置保留，并且可能在将来已弃用。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:fillangle</p></td>
<td><p>可选</p></td>
<td><p>沿 XY （水平） 平面，从 x 轴逆时针旋转度为单位度量的填充模式中，初始角。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:filloverlap</p></td>
<td><p>保留</p></td>
<td><p>Infill （0 和 1 的路径宽度，非独占） 之间的重叠。</p>
<p>此设置保留，并且可能在将来已弃用。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:speed</p></td>
<td><p>是</p></td>
<td><p>默认的微米/第二个中的打印移动，速度。 这是 X 和 Y 轴速度 2-范数。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:speedouter</p></td>
<td><p>是</p></td>
<td><p>外部外围的速度 （首先外壳） 中微米/秒。 这可以设置低于正常的速度，以创建更好的表面光洁度上打印。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:speedfirst</p></td>
<td><p>是</p></td>
<td><p>第一层的速度 (取代<strong>speedouter</strong>) 中微米/秒。 这可以设置低于正常的速度，以获得更好地打印平台 adhesion。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:speedtravel</p></td>
<td><p>是</p></td>
<td><p>中的非延伸的速度移动，微米/秒。 这可以设置高于正常的速度，以尽量减少顺序排列并加快打印时 extruder 是限制因素。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:speedretract</p></td>
<td><p>是</p></td>
<td><p>Filament 收回和微米中推送回的速度/秒。 其他速度与设置不同，这为单位输入 filament，而不是 X 和 Y 轴上。 此速度因此是与上面的速度 （取决于你 filament) 小于 20 为系数。 但是，它可能会高于等效的速度，因为不强制塑料收回过程延伸。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:retraction</p></td>
<td><p>是</p></td>
<td><p>再次输入 filament，微米中计量 filament 要缩进; 的长度。 这是用于收回和将推送回对称，旨在降低顺序排列和旅行时 nozzle 的流动。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:supportorientationoptimization</p></td>
<td><p>保留</p></td>
<td><p>（0 或 1） 一个布尔值，该值指示是否自动重定向模型来或不需要的支持，最大程度减少。</p>
<p>此设置保留，并且可能在将来已弃用。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:supportoverhangangle</p></td>
<td><p>可选</p></td>
<td><p>最大值延伸需要支持，从水平面最多模型方面，以度为单位测量的角度。 较小角度创建更少的支持结构。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:supportzgap</p></td>
<td><p>是</p></td>
<td><p>Z 间隔以与微米之间的部分和支持。 此设置可以减少 adhesion 若要支持，轻松地删除支持。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:supportxygap</p></td>
<td><p>是</p></td>
<td><p>中支持和部件中的 XY 平面之间的微米间隙。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:supportfill</p></td>
<td><p>可选</p></td>
<td><p>稀疏 infill 小数 （0 和 1 之间，非独占） 的支持。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:raftlayers</p></td>
<td><p>可选</p></td>
<td><p>Solid 筏层数。 数值 2 通常已足够。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:raftlayerthickness</p></td>
<td><p>是</p></td>
<td><p>层中微米筏的粗细 （Z 高度）。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:raftpathwidth</p></td>
<td><p>是</p></td>
<td><p>在微米筏路径宽度。 这通常是更大的值以容纳打印平台图面中的变体。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:raftfill</p></td>
<td><p>可选</p></td>
<td><p>稀疏 infill 小数 （0 和 1 之间，非独占） 的支持。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:raftoffset</p></td>
<td><p>可选</p></td>
<td><p>在微米筏的大小。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:raftzgap</p></td>
<td><p>是</p></td>
<td><p>间隙微米筏和对象之间的 Z。 较高的值使筏更轻松地删除，但可能会产生一个不均匀的图面。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:raftspeedfirst</p></td>
<td><p>是</p></td>
<td><p>速度筏首先层中微米/秒。 这应该是类似或到更低<strong>speedfirst</strong>以提高平台 adhesion。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:coolingtime</p></td>
<td><p>可选</p></td>
<td><p>冷却时间 （秒） 层的最小值。 层速度会降低，以便在它打印在超过此秒数。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:mincoolingspeed</p></td>
<td><p>可选</p></td>
<td><p>冷却微米/秒的速度层中的最小值。</p></td>
</tr>

<tr>
<td><p>psk3dx:MS3DPrinter\ </p>
<p>psk3dx:print\ </p>
<p>psk3dx: {质量} \ </p>
<p>psk3dx:bridgingspeed</p></td>
<td><p>是</p></td>
<td><p>延伸期间微米中的桥接的速度。 此值取决于计算机冷却特征和 filament 类型等因素，通常要比普通打印速度慢。</p></td>
</tr>

</tbody>
</table>


**请注意**打印节点的设置中 (psk3dx:MS3DPrinter\\psk3dx:print\\psk3dx: {质量}\)，{质量} 元素名称替换为相应 psk3d:Quality 打印架构 3D 关键字之一在打印作业以及 PrintTicket 中发送的设置。 这样，每个质量级别来定义其自己的切片器设置集。 如果省略 PrintTicket，则将使用切片器\[质量\]设置标记属性默认值 ="true"，因此恰好一个质量级别始终应定义此属性。

<table>

<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>

<thead>
<tr class="header">
<th>设置名称</th>
<th>描述</th>
</tr>
</thead>
<tbody>

<tr>
<td><p>$extrudertemperature$</p>
<p>$extruder2temperature$</p></td>
<td><p>第一个和第二个 extruder，由指定分别温度&lt;psk3dx:extrudertemperature&gt; XML 中的资料部分中。 这些变量已被弃用，替换为 $MaterialSetup$。</p></td>
</tr>

<tr>
<td><p>$platformtemperature$</p></td>
<td><p>指定的激烈的平台上的温度&lt;psk3dx:platformtemperature&gt;列表中的最后一个材料中的条目。</p></td>
</tr>

<tr>
<td><p>$MaterialSetup<n>$</p></td>
<td><p>材料设置部分&lt;psk3dx:SetupCommands&gt;资料中。 例如 $MaterialSetup3$ 表示在列表中，通常第三 extruder 的第三材料。</p></td>
</tr>

<tr>
<td><p>$rampup $</p></td>
<td><p>这是一个变量可以是 0..255 和 Z 轴会随着和控制的&lt;psk3dx:rampuptarget&gt;中切片器质量设置。</p>
<p>例如命令"M106 S rampup$"开启风扇逐渐 Z 轴增加时。 如果&lt;psk3dx:rampuptarget&gt;设置为 500 微米，变量的值是第一层上的 0 和 255 之间后的层是 500 微米或更高。</p>
<p>此变量用于更好地打印 adhesion 上引起热烈打印 beds 的支持，但可在任何命令。</p></td>
</tr>

<tr>
<td><p>;?ack=&lt;pattern&gt;</p></td>
<td><p>此设置会指示驱动程序，若要更改命令确认模式 （打印机响应） 从默认的确定为临时的例如";？ack = 写入到文件"将告知驱动程序要等待的打印机已准备好写入到的内部存储一条确认消息。</p></td>
</tr>

<tr>
<td><p>;?err=&lt;pattern&gt;</p></td>
<td><p>此设置会指示要查找有关在打印机响应中，除了默认 error 模式的其他错误的驱动程序。 例如";？err = 打开失败"将告知驱动程序失败 （在本例中的硬件会返回此响应，如果未初始化内部的 SD 卡存储或完全） 是否收到此类响应。</p></td>
</tr>

<tr>
<td><p>;?wait=&lt;pattern&gt;</p></td>
<td><p>此设置会指示驱动程序忽略模式，这通常用于保持活动状态的信号，并且默认值是;？等待 = 等待。</p></td>
</tr>

</tbody>
</table>




