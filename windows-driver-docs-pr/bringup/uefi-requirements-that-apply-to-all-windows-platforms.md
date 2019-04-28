---
title: 在 SoC 平台上的 Windows 的 UEFI 要求
description: 本主题介绍适用于 Windows 10 桌面版 （主页、 专业版、 企业版和教育版） 和 Windows 10 移动版的 UEFI 要求。
ms.assetid: 7A0B901E-1252-4F8F-B1CB-BA1AB7B01112
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c32694d75dcdd948d93f0fda50674f7fdf3abc55
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337378"
---
# <a name="uefi-requirements-for-windows-editions-on-soc-platforms"></a>针对在 SoC 平台上的 Windows 版本的 UEFI 要求


本主题介绍适用于 Windows 10 桌面版 （主页、 专业版、 企业版和教育版） 和 Windows 10 移动版的 UEFI 要求。 仅适用于 Windows 10 移动版的其他要求，请参阅[Windows 10 移动版的 UEFI 要求](uefi-requirements-specific-to-windows-mobile.md)。

## <a name="summary-of-requirements"></a>要求摘要


下表列出了所有当前 UEFI 法规遵从性要求，UEFI 规范中定义 (部分 2.6 的 UEFI 2.3.1 规范)。 在此表中，术语*明确 Windows 要求*标识任何协议或直接由 Windows 组件调用的服务。 尽管 Windows 通过显式使用只有这些服务，但其他列出的服务和协议可能需要隐式或显式通过核心固件实现中，EFI 设备驱动程序或开发和部署工具链。

Microsoft 欢迎反馈，并注释来自实施者这组需求。 对于任何被确定为不需要的操作系统或固件的 UEFI 法规遵从性要求，是我们的意图来解决各个 UEFI.org 具有这些宽松的此类设备的符合性要求。

有关特定要求的更多详细信息，请在表格之后参阅部分。

