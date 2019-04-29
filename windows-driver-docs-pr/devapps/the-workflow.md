---
title: 构建 UWP 设备应用
description: 设备制造商可以创建用作设备配套的 UWP 设备应用。
ms.assetid: DB88876E-3C92-40E9-A2E2-19493F3357B5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 213869001380bd45adae241e6f26d31ef7266e28
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379493"
---
# <a name="building-uwp-device-apps"></a>构建 UWP 设备应用


设备制造商可以创建用作设备配套的 UWP 设备应用。 本主题介绍 UWP 设备应用，生成一个的基本步骤和必须分别提交到 Microsoft Store 仪表板和 Windows 开发人员中心硬件仪表板中，你应用程序和设备的元数据的顺序的组件。 每个步骤的更多详细信息，请参阅[构建循序渐进的 UWP 设备应用程序](build-a-uwp-device-app-step-by-step.md)。

## <a name="span-idthebuildingblocksspanspan-idthebuildingblocksspanspan-idthebuildingblocksspanthe-building-blocks"></a><span id="The_building_blocks"></span><span id="the_building_blocks"></span><span id="THE_BUILDING_BLOCKS"></span>构建基块


在最基本级别*UWP 设备应用*是与特定设备通过设备元数据相关联的 UWP 应用。 有四个组件与 UWP 设备应用： 设备、 应用、 设备元数据包和设备驱动程序。 不需要使用设备元数据来访问外围设备使用设备协议 （USB、 HID、 蓝牙 GATT 和蓝牙 RFCOMM） 的 Api。 但需要使用设备元数据来启用特殊功能，例如[自动安装](auto-install-for-uwp-device-apps.md)，[自动播放](autoplay-for-uwp-device-apps.md)，并[设备更新](device-sync-and-update-for-uwp-device-apps.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><strong>设备</strong></td>
<td align="left">这是物理设备。 <em>外围设备</em>外部的 PC 机箱。 <em>内部设备</em>是驻留在或集成在一起的 PC 机箱的设备。</td>
</tr>
<tr class="even">
<td align="left"><strong>App</strong></td>
<td align="left">UWP 设备应用程序是为该设备，使用户可以访问设备的唯一功能提供了自定义的用户体验的 UWP 应用。 设备应用程序包含一个名为<strong>StoreManifest.xml</strong>指定体验 id。 <em>体验 ID</em>是一个 GUID，唯一标识设备元数据包。</td>
</tr>
<tr class="odd">
<td align="left"><strong>设备元数据</strong></td>
<td align="left">这是您可能已经创建了 Windows 7 的任何设备元数据包的扩展的版本。 在 Windows 8.1 的设备元数据创建设备和应用之间的链接。 该链接标识体验 id。 除了 PC （可本地化的型号名称、 描述和图像逼真的图标） 的 UI 内容指定设备元数据包<a href="autoplay-for-uwp-device-apps.md" data-raw-source="[AutoPlay](autoplay-for-uwp-device-apps.md)">自动播放</a>配置和哪些应用程序有权访问设备。 Windows 会自动从 Windows 元数据 Internet Service (WMIS) 下载设备元数据。</td>
</tr>
<tr class="even">
<td align="left"><strong>驱动程序</strong></td>
<td align="left">所有 UWP 设备应用都使用间接来访问设备驱动程序。 例如，Windows 运行时设备协议在 Windows 8.1 中引入的 Api 使用现成驱动程序让你通过 USB、 HID 和蓝牙进行通信的应用。 有关这些 Api 使用的驱动程序的详细信息，请参阅<a href="step-1--create-a-uwp-device-app.md" data-raw-source="[Step 1: Create a UWP device app](step-1--create-a-uwp-device-app.md)">步骤 1:创建 UWP 设备应用</a>。
<div class="alert">
<strong>重要</strong>设备访问使用自定义驱动程序需要获得 Microsoft 的批准。 有关详细信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?LinkId=306693" data-raw-source="[UWP device app Design Guide for Specialized Devices Internal to the PC](https://go.microsoft.com/fwlink/p/?LinkId=306693)">UWP 的设备应用程序的专用设备内部到 PC 的设计指南</a>。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

## <a name="span-iddevelopmentworkflowspanspan-iddevelopmentworkflowspanspan-iddevelopmentworkflowspandevelopment-workflow"></a><span id="Development_workflow"></span><span id="development_workflow"></span><span id="DEVELOPMENT_WORKFLOW"></span>开发工作流


有六个步骤创建 UWP 的设备应用，假定您已创建你的设备并提交到硬件仪表板任何必需的驱动程序。 单击链接以查看有关每个步骤的更多详细信息。

![设备应用开发工作流](images/device-app-workflow.png)

[步骤 1：创建应用](step-1--create-a-uwp-device-app.md)。 将您的应用程序与 Microsoft Store 相关联、 开发应用程序，并对其进行测试。

[步骤 2：创建设备元数据](step-2--create-device-metadata.md)。 使用设备元数据创建向导将您的应用程序与你的设备相关联，请创建设备元数据包，并创建一个 StoreManifest.xml 文件 （它指定体验 ID）。

[步骤 3：向应用添加体验 ID](step-3--add-an-experience-id-to-the-app.md)。 将 StoreManifest.xml 文件合并到您的应用程序。

**请注意**  如果您的应用程序是一个特权的应用程序，并且未配置为自动安装，第 3 步不需要。

 

[步骤 4：测试设备元数据 （本地）](step-4--test-device-metadata.md)。 使用设备元数据创建向导来验证并将其部署到本地开发工作站的设备元数据。

[步骤 5：提交到 Microsoft Store 仪表板应用](step-5--submit-the-app.md)。 使用仪表板确认销售详细信息，然后向测试人员指示应用程序是 UWP 设备应用。

**请注意**  如果您的应用程序是一个特权的应用程序，并且未配置为自动安装，您可以将应用提交到 Microsoft Store 仪表板完成步骤 6 之后。 有关详细信息，请参阅[特权应用程序提交序列](#priv-sequence)。

 

[步骤 6：提交到 Windows 开发人员中心硬件仪表板的设备元数据](step-6--submit-device-metadata.md)。 手动提交设备元数据包，或使用设备元数据创建向导来创建向硬件仪表板可以提交的大容量提交包。

## <a name="span-idstandardsubmissionsequencespanspan-idstandardsubmissionsequencespanspan-idstandardsubmissionsequencespanstandard-submission-sequence"></a><span id="Standard_submission_sequence"></span><span id="standard_submission_sequence"></span><span id="STANDARD_SUBMISSION_SEQUENCE"></span>标准提交序列


第一次提交到各种仪表板，你应用程序和设备的元数据必须按特定顺序发生事件。 下表还显示了当提交设备驱动程序，如适用。

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
<th align="left">继续操作之前...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">1</td>
<td align="left"><strong>将设备驱动程序提交</strong>到硬件仪表板。</td>
<td align="left">等待，直到该驱动程序是可从 Windows 更新。</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left"><strong>将应用程序提交</strong>到 Microsoft Store 仪表板。</td>
<td align="left">等待接受，并且在 Microsoft Store 上实时应用程序之前。</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left"><strong>提交设备元数据</strong>到硬件仪表板。 应用程序需要先在 Microsoft Store 中的元数据可以通过验证硬件仪表板上。</td>
<td align="left">等待 10 天，以便接受和分发。</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left"><strong>完成时间：</strong>用户可以从 Microsoft Store 应用设备应用程序的所有功能获益。 请注意，设备应用程序功能，例如<a href="auto-install-for-uwp-device-apps.md" data-raw-source="[automatic installation](auto-install-for-uwp-device-apps.md)">自动安装</a>，<a href="autoplay-for-uwp-device-apps.md" data-raw-source="[AutoPlay](autoplay-for-uwp-device-apps.md)">自动播放</a>，并<a href="device-sync-and-update-for-uwp-device-apps.md" data-raw-source="[device update](device-sync-and-update-for-uwp-device-apps.md)">设备更新</a>直到用户拥有的设备元数据和应用在 PC 上不起作用。 如果应用需要不由 Microsoft 提供的驱动程序，该驱动程序还需要为应用程序处理。</td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

## <a name="span-idpriv-sequencespanspan-idpriv-sequencespanprivileged-app-submission-sequence"></a><span id="priv-sequence"></span><span id="PRIV-SEQUENCE"></span>特权的应用程序提交序列


在某些情况下，UWP 设备应用程序不必先实时 Microsoft Store 中提交设备元数据。 当 UWP 设备应用：

-   指定为特权的应用程序
-   未配置为自动安装

如果这是有关您的应用程序，则返回 true，然后提交到 Microsoft Store 仪表板 UWP 设备应用程序可以提交到硬件仪表板的设备元数据。 在这种情况下，不需要体验标识添加到您的应用程序;为设备元数据中的特权应用指定您的应用程序是足够的权限，才会生效。

**请注意**  UWP 应用的打印机和相机的设备应用程序自动安装。 因此，这些类型的 UWP 设备应用程序必须遵循标准提交序列，并提交到 Microsoft Store，然后提交设备元数据。

 

## <a name="span-idwindowsstoredeviceapplimitsspanspan-idwindowsstoredeviceapplimitsspanspan-idwindowsstoredeviceapplimitsspanuwp-device-app-limits"></a><span id="Windows_Store_device_app_limits"></span><span id="windows_store_device_app_limits"></span><span id="WINDOWS_STORE_DEVICE_APP_LIMITS"></span>UWP 设备应用的限制


设备制造商在可以在设备元数据中指定用于自动安装和应用特权的 UWP 应用的数量方面受到限制。 例如，每个外围设备生产商 (IHV) 可以最多提交配置为自动安装的一个应用，以及最多一个指定为特权应用的应用。 IHV 可以提交满足这两个限制条件的一个应用，或者提交两个应用，每一个仅满足一个限制条件。

**重要**  设备制造商可以提交到 Microsoft Store 的 UWP 设备应用程序的总数没有限制; 这些限制仅适用于单个设备元数据包。

 

移动运营商和 OEM 在他们可以在设备元数据中指定的应用数量方面有不同的限制。 有关详细信息，OEM 应联系其 Microsoft OEM 代表。

在每个设备元数据包中，适用下列限制：

| 开发人员       | 自动安装应用限制 | 特权应用限制 |
|-----------------|----------------------------------|----------------------|
| IHV             | 1                                | 1                    |
| 移动运营商 | 1                                | 8                    |
| OEM             | 联系 Microsoft                | 联系 Microsoft    |

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[分步构建 UWP 设备应用](build-a-uwp-device-app-step-by-step.md)

[UWP 设备应用的自动安装](auto-install-for-uwp-device-apps.md)

[UWP 设备应用的自动播放](autoplay-for-uwp-device-apps.md)

[UWP 设备应用的设备同步和更新](device-sync-and-update-for-uwp-device-apps.md)

[适用于内部设备的 UWP 设备应用](uwp-device-apps-for-specialized-devices.md)

 

 






