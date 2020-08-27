---
description: 设备表示法
title: 设备表示法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ae431b675ca53625881ed6f5fe26ed422ea47ec
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969592"
---
# <a name="device-representation"></a>设备表示法


设备具有两个主要的行为，这些行为由 WPD 体系结构解决：

-   访问和存储内容。 例如，应用程序必须能够将音乐文件添加到便携式音乐播放器。
-   设备编程。 这包括简单的操作，例如更改设置和为数据捕获准备设备，或执行更复杂的操作，如上传固件。 例如，可以向数字照相机发出 " **拍摄照片** " 命令。

在 WPD 中，这些行为通过将设备表示为对象的层次结构来进行描述。 下图显示了多功能设备（在本例中为移动电话）的 WPD 对象表示。

![wpd 层次结构](images/wpd_overview_figure3.png)

此层次结构演示以下功能和内容。

## <a name="span-idfunctionalityspanspan-idfunctionalityspanspan-idfunctionalityspanfunctionality"></a><span id="Functionality"></span><span id="functionality"></span><span id="FUNCTIONALITY"></span>性能


-   存储对象。 此设备具有数据存储。
-   联系人服务。 此服务是一种可用于在手机上同步和存储联系人的功能对象。
-   SMS 服务。 此服务是一个可用于发送、接收和存储 SMS 消息的功能对象。

## <a name="span-idcontentsspanspan-idcontentsspanspan-idcontentsspancontents"></a><span id="Contents"></span><span id="contents"></span><span id="CONTENTS"></span>目录


-   媒体对象。 此设备将图像、音乐和视频文件存储在存储对象上的文件夹中。 虽然上面显示的文件存储在一个文件夹中，但设备可将内容细分为按存储 (媒体类型（如图像文件夹、音乐文件夹或) 视频文件夹）组织的文件夹。
-   Contact 对象。 此设备将联系人信息 (如姓名、电话号码、地址等) 作为 Contacts 服务的子女。
-   消息对象。 此设备将 SMS (短消息服务作为 SMS 服务的子项存储) 消息。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**WPD 驱动程序概述**](wpd-drivers-overview.md)

 

 





