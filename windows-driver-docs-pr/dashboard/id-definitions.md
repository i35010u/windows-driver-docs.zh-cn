---
title: Windows 合作伙伴中心 ID 定义
description: Windows 合作伙伴中心 ID 定义
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71e176d4a0e6238885e1659df95b75c7d54fca60
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "63334980"
---
# <a name="dashboard-id-definitions"></a>仪表板 ID 定义

本主题定义与合作伙伴中心提交关联的标识号。

在 Windows 硬件开发人员中心内，每个驱动程序提交都必须与三个 ID 相关联：专用 ID、共享 ID 和提交 ID。 这三个 ID 之间的关系如下所示：

![显示三种 ID 类型的关系的屏幕截图](images/id_relationship.png)

合作伙伴中心在产品的驱动程序详细信息页上列出了上述每种 ID：

![显示三种 ID 类型的关系的屏幕截图](images/id_driver_details.png)

## <a name="id-definitions"></a>ID 定义

<table>
<thead>
<tr class="header">
<th>ID 名称</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>共享产品 ID</p></td>
<td><p>此标识符在有权访问驱动程序的所有帐户之间进行共享。 共享产品 ID 可让你轻松交流有关特定提交的信息并跟踪多个组织内的提交更新。 在大多数情况下，这是你希望跟踪并与他人共享的 ID。</p></td>
</tr>
<tr class="even">
<td><p>专用产品 ID</p></td>
<td><p>专用产品 ID 是在创建每个新产品时生成的顶级标识符。 此 ID 最常用于对特定产品进行个人参考并预测其 URL。
&gt; [!NOTE] &gt; 与其他人共享驱动程序时，将为他们分配一个新的专用产品 ID。 如果你想要交流有关产品的信息，请使用共享产品 ID。
</p>
</td>
</tr>
<tr class="odd">
<td><p>提交 ID</p></td>
<td><p>此标识符表示你上传到产品的各个程序包。 初始提交以及所有提交更新都具有唯一标识符。 此 ID 最常用于通过产品内的驱动程序更新可接受 (DUA) 进程跟踪更新。 请参阅<a href="https://msdn.microsoft.com/windows/hardware/drivers/dashboard/manage-your-hardware-submissions" data-raw-source="[Manage your hardware submissions](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/manage-your-hardware-submissions)">管理硬件提交</a>，了解更多详细信息。 </p></td>
</tr>
</tbody>
</table>

发货标签还包含两个其他 ID：

|ID 名称 | 描述|
|--- | ---|
|发货标签 ID | 此标识符用于内部跟踪，并分配给为产品分配的任何发货标签。 在大多数情况下，你不需要知道发货标签 ID。|
|推广请求 ID | 如果发货标签需要 Microsoft 进行手动审查，则将为其提供推广请求 ID。 它表示驱动程序发货室内的唯一发货标签。 你应在任何支持查询中包含此 ID。|

## <a name="related-topics"></a>相关主题

* [管理硬件提交](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/manage-your-hardware-submissions)

* [使用发货标签管理驱动程序分发](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/manage-driver-distribution-by-submission)
