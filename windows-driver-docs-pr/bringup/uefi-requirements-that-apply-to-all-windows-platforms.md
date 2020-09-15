---
title: SoC 平台上 Windows 的 UEFI 要求
description: 本主题介绍适用于适用于 Windows 10 的 UEFI 要求 (家庭、专业版、企业版和教育版) 以及 Windows 10 移动版。
ms.assetid: 7A0B901E-1252-4F8F-B1CB-BA1AB7B01112
ms.date: 08/25/2020
ms.localizationpriority: medium
ms.openlocfilehash: 10986dff002311176afcbe66c6c2135be8a929b3
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101518"
---
# <a name="uefi-requirements-for-windows-editions-on-soc-platforms"></a>SoC 平台上 Windows 版本的 UEFI 要求

本主题介绍适用于适用于 Windows 10 的 UEFI 要求 (家庭、专业版、企业版和教育版) 以及 Windows 10 移动版。 有关仅适用于 Windows 10 移动版的其他要求，请参阅 [Windows 10 移动版的 UEFI 要求](uefi-requirements-specific-to-windows-mobile.md)。

## <a name="summary-of-requirements"></a>要求摘要

下表列出了 uefi 规范 (第2.6 节中定义的 uefi 的所有当前要求（在 UEFI 2.3.1 规范) 中定义）。 在此表中，术语 " *显式 Windows 要求* " 标识 windows 组件直接调用的任何协议或服务。 虽然 Windows 只显式使用这些服务，但核心固件实现、EFI 设备驱动程序或开发和部署工具链可能会隐式或显式地要求使用其他列出的服务和协议。

Microsoft 欢迎您对此组要求的实施人员提供反馈和意见。 对于确定不由操作系统或固件要求的 UEFI 符合性要求，我们打算通过 UEFI.org 来处理此类设备的这些符合性要求。

有关特定要求的详细信息，请参阅表后面的部分。

