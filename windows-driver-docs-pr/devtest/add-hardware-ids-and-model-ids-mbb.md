---
title: 在移动宽带元数据创作向导中添加硬件 ID
description: 在移动宽带元数据创作向导中添加硬件 ID
ms.assetid: 1A540E7F-CA03-4CFA-8711-6CDBD7E152AD
keywords:
- 在移动宽带元数据创作向导中添加硬件 ID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c3d89980809aedc4d280e73e1321f266a1e26f2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332066"
---
# <a name="add-hardware-ids-in-the-mobile-broadband-metadata-authoring-wizard"></a>在移动宽带元数据创作向导中添加硬件 ID

指定的元数据的包适用于基于 IMSI 或 ICCID （GSM 网络运营商）、 提供程序的 SID 或提供程序名称 （CDMA 网络运营商） 的硬件 ID 范围。

向导将为您; 生成的硬件 ID 值不用手动创建它们。

可以使用多个硬件 ID 来指定的服务。 例如，您可以输入要创建单个元包匹配多个网络的硬件 ID 的 GSM 和 CDMA 条目。

## <a name="to-add-the-hardware-id"></a>若要添加的硬件 ID

1. 单击**关联**选项卡。

2. 下一步**硬件 ID**，单击**加号 （+）**。

3. 从列表中下一步**服务类型**，选择以下选项之一：

    - 如果在具有 MobileBroadbandMetadataSubmission.xml 文件， **HardwareID**组中，单击**导入**，然后选择 MobileBroadbandMetadataSubmission.xml 文件。 该工具生成基于 MobileBroadbandMetadataSubmission.xml 文件，则硬件 ID 和硬件 Id 将显示在**HardwareID**组。

      如果你想要在 SIM 中，选择上使用 IMSI 值匹配您的软件包**GSM 提供程序 (IMSI)**。

      GSM 网络运营商应指定他们想要应用于的设备元数据包的 IMSI 范围。

      - 输入连接的 MCC 和 mnc 中的是否**提供程序 ID**字段。

        > [!NOTE]
        > 这适用于 6 位数字和 5 位数字的 MCC + mnc 组合。

      - 输入完整 IMSI （MCC + mnc 是否 + MSIN） 开始值和结束值中的**范围**字段。

      > [!NOTE]
      > 若要保护用户隐私，用于匹配目的忽略 IMSI 最后两位数字。 用于匹配目的，完整 IMSI 永远不会发送到服务器。 在 100 个甚至块中指定 IMSI 范围。 开始值必须以 00，结束，99 结尾的结束值。

      - 下一步页显示了生成**硬件 ID**对应于范围的值。 多个**硬件 ID**可能会出现在列表中的值。 请确保所有这些选择，然后依次**下一步**。

        可以通过单击添加更多范围**加号 （+）** 按钮下**硬件 ID**上**关联**选项卡。您可以添加 IMSI 范围，以及中相同的包提交的 ICCID 范围。

    - 若要指定 ICCID 范围，请选择**GSM 提供程序 (ICCID)**。

      GSM 网络运营商可以使用 ICCID 范围来匹配其服务元数据包。

      - 在中**提供程序 ID**字段中，输入开始报告 Sim ICCID 号颁发者标识号。 这就是 6-7-包括"89"前缀的位数字或。
  
      - 输入完整的 ICCID （包括"89"前缀） 开始值和结束值中的**范围**字段。

    > [!NOTE]
    > 为了帮助保护用户隐私，ICCID 最后两位数字将被忽略并完整 ICCID 永远不会用于匹配目的发送到服务器。 在 100 个甚至块中指定 ICCID 范围。 开始值必须以 00，结束，99 结尾的结束值。

      - 下一步页显示了生成**硬件 ID**对应于范围的值。 多个**硬件 ID**可能会出现在列表中的值。 请确保所有这些选择，然后依次**下一步**。

      - 可以通过单击添加更多范围**加号 （+）** 按钮下**硬件 ID**上**关联**选项卡。您可以添加 IMSI 范围，以及 ICCID 范围，在同一个包提交到。

- 如果你想要使用的移动宽带调制解调器上，选择的提供程序 ID 值的匹配**CDMA 提供程序 ID**。
  
  > [!NOTE]
  > 我们建议使用**提供程序 ID** (SID)，因为**提供程序名称**是文本值和易受匹配拼写变体导致的错误。 有关详细信息，请参阅[WWAN\_注册\_状态结构](https://go.microsoft.com/fwlink/p/?linkid=225972)。

  - 输入**提供程序 ID**，这是系统标识号 (SID) 由 3GPP2 向操作员分配。
  
      > [!NOTE]
      > 可以添加多个**提供程序 ID**通过单击值**加号 （+）** 按钮**关联**选项卡。可以添加的组合**提供程序 ID**并**提供程序名称**用于匹配目的的值。

  - 每个**提供程序 ID**指定的值的显示**关联**为特殊格式的硬件 ID 条目的选项卡。 请确保选择每个复选框，然后单击**下一步**完输入提供程序 Id。

- 如果你想要通过使用移动宽带调制解调器上，选择提供程序名称匹配**CDMA 提供程序名称**除了或而不是一个提供程序 id。

  > [!NOTE]
  > 如果你向客户提供的移动宽带硬件的所有使用提供程序 ID 值，无需添加**提供程序名称**中你的设备元数据包的信息。 **提供程序名称**才检查用于匹配目的，如果提供程序 ID 为空，或者值为零。 有关详细信息，请参阅[WWAN\_注册\_状态结构](https://go.microsoft.com/fwlink/p/?linkid=225972)。

  - 输入**提供程序名称**。 此区分大小写的值用于生成硬件 Id。 如果必须表示的移动宽带硬件**提供程序名称**以各种方式，每个变体单独输入，考虑所有大小写和拼写的操作员的名称的组合。

  - 每个**提供程序名称**指定的值将出现在**关联**为特殊格式的硬件 ID 条目的选项卡。 请确保选择了每个复选框，然后单击**下一步**在完成输入的提供程序名称。

4. 单击**确定**回到**关联**选项卡。

有关每个服务样式硬件 ID 的详细信息，请参阅[服务的元数据包架构引用适用于 Windows 8 的](https://msdn.microsoft.com/library/windows/hardware/dn973175)。

有关匹配的详细信息，请参阅[交付体验来 Mvno](https://msdn.microsoft.com/library/windows/hardware/dn973075)。
