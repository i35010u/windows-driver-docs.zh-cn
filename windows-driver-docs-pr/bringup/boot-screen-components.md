---
title: 启动屏幕组件
description: OEM 徽标和更新文本，有两个组件固件更新启动屏幕。
ms.assetid: 7ACD6BFC-AB92-4BCC-A9E1-9574D959B577
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 02f07f71943a6ad1a5433d26da7c66b01be0f8e8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563812"
---
# <a name="boot-screen-components"></a>启动屏幕组件

有两个组件固件更新启动屏幕： OEM 徽标和更新文本。 本主题提供有关如何配置每个这些组件的指南和有关如何将这些组件传递到中的固件更新的固件信息马蹄形。

## <a name="oem-logo"></a>OEM 徽标

固件更新启动屏幕中的 OEM 徽标必须是相同的正常启动过程中显示的徽标。 对于固件更新的启动屏幕徽标必须为相同的大小、 位置和正常启动过程中显示的预期质量。

### <a name="oem-logo-file"></a>OEM 徽标文件

客户会看到任何可操作的屏幕之前，您的 OEM 徽标将显示启动屏幕上。 

未在 OOBE 中的任何屏幕上显示 OEM 徽标和 OOBE 后它会显示**Control Panel**下**性能信息和工具**。 它不会显示在**设置**应用。

POST （开机自检） 和操作系统的启动时间比以前更快。 若要确保你有正确的标记时间，OEM 徽标是可见的跨 POST 和操作系统启动。 在这种方法，OEM 徽标是易于识别、 适当持续和快速、 可靠的体验与相关联。

此外，作为商标元素中显示 OEM 徽标**Control Panel**应用程序下**性能信息和工具**。 它不会显示在**设置**应用。

#### <a name="create-the-logo"></a>创建徽标

添加的徽标向客户提供其第一次 visual 遇到使用其新的 Pc 运行 Windows，因此它应是干净、 清晰，且其边缘上以及在清晰。

启动屏幕的背景始终为黑色，因此请使用一个徽标，它看起来很棒黑色背景上。 徽标还必须具有 true 黑色背景，因此没有任何明显的区别，其中徽标的黑色背景结束和屏幕的黑色背景开始。 不支持透明度。 黑色背景来优化系统性能的徽标和转换从 UEFI 图形输出协议 (GOP) 为操作系统本机视频驱动程序的启动末尾淡出这两个初始呈现。 Windows 的其他领域还使用你的徽标：安装程序、 Push-Button 重置 (PBR)、 安全启动修正和启动修复工具，它们都使用黑色背景。 这些体验使用相同的徽标从启动图形资源表 (BGRT)。

#### <a name="position-the-logo-during-post"></a>在 POST 期间放置徽标

固件在开机自检绘制 OEM 徽标，并将徽标放置在预先确定的位置。 当 Windows 启动开始时，视频缓冲区中保留徽标。 通过读取其 EDID （扩展显示标识数据），桌面可以检测到面板的自身分辨率。

若要使正确显示跨整个序列的徽标，POST 需要出现在设备的本机分辨率。 这可确保徽标的大小、 形状和所需的位置，并且 Windows 要求。

徽标应显示在特定位置来展示 PC 的品牌屏幕上。 我们建议徽标放置在屏幕的上边缘的 38.2%其中心。 这种放置取决于黄金比率的视觉效果，并与 Windows 10 设计比例相匹配。 在运行 Windows 10 的所有 Pc 之间此一致定位允许 Windows 将进度环放在正确位置，并确保徽标和环会以可视方式平衡。

以进一步支持此种视觉平衡，我们建议您限制徽标大小为 40%的屏幕的高度和宽度。 这可确保正确，显示的屏幕和该 Windows 可以正确淡出末尾的启动徽标。 我们建议徽标的最大区域开始不超过 18.2%从屏幕的顶部。

这些设计原则适用于横向与纵向的设备。

#### <a name="add-the-logo-to-the-bgrt"></a>将徽标添加到 BGRT

