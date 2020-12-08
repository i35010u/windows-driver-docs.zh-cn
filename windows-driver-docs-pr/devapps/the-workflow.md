---
title: 构建 UWP 设备应用
description: 设备制造商可以创建用作设备配套的 UWP 设备应用。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65a96031114ea0532d0e5eff6042b4f23fd6ad26
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802661"
---
# <a name="building-uwp-device-apps"></a>构建 UWP 设备应用


设备制造商可以创建用作设备配套的 UWP 设备应用。 本主题介绍 UWP 设备应用的组件、构建一个组件的基本步骤，以及必须将应用和设备元数据分别提交到 Microsoft Store 仪表板和 Windows 开发人员中心硬件仪表板的顺序。 有关每个步骤的详细信息，请参阅逐步 [生成 UWP 设备应用](build-a-uwp-device-app-step-by-step.md)。

## <a name="span-idthe_building_blocksspanspan-idthe_building_blocksspanspan-idthe_building_blocksspanthe-building-blocks"></a><span id="The_building_blocks"></span><span id="the_building_blocks"></span><span id="THE_BUILDING_BLOCKS"></span>构建基块


在最基本的层面上， *uwp 设备应用* 是一个 uwp 应用，它通过设备元数据与特定设备关联。 UWP 设备应用有四个组件：设备、应用、设备元数据包和设备驱动程序。 不需要使用设备元数据来访问使用设备协议 Api (USB、HID、蓝牙 GATT 和蓝牙 RFCOMM) 的外围设备。 但你确实需要使用设备元数据来启用特殊功能，如 [自动安装](auto-install-for-uwp-device-apps.md)、 [自动播放](autoplay-for-uwp-device-apps.md)和 [设备更新](device-sync-and-update-for-uwp-device-apps.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><strong>设备</strong></td>
<td align="left">这是物理设备。 <em>外围设备</em> 位于 PC 机箱外部。 <em>内部设备</em> 是位于或与 PC 机箱集成的设备。</td>
</tr>
<tr class="even">
<td align="left"><strong>应用</strong></td>
<td align="left">UWP 设备应用是一个 UWP 应用，为设备提供自定义的用户体验，使用户能够访问设备的独特功能。 设备应用包含名为 <strong>StoreManifest.xml</strong> 的文件，该文件指定体验 ID。 <em>体验 ID</em>是一个 GUID，用于唯一标识设备元数据包。</td>
</tr>
<tr class="odd">
<td align="left"><strong>设备元数据</strong></td>
<td align="left">这是你可能已为 Windows 7 创建的任何设备元数据包的扩展版本。 在 Windows 8.1 中，设备元数据将在设备和应用之间创建链接。 该链接在体验 ID 中标识。 除了适用于 PC 的 UI 内容 () 设备元数据包指定 <a href="autoplay-for-uwp-device-apps.md" data-raw-source="[AutoPlay](autoplay-for-uwp-device-apps.md)">自动播放</a> 配置以及哪些应用有权访问该设备。 Windows 将从 Windows 元数据 Internet 服务 (WMIS) 自动下载设备元数据。</td>
</tr>
<tr class="even">
<td align="left"><strong>Driver</strong></td>
<td align="left">所有 UWP 设备应用间接使用驱动程序来访问设备。 例如，在 Windows 8.1 中引入 Windows 运行时设备协议 Api，使用内置驱动程序允许应用通过 USB、HID 和蓝牙进行通信。 有关这些 Api 使用的驱动程序的详细信息，请参阅 <a href="step-1--create-a-uwp-device-app.md" data-raw-source="[Step 1: Create a UWP device app](step-1--create-a-uwp-device-app.md)">步骤1：创建 UWP 设备应用</a>。
<div class="alert">
<strong>重要提示</strong>  使用自定义驱动程序的设备访问权限需要 Microsoft 的批准。 有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=306693" data-raw-source="[UWP device app Design Guide for Specialized Devices Internal to the PC](https://go.microsoft.com/fwlink/p/?LinkId=306693)">适用于 PC 内部专用设备的 UWP 设备应用设计指南</a>。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

## <a name="span-iddevelopment_workflowspanspan-iddevelopment_workflowspanspan-iddevelopment_workflowspandevelopment-workflow"></a><span id="Development_workflow"></span><span id="development_workflow"></span><span id="DEVELOPMENT_WORKFLOW"></span>开发工作流


创建 UWP 设备应用有六个步骤，假设已创建设备，并已将所有必需的驱动程序提交到硬件仪表板。 单击链接以了解有关每个步骤的更多详细信息。

![设备应用开发工作流](images/device-app-workflow.png)

[步骤1：创建应用](step-1--create-a-uwp-device-app.md)。 将应用与 Microsoft Store 相关联，开发应用并对其进行测试。

[步骤2：创建设备元数据](step-2--create-device-metadata.md)。 使用设备元数据创作向导将您的应用程序与设备关联，创建设备元数据包，并创建 StoreManifest.xml 文件 (指定体验 ID) 。

[步骤3：将体验 ID 添加到应用](step-3--add-an-experience-id-to-the-app.md)。 将 StoreManifest.xml 文件合并到应用中。

**注意**  如果你的应用程序是特权应用程序，并且未配置为自动安装，则不需要执行步骤3。

 

[步骤4：测试 (本地) 的设备元数据 ](step-4--test-device-metadata.md)。 使用设备元数据创作向导验证设备元数据并将其部署到本地开发工作站。

[步骤5：将应用提交到 Microsoft Store 仪表板](step-5--submit-the-app.md)。 使用 "仪表板" 确认销售详细信息，并向测试人员指示该应用是 UWP 设备应用。

**注意**  如果你的应用程序是特权应用并且未配置为自动安装，则可以在步骤6后将应用提交到 Microsoft Store 仪表板。 有关详细信息，请参阅 [特权应用提交顺序](#priv-sequence)。

 

[步骤6：向 Windows 开发人员中心硬件仪表板提交设备元数据](step-6--submit-device-metadata.md)。 手动提交设备元数据包，或使用设备元数据创作向导创建可提交到硬件仪表板的批量提交包。

## <a name="span-idstandard_submission_sequencespanspan-idstandard_submission_sequencespanspan-idstandard_submission_sequencespanstandard-submission-sequence"></a><span id="Standard_submission_sequence"></span><span id="standard_submission_sequence"></span><span id="STANDARD_SUBMISSION_SEQUENCE"></span>标准提交顺序


首次将应用和设备元数据提交到各个仪表板时，这些事件必须按特定的顺序发生。 下表还显示了提交设备驱动程序的时间（如果适用）。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">序列</th>
<th align="left">描述</th>
<th align="left">继续之前 .。。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">1</td>
<td align="left">将<strong>设备驱动程序提交</strong>到硬件仪表板。</td>
<td align="left">请等待该驱动程序可用 Windows 更新。</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">将<strong>应用提交</strong>到 Microsoft Store 仪表板。</td>
<td align="left">等待接受，直到应用处于 Microsoft Store 状态。</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">向硬件仪表板<strong>提交设备元数据</strong>。 应用必须位于 Microsoft Store 中，然后元数据才能通过硬件仪表板上的验证。</td>
<td align="left">等待10天用于接受和分发。</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left"><strong>完成：</strong> 用户可以从 Microsoft Store 设备应用的所有功能中获益。 请注意，设备应用功能（如 <a href="auto-install-for-uwp-device-apps.md" data-raw-source="[automatic installation](auto-install-for-uwp-device-apps.md)">自动安装</a>、 <a href="autoplay-for-uwp-device-apps.md" data-raw-source="[AutoPlay](autoplay-for-uwp-device-apps.md)">自动播放</a>和 <a href="device-sync-and-update-for-uwp-device-apps.md" data-raw-source="[device update](device-sync-and-update-for-uwp-device-apps.md)">设备更新</a> ）在用户具有设备元数据和 PC 上的应用之前不起作用。 如果应用需要 Microsoft 不提供的驱动程序，该驱动程序也需要存在，应用才能运行。</td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

## <a name="span-idpriv-sequencespanspan-idpriv-sequencespanprivileged-app-submission-sequence"></a><span id="priv-sequence"></span><span id="PRIV-SEQUENCE"></span>特权应用提交顺序


在某些情况下，在提交设备元数据之前，UWP 设备应用无需位于 Microsoft Store 中。 当 UWP 设备应用：

-   指定为特权应用
-   未配置为自动安装

如果这对你的应用是如此，则可以在将 UWP 设备应用提交到 Microsoft Store 仪表板之前，将设备元数据提交到硬件仪表板。 在这种情况下，不需要将体验 ID 添加到应用中;在设备元数据中将应用指定为特权应用足以使权限生效。

**注意**  用于打印机和照相机的 UWP 设备应用会自动安装。 因此，在提交设备元数据之前，这些类型的 UWP 设备应用必须遵循标准提交顺序并提交到 Microsoft Store。

 

## <a name="span-idwindows_store_device_app_limitsspanspan-idwindows_store_device_app_limitsspanspan-idwindows_store_device_app_limitsspanuwp-device-app-limits"></a><span id="Windows_Store_device_app_limits"></span><span id="windows_store_device_app_limits"></span><span id="WINDOWS_STORE_DEVICE_APP_LIMITS"></span>UWP 设备应用的限制


设备制造商在可以在设备元数据中指定用于自动安装和应用特权的 UWP 应用的数量方面受到限制。 例如，每个外围设备生产商 (IHV) 可以最多提交配置为自动安装的一个应用，以及最多一个指定为特权应用的应用。 IHV 可以提交满足这两个限制条件的一个应用，或者提交两个应用，每一个仅满足一个限制条件。

**重要提示**  设备制造商可以提交到 Microsoft Store 的 UWP 设备应用总数没有限制;这些限制仅适用于单个设备元数据包。

 

移动运营商和 OEM 在他们可以在设备元数据中指定的应用数量方面有不同的限制。 有关详细信息，OEM 应联系其 Microsoft OEM 代表。

在每个设备元数据包中，适用下列限制：

| 开发人员       | 自动安装应用限制 | 特权应用限制 |
|-----------------|----------------------------------|----------------------|
| IHV             | 1                                | 1                    |
| 移动运营商 | 1                                | 8                    |
| OEM             | 联系 Microsoft                | 联系 Microsoft    |

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[分步构建 UWP 设备应用](build-a-uwp-device-app-step-by-step.md)

[UWP 设备应用的自动安装](auto-install-for-uwp-device-apps.md)

[UWP 设备应用的自动播放](autoplay-for-uwp-device-apps.md)

[UWP 设备应用的设备同步和更新](device-sync-and-update-for-uwp-device-apps.md)

[适用于内部设备的 UWP 设备应用](uwp-device-apps-for-specialized-devices.md)

 

 






