---
title: 更换器驱动程序模型
description: 更换器驱动程序模型
ms.assetid: 87a70ecf-e518-4c22-945b-9056b59fed5a
keywords:
- 更换器驱动程序 WDK 存储，体系结构
- 存储更换器驱动程序 WDK、体系结构
- 传输元素 WDK 转换器
- 数据传输元素 WDK 转换器
- 存储元素 WDK 转换器
- IEport WDK 转换器
- 导入/导出元素 WDK 转换器
- 门板转换器
- 可移动存储管理器 WDK 转换器
- RSM WDK 转换器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 560fa3832877fd625f411ff4b2b2380648377529
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189211"
---
# <a name="the-changer-driver-model"></a>更换器驱动程序模型


## <span id="ddk_the_changer_driver_model_kg"></span><span id="DDK_THE_CHANGER_DRIVER_MODEL_KG"></span>


下图显示了更换器驱动程序、用户模式应用程序和服务、大容量存储和端口驱动程序和转换器设备之间的关系。

![说明更换器驱动程序、用户模式应用程序和服务、大容量存储和端口驱动程序以及更换器设备之间的关系的关系图](images/changer.png)

变换器驱动程序模型

如上图所示，用户数据的传输由更换器驱动器的合适大容量存储驱动程序处理，并使用与独立驱动器相同的 Microsoft Win32 请求。 但是，大容量存储驱动程序必须处理 [**IOCTL \_ 存储 \_ 获取 \_ 媒体 \_ 类型（ \_ 例如**](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_get_media_types_ex) i/o 请求），才能控制更换器的驱动器。

用户模式应用程序通过名为可移动存储管理器 (RSM) 的用户模式服务访问转换器的元素。 RSM 是更换器驱动程序的唯一客户端，它保留用于独占使用的转换器。 RSM 发送涉及更换器元素的请求 (例如，将驱动器中的一片介质装载) 到更换器驱动程序。 用户模式应用程序不能直接将请求发送到更换器驱动程序。 有关 RSM 的详细信息，请参阅 Microsoft Windows SDK 文档。

转换器的元素包括：

-   *Transport 元素*

    在转换器中的其他元素之间移动媒体的机器人组件。 大多数更换器都有一个传输元素，其中包含一个或两个选取器，其中包含要移动的介质。 高端、容错转换器可能有多个传输元素。

-   *数据传输元素*

    从中读取和写入数据的驱动器。 例如，磁或光盘、磁带、cd-rom 或 DVD。 通常，变换器仅包含一种驱动器。

-   *存储元素*

    未装入驱动器时存储媒体的槽。

变换器还可以有一个或两个以下元素：

-   *导入/导出* (IEport) 

    一个元素，在该元素中，运算符可以在变换器中插入或删除一个或多个（但不是全部）媒体。

-   *Door*

    提供对变换器中所有介质的访问一次。 变换器的门可以是一个操作员打开的物理门，也可以是包含所有介质的单个磁带箱。

转换器 miniclass 驱动程序在由变换器类驱动程序请求时 [**，将报告转换器 \_ \_ **](/windows-hardware/drivers/ddi/ntddchgr/ns-ntddchgr-_get_changer_parameters) 的元素的类型和数目。 具体而言，miniclass 驱动程序必须根据这些定义报告 IEports 和门，而不考虑元素的物理外观，以便应用程序可以向这些元素发出适当的请求。

 

