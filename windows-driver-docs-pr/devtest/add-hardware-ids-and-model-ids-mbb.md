---
title: 在移动宽带元数据创作向导中添加硬件 ID
description: 在移动宽带元数据创作向导中添加硬件 ID
ms.assetid: 1A540E7F-CA03-4CFA-8711-6CDBD7E152AD
keywords:
- 在移动宽带元数据创作向导中添加硬件 ID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93c9b02880d463efb4bc2d2843205c5d7bd75a65
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769417"
---
# <a name="add-hardware-ids-in-the-mobile-broadband-metadata-authoring-wizard"></a>在移动宽带元数据创作向导中添加硬件 ID

基于 IMSI 或 ICCID （GSM 网络运营商）、提供程序 SID 或提供程序名称（CDMA 网络操作员）指定元数据包适用的硬件 ID 范围。

向导将为你生成硬件 ID 值;不需要手动创建它们。

可以使用多个硬件 ID 来指定服务。 例如，可以为硬件 ID 输入 GSM 和 CDMA 条目来创建与多个网络匹配的单个元数据包。

## <a name="to-add-the-hardware-id"></a>添加硬件 ID

1. 单击 "**关联**" 选项卡。

2. 单击 "**硬件 ID**" 旁边的**加号（+）**。

3. 从 "**服务类型**" 旁边的列表中，选择下列选项之一：

    - 如果你有一个 MobileBroadbandMetadataSubmission 文件，则在**HardwareID**组下，单击 "**导入**"，然后选择 MobileBroadbandMetadataSubmission 文件。 该工具基于 MobileBroadbandMetadataSubmission 文件生成硬件 ID，硬件 Id 显示在**HardwareID**组中。

      如果要使用 SIM 上的 IMSI 值匹配包，请选择 " **GSM 提供程序（IMSI）**"。

      GSM 网络操作员应指定要应用设备元数据包的 IMSI 范围。

      - 在 "**提供程序 ID** " 字段中输入串连的 MCC 和 MNC。

        > [!NOTE]
        > 这适用于6位和5位 MCC + MNC 组合。

      - 在 "**范围**" 字段中输入完整的 IMSI （MCC + MNC + MSIN） Begin 值和结束值。

      > [!NOTE]
      > 为了保护用户隐私，出于匹配目的，将忽略 IMSI 的最后两个数字。 完全 IMSI 永远不会发送到服务器以进行匹配。 在甚至100块中指定 IMSI 范围。 开始值必须以00结束，并且结束值必须以99结束。

      - 下一页显示与你的范围相对应的生成的**硬件 ID**值。 列表中可能会出现几个**硬件 ID**值。 确保选中所有这些选项，然后单击 "**下一步**"。

        可以通过单击 "**关联**" 选项卡上 "**硬件 ID** " 下的**加号（+）** 按钮来添加更多范围。可以在同一包提交中添加 IMSI 范围以及 ICCID 范围。

    - 若要指定 ICCID 范围，请选择 " **GSM 提供程序（ICCID）**"。

      GSM 网络运营商可以使用 ICCID 范围来匹配其服务元数据包。

      - 在 "**提供程序 ID** " 字段中，输入 ICCID sim 报告的编号的颁发者标识号。 这是包含 "89" 前缀的6或7位数字。
  
      - 在 "**范围**" 字段中输入完整 ICCID （包括 "89" 前缀） Begin 值和结束值。

    > [!NOTE]
    > 为了帮助保护用户隐私，将忽略 ICCID 的最后两个数字，并且永远不会将完全 ICCID 发送到服务器以进行匹配。 在甚至100块中指定 ICCID 范围。 开始值必须以00结束，并且结束值必须以99结束。

      - 下一页显示与你的范围相对应的生成的**硬件 ID**值。 列表中可能会出现几个**硬件 ID**值。 确保选中所有这些选项，然后单击 "**下一步**"。

      - 可以通过单击 "**关联**" 选项卡上 "**硬件 ID** " 下的**加号（+）** 按钮来添加更多范围。可以将 IMSI 范围以及 ICCID 范围添加到相同的包提交中。

- 如果要使用移动宽带调制解调器上的 "提供程序 ID" 值进行匹配，请选择 " **CDMA 提供程序 id**"。
  
  > [!NOTE]
  > 建议使用**提供程序 ID** （SID），因为**提供程序名称**是一个文本值，并且容易因拼写变体而发生匹配错误。 有关详细信息，请参阅[WWAN \_ 注册 \_ 状态结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_registration_state)。

  - 输入 "**提供程序 ID**"，它是通过3GPP2 分配给操作员的系统标识号（SID）。
  
      > [!NOTE]
      > 通过单击 "**关联**" 选项卡上的**加号（+）** 按钮，可以添加多个**提供程序 ID**值。您可以添加**提供程序 ID**和**提供程序名称**值的组合，以便进行匹配。

  - 你指定的每个**提供程序 ID**值在 "**关联**" 选项卡上显示为特殊格式的硬件 ID 条目。 请确保已选中每个复选框，并在完成输入提供程序 Id 后单击 "**下一步**"。

- 如果要使用移动宽带调制解调器上的访问接口名称进行匹配，请选择 " **CDMA 提供程序名称**"，或选择 "提供程序 ID"。

  > [!NOTE]
  > 如果提供给客户的所有移动宽带硬件都使用提供程序 ID 值，则不需要在设备元数据包中添加**提供程序名称**信息。 仅当提供程序 ID 为空或值为零时，才会检查**提供程序名称**是否匹配。 有关详细信息，请参阅[WWAN \_ 注册 \_ 状态结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_registration_state)。

  - 输入**提供程序名称**。 此区分大小写的值用于生成硬件 Id。 如果你具有以各种方式表示**提供程序名称**的移动宽带硬件，请分别输入每个变体，以考虑操作员名称的所有大写和拼写组合。

  - 你指定的每个**提供程序名称**值在 "**关联**" 选项卡中显示为特殊格式的硬件 ID 条目。 确保选中每个复选框，并在完成输入提供程序名称后单击 "**下一步**"。

4. 单击 **"确定"** 以返回到 "**关联**" 选项卡。

有关每种服务样式的硬件 ID 的详细信息，请参阅[Windows 8 的服务元数据包架构参考](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/service-metadata-package-schema-reference)。

有关匹配的详细信息，请参阅[提供 mvno 体验](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/delivering-experiences-for-mvnos)。
