---
Description: Device Representation
title: 设备表示法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72998e3834958bd22a71ab287fd549ee3808a930
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575354"
---
# <a name="device-representation"></a>设备表示法


设备已解决的 WPD 体系结构的两个主要行为：

-   访问和存储的内容。 例如，应用程序必须能够将音乐文件添加到便携式音乐播放机。
-   编程设备。 这包括简单操作，如更改设置和准备数据捕获或更复杂的操作，例如上传固件的设备。 例如，**拍照**命令可能会发出到数码照相机。

在 WPD，由作为对象的层次结构表示设备描述这些行为。 下图显示了多功能设备，在这种情况下，移动电话的 WPD 对象表示形式。

![wpd 层次结构](images/wpd_overview_figure3.png)

此层次结构演示了以下内容和功能。

## <a name="span-idfunctionalityspanspan-idfunctionalityspanspan-idfunctionalityspanfunctionality"></a><span id="Functionality"></span><span id="functionality"></span><span id="FUNCTIONALITY"></span>功能


-   存储对象。 此设备采用数据的存储。
-   与服务联系。 此服务是可用于同步和手机上存储联系人的功能对象。
-   SMS 服务。 此服务是可用于发送、 接收和存储短信的功能对象。

## <a name="span-idcontentsspanspan-idcontentsspanspan-idcontentsspancontents"></a><span id="Contents"></span><span id="contents"></span><span id="CONTENTS"></span>内容


-   媒体对象。 此设备将图像、 音乐和视频文件存储在存储对象上的文件夹中。 如上所示的文件存储在一个文件夹下，而设备可以细分到组织的存储 （如图像文件夹、 音乐文件夹或视频的文件夹） 的媒体类型的文件夹的内容。
-   联系人对象。 此设备将联系信息 （如名称、 电话号码、 地址等） 存储为联系人服务的子项。
-   消息对象。 此设备将 SMS （短消息服务） 的消息存储为短信服务的子项。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**WPD 驱动程序概述**](wpd-drivers-overview.md)

 

 