| 要求                               | UEFI 规范部分 | 备注                          |
|-------------------------------------------|----------------------------|--------------------------------|
| **EFI 系统表**                      | 4.3                        | 显式 Windows 要求   |
| **EFI 启动服务**                     | 6.0                        |                                |
|   事件、计时器和任务服务          | 6.1                        |                                |
|   内存服务                         | 6.2                        | 显式 Windows 要求\` |
|   协议处理程序服务               | 6.3                        | 显式 Windows 要求   |
|   映像服务                          | 6.4                        | 显式 Windows 要求   |
|   其他服务                  | 6.5                        | 显式 Windows 要求   |
| **EFI 运行时服务**                  | 7.0                        |                                |
|   时间服务                           | 7.3                        | 显式 Windows 要求   |
|   变量服务                       | 7.2                        | 显式 Windows 要求   |
|   其他服务                  | 7.5                        | 显式 Windows 要求   |
| **必需的 UEFI 协议**               |                            |                                |
|   EFI 已加载映像协议               | 8.1                        |                                |
|   EFI 已加载映像设备路径协议   | 8.2                        |                                |
|   EFI 设备路径协议                | 9.2                        | 显式 Windows 要求   |
|   EFI 设备路径实用工具协议      | 9.5                        |                                |
|   EFI 解压缩协议                 | 18.5                       |                                |
|   EBC 解释器协议                | 20.11                      |                                |
| **有条件地要求 UEFI 协议** |                            |                                |
|   EFI 简单文本输入协议          | 11.3                       | 显式 Windows 要求   |
|   EFI 简单文本输入 EX 协议       | 11.2                       |                                |
|   EFI 简单文本输出协议         | 11.4                       |                                |
|   EFI 图形输出协议            | 11.9                       | 显式 Windows 要求   |
|   EFI EDID 发现的协议            | 11.9.1                     |                                |
|   EFI EDID 活动协议                | 11.9.1                     |                                |
|   EFI 块 IO 协议                   | 12.8                       | 显式 Windows 要求   |
|   EFI 磁盘 IO 协议                    | 12.7                       |                                |
|   EFI 简单文件系统协议         | 12.4                       |                                |
|   EFI Unicode 排序规则协议          | 12.10                      |                                |
|   EFI 简单网络协议             | 21.1                       |                                |
|   EFI PXE 基本代码协议              | 21.3                       |                                |
|   EFI boot 整体性服务协议    | 21.5                       |                                |
|   EFI 串行 IO 协议                  | 11.8                       |                                |
|   UEFI ARM 绑定                        | 2.3.5                      | 显式 Windows 要求   |
| **安全要求**                 |                            |                                |
|   安全启动                             | 27.0                       | 显式 Windows 要求   |
|   启动管理器要求               | 3.1、3。3                   | 显式 Windows 要求   |

## <a name="efi-system-table-requirements"></a>EFI 系统表要求

EFI 系统表必须符合所实现的版本级别中的标准定义。 EFI 系统表指向的配置表必须包含下表中描述的两个 Guid 及其关联的指针。

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
<td><p>此 GUID 必须指向平台 (RSDP) 的 ACPI 根系统说明指针。</p></td>
</tr>
<tr class="even">
<td>SMBIOS_Table GUID</td>
<td><p>此 GUID 必须指向 SMBIOS 入口点结构。</p>
<p>Windows 要求 SMBIOS 规范为2.4 或更高版本。 需要3.2 节 "所需的结构和数据"，以及4个 "一致性指南"。 Windows SMBIOS 兼容性测试可用。</p></td>
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
<td>Windows 要求所有内存服务。</td>
</tr>
<tr class="even">
<td>协议处理程序服务</td>
<td><p>Windows 需要以下协议处理程序服务：</p>
<ul>
<li><p>OpenProtocol ( # A1</p></li>
<li><p>CloseProtocol ( # A1</p></li>
<li><p>LocateDevicePath ( # A1</p></li>
<li><p>LocateHandle ( # A1</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>映像服务</td>
<td><p>Windows 需要以下映像服务：</p>
<ul>
<li><p>ExitBootServices ( # A1</p></li>
</ul></td>
</tr>
<tr class="even">
<td>其他启动服务</td>
<td><p>Windows 需要以下其他启动服务：</p>
<ul>
<li><p>延迟 ( # A1</p></li>
</ul>
<div class="alert">
<strong>注意</strong>   需要 ( # A1 实现才能具有确定性 (可重复) 错误，以便可以可靠地纠正错误或取消。
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
<li><p>GetTime ( # A1</p></li>
<li><p>SetTime ( # A1</p>
<div class="alert">
<strong>注意</strong>   在 ExitBootServices ( # A2 # A3 用于访问平台时间的硬件之前，将仅在 boot (中调用时间服务。
</div>
<div>
 
</div></li>
</ul></td>
</tr>
<tr class="even">
<td>变量服务</td>
<td><p>在系统的目标类上管理多个启动设备和安全变量需要所有 UEFI 变量服务。</p></td>
</tr>
<tr class="odd">
<td>其他运行时服务</td>
<td><p>Windows 需要以下其他运行时服务：</p>
<ul>
<li><p>ResetSystem ( # A1</p>
<div class="alert">
<strong>注意</strong>   ResetSystem ( # A1 实现必须支持重置和关闭选项。
</div>
<div>
 
</div></li>
</ul></td>
</tr>
</tbody>
</table>

## <a name="protocol-requirements"></a>协议要求

下表描述了 Windows 在启动过程中完成特定功能所需的 UEFI 协议。

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
<td><p>Windows 要求 (GOP) 的图形输出协议。 特定帧缓冲区要求如下：</p>
<ul>
<li><p>对于集成显示器， <em>HorizontalResolution</em> 和 <em>VerticalResoluton</em> 必须是面板的本机分辨率。</p></li>
<li><p>对于外部显示器， <em>HorizontalResolution</em> 和 <em>VerticalResoluton</em> 必须为显示器的本机分辨率，或者，如果不支持，则为视频适配器和连接显示支持的最高值。</p></li>
<li><p><em>PixelsPerScanLine</em> 必须等于 <em>HorizontalResolution</em>。</p></li>
<li><p><em>PixelFormat</em> 必须为 <em>PixelBlueGreenRedReserved8BitPerColor</em>。 请注意，需要物理帧缓冲区;不支持 <em>PixelBltOnly</em> 。</p></li>
</ul>
<p>在将执行移交给 UEFI 引导应用程序时，固件启动管理器和固件不得将帧缓冲区用于任何目的。 启动服务退出后，必须继续扫描帧缓冲区。</p></td>
</tr>
<tr class="even">
<td>备用显示输出</td>
<td><p>UEFI 固件必须支持使用硬件支持的任何显示连接器进行启动。 如果内部面板已连接并且可见，则必须使用内部面板。 显示了物理连接的所有输出都必须显示启动屏幕。 对于连接显示器，UEFI 固件必须：</p>
<ul>
<li><p>如果可以确定本机分辨率，请将输出初始化为显示的本机模式。</p></li>
<li><p>如果不能使用纯模式，则必须将其初始化为最高的兼容模式。</p></li>
<li><p>如果无法确定显示功能，则必须在以 60Hz)  (通常为640x480 或1024x768 的相同模式下初始化已连接的显示器。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>在启动时输入</td>
<td><p>需要提供 EFI 简单文本输入协议，才能在内置键盘或附加键盘的系统上进行启动选择或其他菜单选择。 对于无键盘系统，建议在启动环境中使用三个按钮：</p>
<ul>
<li><p>“开始”按钮</p></li>
<li><p>调高音量按钮</p></li>
<li><p>"音量减小" 按钮</p></li>
</ul>
<p>按钮按下应通过 EFI 简单文本输入协议进行报告，方法是将它们分别映射到以下键盘键：</p>
<ul>
<li><p>Windows 键</p></li>
<li><p>向上键</p></li>
<li><p>向下键</p></li>
</ul></td>
</tr>
<tr class="even">
<td>本地存储启动</td>
<td><p>Windows 需要块 i/o 协议和设备路径协议对包含 EFI 系统分区和 Windows OS 分区的存储解决方案的支持。 若要从需要磨损或其他 flash 管理的闪存存储启动，必须在固件中实现此操作， (不在 UEFI 应用程序) 中。</p></td>
</tr>
</tbody>
</table>

## <a name="security-requirements"></a>安全要求

Windows 在安全启动、标准启动、加密和数据保护方面具有安全要求。 下表详细介绍了这些要求。 此外，对于其中 SoC 硬件阻止现有标准 (TPM、RTC 等) 的区域，还会开发其他要求。 表的末尾介绍了这些步骤。

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
<li><p>要求1：必填。 平台应符合本部分中指定的所有要求。</p></li>
<li><p>要求2：必填。 平台应为 UEFI 类3，无兼容性支持模块安装或可安装。 必须禁用 BIOS 仿真和旧式 PC/AT boot。</p></li>
</ul></td>
</tr>
<tr class="even">
<td>UEFI 安全启动</td>
<td><ul>
<li><p>要求3：必填。 在 UEFI v1.0 第27节中定义的安全引导必须附带启用并且签名数据库 (EFI_IMAGE_SECURITY_DATABASE) 安全预配的计算机必需的。 签名数据库的初始内容取决于所需的第三方 UEFI 驱动程序、恢复需求以及计算机上安装的 OS 启动加载程序，但应包括 Microsoft 提供的 EFI_CERT_X509 签名。 不应存在其他签名。</p></li>
<li><p>要求4：必填。 缺少 UEFI "已禁止" 的签名数据库 (EFI_IMAGE_SECURITY_DATABASE1) 是必需的。</p></li>
<li><p>要求5：必填。 由 Microsoft 提供的 UEFI KEK 应包括在 UEFI KEK 数据库中。 不应存在其他 Kek。 Microsoft 将以 EFI_CERT_X509 签名的形式提供 KEK。</p></li>
<li><p>要求6：必填。 PK<em><sub>pub</sub></em> 密钥应存在并存储在固件闪存中。</p>
<div class="alert">
<strong>注意</strong>   由于 PK<em><sub>特权</sub></em> (pk<em><sub>pub</sub></em>的私钥对应) 控制使用 pk<em><sub>pub</sub></em>预配的所有设备上的安全启动策略，因此必须严格保护其保护和使用。
</div>
<div>
 
</div></li>
<li><p>要求7：必填。 初始的签名数据库应存储在固件刷新中，只能通过 OEM 签名的固件更新或通过 UEFI 身份验证的变量写入来进行更新。</p></li>
<li><p>要求8：必填。 不能执行签名验证失败的启动路径中的映像，并且应将失败原因添加到 EFI_IMAGE_EXECUTION_TABLE。 此外，在这种情况下，建议的方法是 UEFI 启动管理器根据特定于 OEM 的策略启动恢复。</p></li>
<li><p>要求9：必填。 对于未通过签名验证的 UEFI 映像，不得允许实际存在的用户覆盖。</p></li>
<li><p>要求10：可选。 OEM 可以为物理上的用户实现此功能，使其能够使用 PK<em><sub>特权</sub></em> 访问或通过固件设置物理状态关闭安全启动。 可以通过特定于平台的方式保护对固件设置的访问， (管理员密码、智能卡、静态配置等 ) </p></li>
<li><p>要求11：实现要求10时是必需的。 如果关闭安全引导，则所有现有 UEFI 变量都不应访问。</p></li>
<li><p>要求12：可选。 OEM 可以为物理上的用户实现在固件设置中选择两种安全启动模式的功能： "自定义" 和 "标准"。 自定义模式允许更灵活，如以下所示。</p></li>
<li><p>要求13：如果实现了要求12，则为必需。 可以通过设置特定于所有者的 <em>PK</em>，在自定义模式下重新启用禁用的安全启动。 管理应按照 UEFI 规范（2.3.1：固件/OS 密钥交换）的27.5 节中的定义继续进行。 在自定义模式下，设备所有者可以在签名数据库中设置他们选择的签名。</p></li>
<li><p>要求14：如果实现了要求12，则为必需。 固件设置应指出是否启用了安全启动，以及是否在标准或自定义模式下操作。 固件设置应提供一个选项，以从自定义模式返回到标准模式。</p></li>
<li><p>要求15：必填。 如果固件设置被重置为出厂默认值，则应删除所有自定义集的受保护的变量，并且应与原始的制造商预配的签名数据库一起重新建立原始 PK<em><sub>pub</sub></em> 。</p></li>
<li><p>要求16：必填。 驱动程序签名应使用 Authenticode 选项 (WIN_CERT_TYPE_PKCS_SIGNED_DATA) 。</p></li>
<li><p>要求17：必填。 对 EFI_IMAGE_EXECUTION_INFO_TABLE (的支持，即在启动) 期间创建和存储映像的信息的创建和存储。</p></li>
<li><p>需求18：必填。 支持对 EFI_IMAGE_SECURITY_DATABASE ( # A1， (授权和禁止的签名数据库) 。</p></li>
<li><p>要求19：必填。 使用 Microsoft KEK 进行身份验证时，支持 SetVariable ( # A1 的 EFI_IMAGE_SECURITY_DATABASE (授权和禁止的签名数据库) 。</p></li>
<li><p>要求20：必填。 EFI_HASH_SERVICE_BINDING_PROTOCOL：服务支持： CreateChild ( # A1，DestroyChild ( # A3。</p></li>
<li><p>要求21：必填。 EFI_HASH_PROTOCOL。 服务支持：哈希 ( # A1。 支持 SHA_1 和 256 SHA-1 哈希算法。 必须支持至少 10 Mb 的消息传递。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>UEFI 标准启动</td>
<td><p>以下要求并不意味着需要 TCG TPM 实现;但它们却意味着需要对受影响的区域使用等效功能。</p>
<p>平台支持可以通过在安全执行环境中执行的 TPM 的固件实现来提供，在加密加速引擎之上进行分层，并利用独立存储。 Microsoft 可能会提供供供应商使用的此类 TPM 实现的参考软件。 这会进一步讨论。</p>
<ul>
<li><p>要求22：必填。 平台应符合 <a href="/previous-versions/windows/hardware/hck/jj923068(v=vs.85)" data-raw-source="[UEFI Trusted Execution Environment EFI Protocol](/previous-versions/windows/hardware/hck/jj923068(v=vs.85))">UEFI 可信执行环境 Efi 协议</a>中指定的 efi 协议。</p></li>
<li><p>要求23：必填。 平台应遵循 TCG EFI 平台规范，其中添加了以下内容：</p>
<ul>
<li><p>在支持在 TrEE EFI 协议中定义的接口的平台上，PK<em><sub>pub</sub></em> 的摘要应扩展为 TPM PCR [03] 作为 EV_EFI_VARIABLE_CONFIG 事件。</p></li>
<li><p>授权的签名数据库内容的摘要 (参阅 UEFI 规范 v4.0) 列表的第27.8 部分必须在以 EV_EFI_VARIABLE_CONFIG 事件的度量启动中扩展。 "扩展" 操作应为 "TPM PCR [03]"。</p></li>
<li><p>UEFI 客户端应可以使用 EFI_IMAGE_SECURITY_DATABASE 变量来读取和解析证书列表，并根据扩展值验证摘要。</p></li>
<li><p>TCG_PCR_EVENT 摘要值应为 SHA-256，而不是 SHA-1。</p></li>
</ul></li>
<li><p>要求24：必填。 平台必须实现 <a href="https://trustedcomputinggroup.org/wp-content/uploads/Platform-Reset-Attack-Mitigation-Specification.pdf" data-raw-source="[TCG Platform Reset Attack Mitigation Specification](https://trustedcomputinggroup.org/wp-content/uploads/Platform-Reset-Attack-Mitigation-Specification.pdf)">TCG 平台重置攻击缓解规范</a>中定义的 MemoryOverwriteRequestControl。</p></li>
</ul></td>
</tr>
<tr class="even">
<td>加密</td>
<td><ul>
<li><p>要求25：强制。 平台应为卸载加密哈希操作提供 EFI_HASH_PROTOCOL (UEFI v1.0) 27.4 部分。 必须支持 SHA-256。</p></li>
<li><p>要求26：必填。 平台应支持 Microsoft 定义的 <a href="uefi-entropy-gathering-protocol.md" data-raw-source="[EFI_RNG_PROTOCOL](uefi-entropy-gathering-protocol.md)">EFI_RNG_PROTOCOL</a> ，以进行 OS 预操作系统读取。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>数据保护</td>
<td><ul>
<li><p>要求27：必填。 平台必须支持具有以下 UEFI 变量属性集组合的 EFI 变量：</p>
<ul>
<li><p>EFI_VARIABLE_BOOTSERVICE_ACCESS</p></li>
<li><p>EFI_VARIABLE_NON_VOLATILE</p></li>
<li><p>EFI_VARIABLE_AUTHENTICATED_WRITE_ACCESS</p></li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<td>其他安全要求</td>
<td><p>Windows 上的 SoC 平台需要以下附加要求。</p>
<ul>
<li><p>Microsoft 定义了从 UEFI 平台收集平均信息量的协议。 尽管不是 UEFI 要求，但 Windows 在 SoC 平台上是必需的。 有关此协议的详细信息，请参阅 <a href="uefi-entropy-gathering-protocol.md" data-raw-source="[UEFI entropy gathering protocol](uefi-entropy-gathering-protocol.md)">UEFI 熵收集协议</a>。</p></li>
<li><p>UEFI 签名数据库更新。 在 UEFI 2.3.1 的第27节中采用了用于更新已验证的变量的一种新机制。 Windows 需要此机制。</p></li>
<li><p>受信任的执行环境。 Microsoft 已开发了一个 EFI 协议，用于与受信任的执行环境交互 (树) ，与受信任计算组的子集 (TCG) 受信任的平台模块 (TPM) 的功能类似。 EFI 协议利用受信任的计算组，使用较大的 "TCG EFI 协议" 版本1.2 修订版1.00 （6月9日2006）。</p>
<p>有关详细信息，请参阅 <a href="/previous-versions/windows/hardware/hck/jj923068(v=vs.85)" data-raw-source="[UEFI Trusted Execution Environment EFI Protocol](/previous-versions/windows/hardware/hck/jj923068(v=vs.85))">UEFI 可信执行环境 EFI 协议</a>。</p></li>
</ul></td>
</tr>
</tbody>
</table>

## <a name="firmware-boot-manager-requirements"></a>固件启动管理器要求

固件启动管理器必须支持规范的3.3 节中定义的默认启动行为。 此外，为支持多启动、全局定义的变量以及规范的第3.1 节的启动管理器要求。

## <a name="uefi-arm-binding-requirements"></a>UEFI ARM 绑定要求

UEFI ARM 绑定包括特定于 ARM 平台的要求，这些要求必须符合 UEFI 规范要求。 Windows 要求 ARM 绑定中所有适用于 ARMv7 的内容。 由于 Windows 不支持 ARMv7 之前的任何内容，因此，特定于 ARMv6k 和更低版本的绑定中的要求是可选的。

绑定指定如何配置 MMU，并指定物理内存的映射方式。 绑定还指定对 UEFI 协议和服务的调用应仅在 ARM ISA 中进行，这意味着在 Thumb2 或 Thumb 中运行的软件需要在调用 UEFI 函数之前切换回 ARM 模式。

## <a name="uefi-arm-multiprocessor-startup-requirements"></a>UEFI ARM 多处理器启动要求

Microsoft 已开发了一个协议，用于在多处理器 UEFI 平台上启动多个 ARM 核心。 ARM 平台上的 Windows 需要此协议，但不支持 [)  (PSCI 的电源状态协调接口 ](https://static.docs.arm.com/den0022/d/Power_State_Coordination_Interface_PDD_v1_1_DEN0022D.pdf)。 支持 PSCI 的平台不能使用此协议。 有关此协议的详细信息，请参阅 ACPI 组件体系结构 (ACPICA) 网站上的 [基于 UEFI ARM 平台的多处理器启动](https://acpica.org/sites/acpica/files/MP%20Startup%20for%20ARM%20platforms.docx) 文档。

## <a name="platform-setup-requirements"></a>平台设置要求

在将系统硬件交付到 OS 加载程序之前，固件负责将系统硬件置于明确定义的状态。 下表定义了相关的平台设置要求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>要求</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>启动路径</td>
<td>固件必须将平台初始化为 Windows 能够通过 UEFI 访问启动设备的点，并加载内核。 对于要从启动设备读取的层次结构中涉及的任何设备，都必须按合理的速率进行时钟和电源计算，前提是性能和电源注意事项。 基本处理器核心本身还应以合理的速率进行时钟和电源，以便系统可以及时启动，而不会耗尽电池。</td>
</tr>
<tr class="even">
<td>核心系统资源</td>
<td><p>通过 ACPI 表向操作系统公开的核心系统资源必须开机并进行时钟。 核心系统资源包括中断控制器、计时器和必须由操作系统管理的 DMA 控制器。</p>
<p>此外，必须通过调用 ExitBootServices ( # A1 来屏蔽中断，直到 OS 解除中的关联设备驱动程序，然后在设备上重新启用中断。 如果在启动服务期间启用中断，则假定固件将对其进行管理。</p></td>
</tr>
<tr class="odd">
<td>调试</td>
<td>Windows 支持通过 USB 3 主机 (XHCI) 、USB 2 主机 (EHCI) 1、IEEE 1394、串行和 USB 函数接口 (以及 PCI 以太网适配器) 进行调试。 在 OS 切换之前，固件中必须至少有一个处于 "已启动"、"时钟" 和 "已被" 初始化。 无论提供哪种选项，它都必须有一个已公开的端口用于调试，并且必须通过专用的 (非共享) 外围总线来连接控制器。</td>
</tr>
<tr class="even">
<td>其他平台设置要求</td>
<td>在将控制权移交给 OS 加载程序之前，必须在固件中完成任何 pin 复用和 pad 配置。</td>
</tr>
</tbody>
</table>

## <a name="installation-requirements"></a>安装要求

Windows 要求 OS 分区驻留在 GPT 分区的存储解决方案上。 可以使用 MBR 分区存储作为数据存储。 如 UEFI 规范中所定义，UEFI 平台需要专用的系统分区。 Windows 需要此专用系统分区（称为 EFI 系统分区） (ESP) 。

## <a name="hardware-security-test-interface-hsti-requirement"></a>硬件安全测试界面 (HSTI) 要求

平台必须实现硬件安全测试接口，并且需要平台来共享 [硬件安全测试规范](/windows-hardware/test/hlk/testref/hardware-security-testability-specification)中指定的文档和工具。

## <a name="related-topics"></a>相关主题

[SoC 平台上的 Windows 的最低 UEFI 要求](minimum-uefi-requirements-for-windows-on-soc-platforms.md)  

[Windows 10 移动版的 UEFI 要求](uefi-requirements-specific-to-windows-mobile.md)  

[USB 刷写支持的 UEFI 要求](uefi-requirements-for-usb-flashing-support.md)