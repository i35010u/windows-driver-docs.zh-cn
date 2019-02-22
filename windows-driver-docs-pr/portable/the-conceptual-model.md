---
Description: The Conceptual Model
title: 概念模型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8340e69edaf2b0b20492ff470ca2db6608723204
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534846"
---
# <a name="the-conceptual-model"></a>概念模型


WPD 概念模型介绍根据对象、 属性和资源的设备。 以下主题介绍这些元素。

## <a name="span-idobjectsspanspan-idobjectsspanspan-idobjectsspanobjects"></a><span id="Objects"></span><span id="objects"></span><span id="OBJECTS"></span>Objects


WPD，在设备上的逻辑实体都称为对象。 通常情况下，但并非总是，这些表示设备上的数据。 对象具有属性，并引用的对象标识符。 对象的示例包括图片和照相机、 歌曲和媒体播放器，联系人在移动电话上的播放列表上的文件夹，依次类推。

对象还可以表示设备的功能或信息性的部分。 其中的示例包括播放器控件 （播放/记录/暂停）、 相机设置、 移动电话的短消息服务 (SMS) 功能，等等。 对象还可以作为资源存储的二进制数据。

## <a name="span-idpropertiesspanspan-idpropertiesspanspan-idpropertiesspanproperties"></a><span id="Properties"></span><span id="properties"></span><span id="PROPERTIES"></span>属性


对象属性提供了一种机制，用来描述对象的元数据交换。 例如，图像对象可能包括描述其文件名、 大小、 格式、 宽度以像素为单位，等的属性。

属性具有当前值，以及属性。 WPD 定义一组构成的 API 和 DDI 定义的标准属性。 供应商并不局限于预定义的 WPD 属性和随意添加其自己。

## <a name="span-idpropertyattributesspanspan-idpropertyattributesspanspan-idpropertyattributesspanproperty-attributes"></a><span id="Property_Attributes"></span><span id="property_attributes"></span><span id="PROPERTY_ATTRIBUTES"></span>属性特性


属性特性描述的访问权限、 有效的值和与属性相关的其他信息。 例如，属性表示比特率可能是一个范围从 8 千位 / 秒 (Kbps) 为 20 Kbps 步骤值为 1 Kbps。

访问权限指示是否调用方可以读取、 写入和/或删除该属性。 有效的值指示属性值的限制。 有效的值被称为特定窗体。 有效的值的窗体包括范围 （即，属性可能需要一个值距离最小值到最大值与指定的步骤），枚举 （也就是说，属性值为指定列表中的某个），未使用任何 （即，某个文件夹下有任何有效的特定值）。

## <a name="span-idresourcesspanspan-idresourcesspanspan-idresourcesspanresources"></a><span id="Resources"></span><span id="resources"></span><span id="RESOURCES"></span>资源


资源都是二进制数据的占位符。 对象可以有多个资源。 例如，如果该对象表示与音频批注的图像文件，则此对象的资源可能是，如下所示：

-   默认的资源。 此资源表示整个图像文件。 （这包括任何嵌入的数据批注音频、 缩略图，等）
-   缩略图的资源。 此资源表示的图像的缩略图的数据。
-   一种音频批注资源。 此资源表示与图像关联的音频数据。

## <a name="span-idresourceattributesspanspan-idresourceattributesspanspan-idresourceattributesspanresource-attributes"></a><span id="Resource_Attributes"></span><span id="resource_attributes"></span><span id="RESOURCE_ATTRIBUTES"></span>资源属性


类似于属性的特性，资源属性描述的访问权限、 大小、 格式和与资源相关的其他信息。 例如，图像对象上的音频批注资源的属性可以指定的比特率、 通道计数和的音频数据格式。

## <a name="span-idobjectillustrationspanspan-idobjectillustrationspanspan-idobjectillustrationspanobject-illustration"></a><span id="Object_Illustration"></span><span id="object_illustration"></span><span id="OBJECT_ILLUSTRATION"></span>对象图


下图显示了一个对象，其属性和其资源，例如使用的图像对象之间的关系。

![wpd 对象](images/wpd_overview_figure2.png)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[**WPD 驱动程序概述**](wpd-drivers-overview.md)

 

 





