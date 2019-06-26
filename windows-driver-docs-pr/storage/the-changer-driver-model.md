---
title: 更换器驱动程序模型
description: 更换器驱动程序模型
ms.assetid: 87a70ecf-e518-4c22-945b-9056b59fed5a
keywords:
- 更换器驱动程序 WDK 存储体系结构
- 存储更换器驱动程序 WDK，体系结构
- 传输元素 WDK 换带机
- 数据传输元素 WDK 换带机
- 存储元素 WDK 换带机
- IEport WDK 换带机
- 导入/导出元素 WDK 换带机
- 门 WDK 换带机
- 可移动存储管理器 WDK 换带机
- RSM WDK 换带机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b004ccdd87364e72805034e2df73b25ea450162
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386813"
---
# <a name="the-changer-driver-model"></a>更换器驱动程序模型


## <span id="ddk_the_changer_driver_model_kg"></span><span id="DDK_THE_CHANGER_DRIVER_MODEL_KG"></span>


下图显示了更换器驱动程序、 用户模式应用程序和服务、 大容量存储和端口驱动程序和换带机设备之间的关系。

![说明更换器驱动程序、 用户模式应用程序和服务、 大容量存储和端口驱动程序和换带机设备之间的关系的关系图](images/changer.png)

更换器驱动程序模型

此图中所示，传输的用户数据都由处理换带机的驱动器的合适大容量存储驱动程序使用相同 Microsoft Win32 请求与独立驱动器。 但是，大容量存储驱动程序必须处理[ **IOCTL\_存储\_获取\_媒体\_类型\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_get_media_types_ex)以便 I/O 请求控制换带机的驱动器。

通过用户模式服务的用户模式应用程序访问转换器元素调用的可移动存储管理器 (RSM)。 RSM 是更换器驱动程序的唯一客户端，它包含着换带机供独占使用。 RSM 发送请求涉及到更换器驱动程序 （例如，若要装载的驱动器中的介质） 的转换器的元素。 用户模式应用程序不能直接向更换器驱动程序发送请求。 RSM 的详细信息，请参阅 Microsoft Windows SDK 文档。

换带机中的元素包括：

-   *传输元素*

    换带机中的其他元素之间移动媒体机器人组件。 大多数更换器保存要移动的介质的一个或两个选取器中具有一个传输元素。 高端、 容错的转换器可能具有多个传输元素。

-   *数据传输元素*

    从中读取和写入媒体数据驱动器。 例如，磁性介质或光学磁盘、 磁带、 CD-ROM 或 DVD。 通常情况下，换带机包含仅一种类型的驱动器。

-   *存储元素*

    当未在驱动器中装入媒体存储槽。

转换器可能还有一个或两个以下元素：

-   *导入/导出*(IEport)

    操作员可以插入其中的元素或删除一个或多个，但不是所有，换带机中的媒体。

-   *Door*

    提供了一次在换带机中的所有媒体访问权限。 转换器的门可以是物理门，此时会打开一个运算符，或单个杂志，它持有所有媒体。

换带机 miniclass 驱动程序报告的类型和换带机中的元素数目[**获取\_转换器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddchgr/ns-ntddchgr-_get_changer_parameters)结构转换器类驱动程序的请求。 具体而言，miniclass 驱动程序必须报告 ie 端口和门根据这些定义，而不考虑元素的外观，以便应用程序可以向这些元素发出相应的请求。

 

 