除了在 POST 期间正确定位徽标，你还应用商店徽标内启动图形资源表 (BGRT)。 BGRT 动态定义的 Windows，用于描述资源的新对象和屏幕位置。 存储在 EfiBootServicesData 徽标，并将其公开通过 BGRT。 BGRT 接口支持 24 位位图像素格式为 0xRRGGBB 或使用 0xrrRRGGBB，其中 rr 保留的像素格式的 32 位位图作为此徽标。 这是一个标准接口，Windows 使用访问徽标。

BGRT 中两个重要的字段是"图像偏移量 X"和"图像偏移量 Y"。 这些是 （x，y） 值的左上角的徽标屏幕上的位置。 当设置这些值时，请确保不使用徽标的位置或边界框或 Windows 的左上角不会正确位置中安装程序、 启动修复、 Push-Button 重置，或其他体验的徽标。

应最大程度减少徽标资源中的填充和使用仅是必要的正确居中。 使用最小填充在固件中节省空间，并允许 Windows 能正确缩放基于 BGRT 的徽标。 

> [!NOTE]
> OEM 徽标不出现在任何满足在 OOBE 屏幕上。

有关 BGRT 的其他详细信息，请参阅部分 5.2.22[高级配置和电源接口 (ACPI) 规范](https://www.uefi.org/specifications)。

## <a name="update-text"></a>更新文本

固件更新启动屏幕中的更新文本是一个简单字符串，是可快速读取和理解。 通过 Windows 引导加载程序呈现的文本。 一次它会确定固件更新处于挂起状态，则引导加载程序确定的 Windows 区域设置，并在屏幕上显示的本地化的文本。

在调入 UpdateCapsule 期间引导加载程序将传递所有固件更新马蹄形。 此外它还将在 Microsoft 定义*固件更新显示*capsule 包含位图的显示的文本和位图在屏幕上的位置。 系统固件 UpdateCapsule 方法必须保留胶囊形，以便清除或修改屏幕时它可以重新显示在屏幕上的位图。

![固件更新启动屏幕组件](images/firmwareupdatebootscreencomponents.png)

## <a name="windows-firmware-update-display-capsule"></a>Windows 固件更新显示 capsule

当 Windows 引导加载程序调用到系统固件 UpdateCapsule 方法时，它会传入所有固件更新马蹄形。 此外它将在 Windows 用户体验 capsule 中传递。 此 capsule 包含的位图呈现，必须在屏幕上显示的本地化的文本。 下列 GUID 用于标识此 capsule: {3b8c8162-188c-46a4-aec9-be43f1d65697}。

就用户体验胶囊形将马蹄形数组中的显示的顺序不能保证。 不依赖特定索引位置查找 UX capsule。 一种最佳做法包括扫描寻找 UX capsule，处理就可处理数组中的剩余固件马蹄形的数组。

务必要注意可能会在其中将有某些情况下没有 UX capsule。 例如，将在具有不显示适配器的无外设服务器的情况下没有 UX capsule。 在这种情况下固件 UpdateCapsule 调用可以忽略 UX 封装要求。 但是如果 UX Capsule 存在，然后 UpdateCapsule 必须处理它根据在本部分中所述的过程。

下表描述了用户体验 capsule 的固件更新显示标头。

| 字段 | 字节长度 | 字节偏移量 | 描述 
|---|---|---|---|
| CapsuleGuid      | 16 | 0 | 固件\_更新\_显示\_CAPSULE |
| HeaderSize       | 4  | 16 | sizeof(EFI\_CAPSULE\_HEADER) |
| Flags            | 4           | 20          | CAPSULE\_FLAGS\_PERSIST\_ACROSS\_RESET |
| CapsuleImageSize | 4           | 24          | 描述固件更新的长度的 4 字节无符号的整数显示 capsule。 大小包括标头和 capsule，其中包括显示的图像。 |

下表描述了固件更新显示封装有效负载。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>字段</th>
<th>字节长度</th>
<th>字节偏移量</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>版本</td>
<td>1</td>
<td>28</td>
<td>标识实现显示 capsule 的修订版本。 此字段将设置为 1。</td>
</tr>
<tr class="even">
<td>校验和</td>
<td>1</td>
<td>29</td>
<td>包含要启用简单的验证的校验和。 整个 capsule （标头和有效负载） 之和包括显示的图像，必须等于零。 如果总和不等于零，则应忽略胶囊形。</td>
</tr>
<tr class="odd">
<td>ImageType</td>
<td>1</td>
<td>30</td>
<td>指定嵌入图像的格式：
<ul>
<li>0:位图</li>
<li>1-255:保留供将来使用。</li>
</ul></td>
</tr>
<tr class="even">
<td>保留</td>
<td>1</td>
<td>31</td>
<td>保留供将来使用。 必须为零。</td>
</tr>
<tr class="odd">
<td>模式</td>
<td>4</td>
<td>32</td>
<td>指定的图形输出协议视频模式能够显示嵌入的图像。 视频模式在调用 UpdateCapsule 之前查询，并描述的当前视频模式和本地显示的视频模式的启动加载器显示嵌入的图像时。 该值等于 EFI_GRAPHICS_OUTPUT_PROTOCOL_MODE 结构的模式字段呈现图像时。</td>
</tr>
<tr class="even">
<td>图像偏移量 X</td>
<td>4</td>
<td>36</td>
<td>4 字节 （32 位） 无符号长描述位图图像的 X 偏移量。 （X，Y） 显示的图像的左上角的偏移量。 显示的左上的角位于 （0，0） 的偏移量。</td>
</tr>
<tr class="odd">
<td>图像偏移 Y</td>
<td>4</td>
<td>40</td>
<td><p>4 字节 （32 位） 无符号长描述位图图像的 Y 偏移量。 （X，Y） 显示的图像的左上角的偏移量。 显示的左上的角位于 （0，0） 的偏移量。</p>
<img src="images/imageoffsetrelativetodisplay.png" alt="Image offset value relative to display" /></td>
</tr>
<tr class="even">
<td>图像</td>
<td>不可用</td>
<td>44</td>
<td>一个字节的数组，其中包含嵌入的位图，以显示固件更新过程中。 位图可以是 24 位位图像素格式 0xRRGGBB 或 32 位位图像素格式 0xrrRRGGBB，其中保留 rr。</td>
</tr>
</tbody>
</table>

请注意，与不同的固件更新有效负载生成 capsule，显示封装负载没有填充页面对齐。 显示有效负载紧随封装标头。

固件更新显示 capsule 介绍固件更新的持续期间必须呈现的图形。 最开始呈现图形和 Windows 的显示，并作为一部分包含对固件更新 payload(s) 相同 UpdateCapsule 调用移交给固件。 如果固件重置系统或视频设备固件必须重新显示在显示 capsule 中提供的位图。 如果物理内存不会保留在重置，则固件可能需要将该位图保存到持久性存储区以在重置之后重新显示位图。 有关如何保存和还原位图跨重置的详细信息是特定于实现的并不在本文中讨论。

固件更新显示 capsule 建模从启动图形资源表 (BGRT) 在 ACPI 5.0 中定义。 BGRT 定义系统固件来提供到 OS 启动加载程序的图形的机制。 尽管两个表类似，有几个明显的差异。

| BGRT | 固件更新显示 capsule | 原因 |
|---|---|---|
| 指向位图 | 通过嵌入位图，capsule 保存和还原单个操作。 | 0 |
| 不包含视频模式 | 包含视频的模式 | 为了避免 UpdateCapsule 调用期间需要为查询视频模式的固件。 |
| 包含状态字段 | 不包含状态字段 | BGRT 的状态字段描述图像当前是否显示在屏幕上。 这不是适用于固件更新显示 capsule。 |

## <a name="related-topics"></a>相关主题

[用户体验的 UEFI 固件更新](user-experience-for-uefi-firmware-updates.md)  
