---
title: 管理设备元数据体验
description: 管理设备元数据体验
ms.assetid: aede9597-4b67-4c1a-8ae4-924d39c88b53
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 455a1dd138a24352e07233652cb83155c90e4e3f
ms.sourcegitcommit: 4f08f5686c0bbc27d58930b993cbab1a98e3afb0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89443897"
---
# <a name="manage-device-metadata-experiences"></a>管理设备元数据体验

在创建和提交设备元数据体验后，你可以通过仪表板查看或编辑这些体验。

## <a name="managing-your-device-metadata-experiences"></a>管理设备元数据体验

在“管理体验”  页上，你可以添加、删除或提升（从预览到发布）选定体验中的设备元数据包。 你也可以将相同硬件 ID 或型号 ID 的包添加到同一体验（如果这些 ID 针对不同的区域设置）。

## <a name="to-filter-your-device-metadata-experiences"></a>筛选设备元数据体验

1. 从硬件开发人员中心或 Windows 开发人员中心，使用 Microsoft 帐户登录到“仪表板”  。

2. 在窗口左侧，单击“设备元数据”  ，然后单击“管理体验”  。

3. 此时将显示你或你的公司创建的所有体验。 单击列标题可更改列表的顺序。

4. 使用列表顶部的筛选器以仅显示你希望看到的体验。 输入以下一个或多个参数：

|参数|说明|
|---|---|
|体验名称|从列表中，选择你要查看或更新的体验名称。|
|硬件 ID|输入你要查看的硬件 ID，在输入每个 ID 后插入分号。 这将显示包含所选硬件 ID 的体验。
|设备类别|从列表中，选择你要查看的设备类别。|
|型号 ID|输入你要查看的型号 ID，在输入每个 ID 后插入分号。 这将显示包含所选型号 ID 的体验。|

## <a name="to-open-and-view-your-device-metadata-experience"></a>打开并查看设备元数据体验的步骤

1. 单击体验以查看详细信息。

2. 在“体验信息”  下查看信息，其中包括：

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>元素</th>
    <th>说明</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>体验类型</p></td>
    <td><p>体验中的包类型，包括以下各项的元数据：</p>
    <ul>
    <li><p>设备和打印机</p></li>
    <li><p>Device stage</p></li>
    </ul></td>
    </tr>
    <tr class="even">
    <td><p>设备类别</p></td>
    <td><p>体验中包的设备类别。</p></td>
    </tr>
    <tr class="odd">
    <td><p>型号 ID</p></td>
    <td><p>体验的包中定义的型号 ID。</p></td>
    </tr>
    <tr class="even">
    <td><p>硬件 ID</p></td>
    <td><p>体验的包中定义的硬件 ID。</p></td>
    </tr>
    <tr class="odd">
    <td><p>徽标提交 ID</p></td>
    <td><p>绑定到体验的提交 ID。</p></td>
    </tr>
    </tbody>
    </table>

3. 在“元数据包”  下，展开各个程序包以查看详细信息。 还可以下载实时包或准备发布的包。

    >[!NOTE]
    >如果元数据包有错误，它将显示在此处。

4. 可通过单击以下列标题之一对列表进行排序：

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>列标题</th>
    <th>说明</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>名称</p></td>
    <td><p>体验中的包将根据它们的友好名称（如果已提供）或按照它们的文件名列出。</p></td>
    </tr>
    <tr class="even">
    <td><p>提交日期</p></td>
    <td><p>这将显示你提交每个包的日期。</p></td>
    </tr>
    <tr class="odd">
    <td><p>预览</p></td>
    <td><p>如果包处于预览状态，尚未发布，则选中此复选框。</p></td>
    </tr>
    <tr class="even">
    <td><p>Locale</p></td>
    <td><p>这将列出设计包所针对的国家/地区。</p></td>
    </tr>
    <tr class="odd">
    <td><p>默认值</p></td>
    <td><p>“是”指示你已指定为默认包的包。</p></td>
    </tr>
    <tr class="even">
    <td><p>状态</p></td>
    <td><p>此值指示选定包的当前状态，它可以是以下值之一：</p>
    <ul>
    <li><p>挂起：已上传包，正在进行验证。</p></li>
    <li><p>待发布：包已被验证，正在等待发送到元数据服务器。 你可以下载经过验证的包副本，它将在 24 小时后处于实时状态并提供给你的用户。</p></li>
    <li><p>实时：包现在已可供用户下载。</p></li>
    <li><p>错误：在验证期间发现一个或多个错误。 展开该部分可获得详细信息。</p></li>
    </ul></td>
    </tr>
    </tbody>
    </table>

## <a name="to-modify-your-device-metadata-experience"></a>修改设备元数据体验的步骤

1. 若要发布预览程序包，请选择该程序包，然后单击“发布”  。

    >[!NOTE]
    >用户最长可能需要等待 48 小时后才能下载发布的文件。

2. 若要从体验中删除某个程序包，请选择该程序包，然后单击“删除”  。

   >[!NOTE]
   >你只能删除处于“实时”  或“错误”  状态的程序包。

3. 若要更新现有程序包，请选择该程序包、单击“删除”  ，然后创建并上载新程序包。

    有关创建新程序包的详细信息，请参阅[设备元数据创作向导](../devtest/device-metadata-authoring-wizard-portal.md)，此向导位于 [Windows 驱动程序工具包](../download-the-wdk.md)中。

4. 若要添加新程序包，请在“添加更多元数据”  下，浏览要添加的一个或多个文件、创建友好名称（如果需要），然后单击“提交”  。

    >[!NOTE]
    >你一共可以向体验中添加 50 个程序包。

## <a name="related-topics"></a>相关主题

- [创建设备元数据体验](create-a-device-metadata-experience.md)

- [提交批量元数据包](submit-a-bulk-metadata-package.md)

- [创建预览包](creating-a-preview-package.md)

- [提交设备元数据体验时的错误和解决方案](errors-and-solutions-when-submitting-device-metadata-experiences.md)

- [设备元数据业务规则](device-metadata-business-rules.md)