| 要求                               | UEFI 规范部分 | 说明                          |
|-------------------------------------------|----------------------------|--------------------------------|
| **EFI 系统表**                      | 4.3                        | 明确 Windows 要求   |
| **EFI 启动服务**                     | 6.0                        |                                |
|   事件、 计时器和任务服务          | 6.1                        |                                |
|   内存服务                         | 6.2                        | 明确 Windows 要求\` |
|   协议处理程序服务               | 6.3                        | 明确 Windows 要求   |
|   图像服务                          | 6.4                        | 明确 Windows 要求   |
|   其他服务                  | 6.5                        | 明确 Windows 要求   |
| **EFI 运行时服务**                  | 7.0                        |                                |
|   时间服务                           | 7.3                        | 明确 Windows 要求   |
|   变量服务                       | 7.2                        | 明确 Windows 要求   |
|   其他服务                  | 7.5                        | 明确 Windows 要求   |
| **所需的 UEFI 协议**               |                            |                                |
|   EFI 加载图像协议               | 8.1                        |                                |
|   EFI 加载图像设备路径协议   | 8.2                        |                                |
|   EFI 设备路径协议                | 9.2                        | 明确 Windows 要求   |
|   EFI 设备路径实用程序协议      | 9.5                        |                                |
|   EFI 解压缩协议                 | 18.5                       |                                |
|   EBC 解释程序协议                | 20.11                      |                                |
| **有条件地要求的 UEFI 协议** |                            |                                |
|   EFI 简单的文本输入的协议          | 11.3                       | 明确 Windows 要求   |
|   EFI EX 协议的简单文本输入       | 11.2                       |                                |
|   EFI 简单的文本输出协议         | 11.4                       |                                |
|   EFI 图形输出协议            | 11.9                       | 明确 Windows 要求   |
|   EFI EDID 发现协议            | 11.9.1                     |                                |
|   EFI EDID active 协议                | 11.9.1                     |                                |
|   EFI 块 IO 协议                   | 12.8                       | 明确 Windows 要求   |
|   EFI 磁盘 IO 协议                    | 12.7                       |                                |
|   EFI 简单的文件系统协议         | 12.4                       |                                |
|   EFI Unicode 排序规则协议          | 12.10                      |                                |
|   EFI 简单网络协议             | 21.1                       |                                |
|   EFI PXE 基代码协议              | 21.3                       |                                |
|   EFI 启动完整性服务协议    | 21.5                       |                                |
|   EFI 串行 IO 协议                  | 11.8                       |                                |
|   UEFI ARM 绑定                        | 2.3.5                      | 明确 Windows 要求   |
| **安全要求**                 |                            |                                |
|   安全启动                             | 27.0                       | 明确 Windows 要求   |
|   启动管理器要求               | 3.1, 3.3                   | 明确 Windows 要求   |

 

## <a name="efi-system-table-requirements"></a>EFI 系统表的要求


EFI 系统表必须符合在级别实现的修订版本的标准定义。 指向 EFI 系统表的配置表必须包括以下两个 Guid 和其关联的指针下, 表中所述。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>GUID</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>EFI_ACPI_Table GUID</td>
<td><p>此 GUID 必须点到 ACPI 根系统说明指针 (RSDP) 平台。</p></td>
</tr>
<tr class="even">
<td>SMBIOS_Table GUID</td>
<td><p>此 GUID 必须指向 SMBIOS 入口点结构。</p>
<p>Windows 要求 SMBIOS 规范，在 2.4 或更高版本的修订级别。 需要部分 3.2 中，"所需结构和数据"和 4 中，"一致性指南"。 Windows SMBIOS 兼容性测试将会出现。</p></td>
</tr>
</tbody>
</table>

 

## <a name="efi-boot-services-requirements"></a>EFI 启动服务要求


下表列出了 Windows 的 EFI 启动服务要求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>EFI 启动服务</th>
<th>要求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>内存服务</td>
<td>Windows 需要的所有内存服务。</td>
</tr>
<tr class="even">
<td>协议处理程序服务</td>
<td><p>Windows 需要的以下协议处理程序服务：</p>
<ul>
<li><p>OpenProtocol()</p></li>
<li><p>CloseProtocol()</p></li>
<li><p>LocateDevicePath()</p></li>
<li><p>LocateHandle()</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>图像服务</td>
<td><p>Windows 需要以下映像服务：</p>
<ul>
<li><p>ExitBootServices()</p></li>
</ul></td>
</tr>
<tr class="even">
<td>其他引导服务</td>
<td><p>Windows 需要以下其他启动服务：</p>
<ul>
<li><p>Stall()</p></li>
</ul>
<div class="alert">
<strong>请注意</strong>  Stall() 实现需要具有确定性的 （可重复） 错误，以便可以可靠地完成错误纠正或取消。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

## <a name="efi-runtime-services-requirements"></a>EFI 运行时服务要求


下表列出了 Windows 的 EFI 运行时服务要求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>EFI 运行时服务</th>
<th>要求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>时间服务</td>
<td><p>Windows 需要以下时间服务：</p>
<ul>
<li><p>GetTime()</p></li>
<li><p>SetTime()</p>
<div class="alert">
<strong>请注意</strong>  时服务只会调用期间启动 （在之前访问平台时间一天的硬件 ExitBootServices())。
</div>
<div>
 
</div></li>
</ul></td>
</tr>
<tr class="even">
<td>变量服务</td>
<td><p>需要管理多个启动设备和系统的目标类上的安全变量的所有 UEFI 变量服务。</p></td>
</tr>
<tr class="odd">
<td>其他运行时服务</td>
<td><p>Windows 需要以下其他运行时服务：</p>
<ul>
<li><p>ResetSystem()</p>
<div class="alert">
<strong>请注意</strong>  ResetSystem() 实现必须支持重置和关闭选项。
</div>
<div>
 
</div></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="protocol-requirements"></a>协议要求


下表介绍了 UEFI 协议所需的 Windows 在启动过程中完成特定的函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>协议</th>
<th>要求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>图形输出协议</td>
<td><p>Windows 需要图形输出协议 (GOP)。 特定帧缓冲区要求如下：</p>
<ul>
<li><p>集成显示器<em>HorizontalResolution</em>并<em>VerticalResoluton</em>必须为面板自身分辨率。</p></li>
<li><p>对于外部显示器<em>HorizontalResolution</em>并<em>VerticalResoluton</em>必须是自身分辨率的显示器，或者如果不支持此功能，则这两个视频支持的最高值适配器，并已连接的显示。</p></li>
<li><p><em>PixelsPerScanLine</em>必须等于<em>HorizontalResolution</em>。</p></li>
<li><p><em>PixelFormat</em>必须是<em>PixelBlueGreenRedReserved8BitPerColor</em>。 请注意，物理帧缓冲区是必需的;<em>PixelBltOnly</em>不受支持。</p></li>
</ul>
<p>当执行移交给 UEFI boot 应用程序时，固件启动管理器和固件必须不使用帧缓冲区出于任何目的。 帧缓冲区必须继续扫描出之后启动服务都已退出。</p></td>
</tr>
<tr class="even">
<td>备用显示输出</td>
<td><p>UEFI 固件必须支持启动使用受硬件支持任何显示连接器。 如果内部面板已连接并且可见，则必须使用内部面板。 以物理方式连接显示的所有输出必须都显示启动屏幕。 连接显示为 UEFI 固件必须：</p>
<ul>
<li><p>如果不能确定自身分辨率，初始化与显示中，纯模式的输出。</p></li>
<li><p>如果纯模式不是可能的则它必须初始化为最高级别的兼容模式。</p></li>
<li><p>如果不能确定显示功能，必须在已知要尽可能 （通常采用 640x480 或 1024 x 768，60 hz） 与多监视器兼容模式下初始化连接的显示。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>在启动时输入</td>
<td><p>EFI 简单文本输入协议是必需的系统具有内置键盘或附加键盘的系统上进行启动选项或其他菜单选项。 对于无键盘的系统，在启动环境中建议三个按钮：</p>
<ul>
<li><p>“开始”按钮</p></li>
<li><p>调高音量按钮</p></li>
<li><p>调低音量按钮</p></li>
</ul>
<p>按钮按下应通过分别将它们映射到以下键盘键，报告通过 EFI 简单文本输入协议：</p>
<ul>
<li><p>Windows 键</p></li>
<li><p>向上键</p></li>
<li><p>向下箭头键</p></li>
</ul></td>
</tr>
<tr class="even">
<td>本地存储启动</td>
<td><p>Windows 要求块 I/O 协议和设备路径协议支持包含 EFI 系统分区和 Windows OS 分区的存储解决方案。 用于启动从需要调节穿戴设备或其他闪存管理的闪存存储，这必须 （而不是在 UEFI 应用程序） 固件中实现。</p></td>
</tr>
</tbody>
</table>

 

## <a name="security-requirements"></a>安全要求


Windows 在安全引导、 标准引导、 加密和数据保护方面具有的安全要求。 下表中详细介绍了这些要求。 此外，在哪些 SoC 中硬件会阻止与现有的标准 （TPM、 RTC 等） 的符合性的那些方面，其他要求是正在开发的。 描述了这些内容在表的末尾。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>区域</th>
<th>要求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>常规</td>
<td><ul>
<li><p>要求 1:必需。 本部分中指定的所有要求，应符合平台。</p></li>
<li><p>要求 2:必需。 平台应是 UEFI 类三个与已安装或可安装不兼容性支持模块。 BIOS 仿真以及旧 PC / 必须禁用在启动过程。</p></li>
</ul></td>
</tr>
<tr class="even">
<td>UEFI 安全启动</td>
<td><ul>
<li><p>要求 3:必需。 作为适用于版本 v2.3.1 部分 27 中定义 UEFI 安全启动必须已启用且与签名数据库 (EFI_IMAGE_SECURITY_DATABASE) 需要安全地启动机预配。 签名数据库的初始内容由 OEM，根据所需的第三方 UEFI 驱动程序、 恢复需求和 OS 引导加载程序安装的计算机上，但应包含由 Microsoft 提供 EFI_CERT_X509 签名。 不应存在任何附加的签名。</p></li>
<li><p>要求 4:必需。 UEFI"禁止访问"签名数据库 (EFI_IMAGE_SECURITY_DATABASE1) 的存在是必需的。</p></li>
<li><p>要求 5:必需。 Microsoft 提供的 UEFI KEK 应包括在 UEFI KEK 数据库。 没有其他的 Kek，应显示。 Microsoft 将提供的 KEK EFI_CERT_X509 签名的窗体中。</p></li>
<li><p>要求 6:必需。 一个 PK<em><sub>pub</sub></em> 密钥应存在并存储在闪存的固件。</p>
<div class="alert">
<strong>请注意</strong>  因为 PK<em><sub>priv</sub> </em> (PK 的私钥对应<em><sub>pub</sub></em>) 控制安全启动使用 PK 预配的所有设备上的策略<em><sub>pub</sub></em>，它的保护和使用必须受到严密保护。
</div>
<div>
 
</div></li>
<li><p>要求 7:必需。 初始签名数据库应存储在闪存的固件，可能仅与 OEM 签名固件更新或通过 UEFI 已经过身份验证变量写入更新。</p></li>
<li><p>要求 8:必需。 不会执行签名验证失败的启动路径中的映像，并且失败的原因应添加到 EFI_IMAGE_EXECUTION_TABLE。 此外，在这些情况下建议的方法是 UEFI 启动管理器启动恢复根据特定于 OEM 的策略。</p></li>
<li><p>要求 9:必需。 未通过签名验证的 UEFI 映像必须不允许实际存在的用户重写。</p></li>
<li><p>要求 10:可选。 OEM 可能会实施实际存在的用户可以关闭安全启动使用访问 PK<em><sub>priv</sub></em> 或现场通过固件安装程序。 通过平台特定方法 （管理员密码、 智能卡、 静态配置等） 中对固件安装程序的访问可能会受到保护</p></li>
<li><p>要求 11:如果实现要求 10，强制参数。 如果关闭安全引导然后所有现有的 UEFI 变量应不能访问。</p></li>
<li><p>要求 12:可选。 OEM 可能会实现实际存在的用户在固件安装程序中的两种安全启动模式之间进行选择的功能："自定义"和"标准"。 自定义模式允许以下指定更大的灵活性。</p></li>
<li><p>要求 13:如果实现要求 12，强制参数。 它应能特定设置所有者来重新启用自定义模式已禁用安全启动<em>PK</em>。 管理应继续执行，部分 27.5 的 UEFI 规范适用于版本 v2.3.1 中定义：固件/OS 密钥交换。 在自定义模式下，设备所有者可能签名数据库中设置她所选择的签名。</p></li>
<li><p>要求 14:如果实现要求 12，强制参数。 如果启用安全启动和运行在标准或自定义模式下，应指示固件安装程序。 固件安装程序应提供要从自定义返回到标准模式的选项。</p></li>
<li><p>要求 15:必需。 如果固件设置重置为出厂默认设置，应清除受保护的所有自定义组变量和原始 PK<em><sub>pub</sub></em> 应重新建立与原始，一起制造商设置签名的数据库。</p></li>
<li><p>要求 16:必需。 驱动程序签名应使用验证码选项 (WIN_CERT_TYPE_PKCS_SIGNED_DATA)。</p></li>
<li><p>要求 17:必需。 对 EFI_IMAGE_EXECUTION_INFO_TABLE （即创建和存储有关启动或未在启动期间启动映像的信息） 的支持。</p></li>
<li><p>要求 18:必需。 EFI_IMAGE_SECURITY_DATABASE （授权和禁止签名数据库） 的支持 GetVariable()。</p></li>
<li><p>要求 19:必需。 支持 SetVariable() EFI_IMAGE_SECURITY_DATABASE （授权和禁止签名数据库），用于使用 Microsoft KEK 进行身份验证。</p></li>
<li><p>要求 20:必需。 EFI_HASH_SERVICE_BINDING_PROTOCOL:服务支持：CreateChild()，DestroyChild()。</p></li>
<li><p>要求 21:必需。 EFI_HASH_PROTOCOL。 服务支持：Hash()。 对 SHA_1 和 SHA-256 哈希算法的支持。 必须支持传递长消息至少 10 兆字节数。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>UEFI 标准的引导</td>
<td><p>以下要求并不意味着需要的 TCG TPM 实现;它们但是指示受影响区域的等效功能的需求。</p>
<p>可能由 TPM 安全执行环境中执行、 加密加速引擎的基础上分层和利用独立的存储的固件实现提供的平台支持。 Microsoft 可能能够提供参考软件供应商使用此类的 TPM 实现。 这将受到进一步的讨论。</p>
<ul>
<li><p>要求 22:必需。 在平台中指定的 EFI 协议应符合<a href="https://go.microsoft.com/fwlink/p/?LinkId=528536" data-raw-source="[UEFI Trusted Execution Environment EFI Protocol](https://go.microsoft.com/fwlink/p/?LinkId=528536)">UEFI 的受信任执行环境 EFI 协议</a>。</p></li>
<li><p>要求 23:必需。 平台应遵循作为 TCG EFI 平台规范的开头添加以下内容：</p>
<ul>
<li><p>在支持树 EFI 协议，PK 的摘要中定义的接口的平台上<em><sub>pub</sub></em> 应扩展到 TPM PCR [03] 为 EV_EFI_VARIABLE_CONFIG 事件。</p></li>
<li><p>为 EV_EFI_VARIABLE_CONFIG 事件，必须在标准引导扩展授权的签名数据库 （请参见 27.8 一部分 UEFI 规范适用于版本 v2.3.1） 列表的内容的摘要。 延伸操作应是到 TPM PCR [03]。</p></li>
<li><p>它应是 UEFI 客户端读取和分析所列出的证书使用 EFI_IMAGE_SECURITY_DATABASE 变量和验证的扩展值对的摘要。</p></li>
<li><p>TCG_PCR_EVENT 摘要值应为 SHA-256，而不是 SHA-1。</p></li>
</ul></li>
<li><p>要求 24:必需。 在平台必须实现中定义 MemoryOverwriteRequestControl <a href="https://go.microsoft.com/fwlink/p/?LinkId=528539" data-raw-source="[TCG Platform Reset Attack Mitigation Specification](https://go.microsoft.com/fwlink/p/?LinkId=528539)">TCG 平台重置攻击缓解规范</a>。</p></li>
</ul></td>
</tr>
<tr class="even">
<td>加密</td>
<td><ul>
<li><p>要求 25:必需。 平台应提供 EFI_HASH_PROTOCOL (UEFI 适用于版本 v2.3.1 部分 27.4) 以进行卸载的加密哈希操作。 必须支持 SHA-256。</p></li>
<li><p>要求 26:必需。 平台应支持的 Microsoft 定义<a href="uefi-entropy-gathering-protocol.md" data-raw-source="[EFI_RNG_PROTOCOL](uefi-entropy-gathering-protocol.md)">EFI_RNG_PROTOCOL</a>为预操作系统读取的平均信息量。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>数据保护</td>
<td><ul>
<li><p>要求 27:必需。 在平台必须支持具有以下 UEFI 变量的属性集的任意组合的 EFI 变量：</p>
<ul>
<li><p>EFI_VARIABLE_BOOTSERVICE_ACCESS</p></li>
<li><p>EFI_VARIABLE_NON_VOLATILE</p></li>
<li><p>EFI_VARIABLE_AUTHENTICATED_WRITE_ACCESS</p></li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<td>其他安全要求</td>
<td><p>以下附加要求所需 Windows SoC 平台上。</p>
<ul>
<li><p>Microsoft 还定义了协议，用于收集 UEFI 平台平均信息量。 在 SoC 平台上情况下，而不是 UEFI 要求使用 Windows 需要此协议。 有关此协议的详细信息，请参阅<a href="uefi-entropy-gathering-protocol.md" data-raw-source="[UEFI entropy gathering protocol](uefi-entropy-gathering-protocol.md)">UEFI 平均信息量收集协议</a>。</p></li>
<li><p>UEFI 签名数据库更新。 已在配有 UEFI 2.3.1 部分 27 中采用新的更新变量进行身份验证机制。 此机制是所需的 Windows。</p></li>
<li><p>受信任的执行环境。 Microsoft 开发了一种 EFI 协议与受信任执行环境 （树） 中，在功能上类似于一个子集的受信任计算组 (TCG) 受信任的平台模块 (TPM) 进行交互。 EFI 协议利用在很大程度，1.2 版修订 1.00，2006 年 6 月 9 日，由受信任计算组"TCG EFI 协议"。</p>
<p>有关详细信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?LinkId=528536" data-raw-source="[UEFI Trusted Execution Environment EFI Protocol](https://go.microsoft.com/fwlink/p/?LinkId=528536)">UEFI 的受信任执行环境 EFI 协议</a>。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="firmware-boot-manager-requirements"></a>固件启动管理器要求


固件启动管理器必须支持规范的 3.3 节中定义的默认启动行为。 此外，对于多引导的支持下，全局定义的变量和规范的第 3.1 节的启动管理器要求操作则需要。

## <a name="uefi-arm-binding-requirements"></a>UEFI ARM 绑定要求


UEFI ARM 绑定包含特定于要符合 UEFI 规范所需的 ARM 平台的要求。 Windows 要求适用于 ARMv7 ARM 绑定中的所有内容。 因为 Windows 不支持上一步 ARMv7 的任何内容，在绑定中特定于 ARMv6k 和更的要求是可选的。

绑定指定应映射 MMU 应如何配置和如何物理内存的示例。 绑定还指定调用对 UEFI 协议和服务应在仅 ARM ISA，这意味着 Thumb2 或 thumb 控件中运行的软件需要调用 UEFI 函数之前切换到 ARM 模式。

## <a name="uefi-arm-multiprocessor-startup-requirements"></a>UEFI ARM 多处理器启动要求


Microsoft 开发了一种用于在多处理器 UEFI 平台上启动多个 ARM 核心协议。 此协议所需的 Windows 不支持 ARM 平台上[电源状态协调接口 (PSCI)](https://go.microsoft.com/fwlink/p/?LinkId=528534)。 PSCI 支持的平台不得使用此协议。 有关此协议的详细信息，请参阅[在基于 UEFI ARM 平台上的多处理器启动](https://go.microsoft.com/fwlink/p/?LinkId=528533)ACPI 组件体系结构 (ACPICA) 网站上的文档。

## <a name="platform-setup-requirements"></a>平台安装程序要求


固件负责使系统硬件的定义完善状态之前处理关闭操作系统加载程序。 下表定义相关的平台安装程序的要求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>要求</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>启动路径</td>
<td>固件必须初始化 Windows 能够访问通过 UEFI 启动设备并加载内核的点到平台。 要从启动设备读取的层次结构中所涉及的任何设备必须上班，并且提供支持以合理的速率，提供性能和功能的注意事项。 基处理器核心本身还应上班并且，以便系统可以及时地启动而无需消耗电池提供支持以合理的速率。</td>
</tr>
<tr class="even">
<td>核心系统资源</td>
<td><p>核心系统公开的资源的 ACPI 表通过操作系统必须打开并上班。 核心系统资源包括中断控制器，计时器和 DMA 控制器必须由操作系统管理。</p>
<p>此外，中断必须通过调用 ExitBootServices() 屏蔽之前在 OS 中的关联的设备驱动程序解除屏蔽和重新启用该设备上的中断。 如果在启动服务期间启用了中断，假定固件将管理它们。</p></td>
</tr>
<tr class="odd">
<td>调试</td>
<td>Windows 支持调试通过 USB 3 主机 (XHCI)、 USB 2 主机 (EHCI) 1、 串行的 IEEE 1394 和 USB 函数接口 （以及 PCI 以太网适配器）。 这些在至少一个必须为提供支持、 上班，由在 OS 提交固件初始化。 无论选项提供，它必须具有出于调试目的，公开的端口，控制器必须为内存映射，或通过专用 （非共享） 外围总线连接。</td>
</tr>
<tr class="even">
<td>其他平台安装程序要求</td>
<td>必须在任何 pin 多路复用和板配置完成之前将控制传递给操作系统加载程序在固件中。</td>
</tr>
</tbody>
</table>

 

## <a name="installation-requirements"></a>安装要求


Windows 需要 OS 分区，使其位于 GPT 分区的存储解决方案。 MBR 分区存储可用作数据存储。 UEFI 规范中定义，UEFI 平台所需的专用的系统分区。 Windows 需要此专用系统分区，称为 EFI 系统分区 (ESP)。

## <a name="hardware-security-test-interface-hsti-requirement"></a>硬件安全测试接口 (HSTI) 要求


在平台必须实现硬件安全测试接口，并共享文档和工具中指定所需的平台[硬件安全可测试性规范](https://docs.microsoft.com/windows-hardware/test/hlk/testref/hardware-security-testability-specification)。

## <a name="related-topics"></a>相关主题

[最小的 Windows 在 SoC 平台上的 UEFI 要求](minimum-uefi-requirements-for-windows-on-soc-platforms.md)  

[Windows 10 移动版的 UEFI 要求](uefi-requirements-specific-to-windows-mobile.md)  

[USB 闪烁的支持的 UEFI 要求](uefi-requirements-for-usb-flashing-support.md)  



