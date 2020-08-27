---
description: 概念模型
title: 概念模型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c834f1233083c8bda00798ceda42ffe9b65c599a
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968700"
---
# <a name="the-conceptual-model"></a>概念模型


WPD 概念模型根据对象、属性和资源对设备进行了说明。 以下主题描述了这些元素。

## <a name="span-idobjectsspanspan-idobjectsspanspan-idobjectsspanobjects"></a><span id="Objects"></span><span id="objects"></span><span id="OBJECTS"></span>对象


在 WPD 中，设备上的逻辑实体称为对象。 通常（但不总是）表示设备上的数据。 对象具有属性，并且由对象标识符引用。 对象的示例包括相机上的图片和文件夹、media player 上的歌曲和播放列表、移动电话上的联系人等。

对象也可以表示设备的功能或信息性部分。 这些示例包括播放机控件 (播放/录制/暂停) 、照相机设置、移动电话短信服务 (SMS) 功能等。 对象还可以具有作为资源存储的二进制数据。

## <a name="span-idpropertiesspanspan-idpropertiesspanspan-idpropertiesspanproperties"></a><span id="Properties"></span><span id="properties"></span><span id="PROPERTIES"></span>属性


对象属性提供了一种用于交换对象描述元数据的机制。 例如，image 对象可能包含描述其文件名、大小、格式、宽度（以像素为单位）的属性。

属性具有当前值以及属性。 WPD 定义一组标准属性，这些属性构成 API 和 DDI 定义。 供应商不仅限于预定义的 WPD 属性，还可以自由地添加它们自己的属性。

## <a name="span-idproperty_attributesspanspan-idproperty_attributesspanspan-idproperty_attributesspanproperty-attributes"></a><span id="Property_Attributes"></span><span id="property_attributes"></span><span id="PROPERTY_ATTRIBUTES"></span>属性特性


属性特性描述访问权限、有效值以及与属性相关的其他信息。 例如，表示比特率的属性可以为每秒8千字节 (Kbps) 到 20 Kbps，步长值为 1 Kbps。

访问权限指示调用方是否可以读取、写入和/或删除该属性。 有效值表示对属性值的限制。 有效值称为特定形式。 有效值窗体包括范围 (即，属性可以采用指定步骤) 的最小值和最大值，枚举 (也就是说，属性值是指定列表) 中的一个值，而不是 (的任何特定有效值。

## <a name="span-idresourcesspanspan-idresourcesspanspan-idresourcesspanresources"></a><span id="Resources"></span><span id="resources"></span><span id="RESOURCES"></span>中心


资源是用于二进制数据的占位符。 一个对象可以具有多个资源。 例如，如果对象表示带有音频批注的图像文件，则此对象的资源如下所示：

-   默认资源。 此资源表示整个映像文件。  (包括任何嵌入数据，如音频批注、缩略图等) 
-   缩略图资源。 此资源表示图像的缩略图数据。
-   音频批注资源。 此资源表示与图像关联的音频数据。

## <a name="span-idresource_attributesspanspan-idresource_attributesspanspan-idresource_attributesspanresource-attributes"></a><span id="Resource_Attributes"></span><span id="resource_attributes"></span><span id="RESOURCE_ATTRIBUTES"></span>资源属性


与属性属性类似，资源属性描述访问权限、大小、格式以及与资源相关的其他信息。 例如，图像对象上音频批注资源的属性可以指定音频的比特率、通道计数和数据格式。

## <a name="span-idobject_illustrationspanspan-idobject_illustrationspanspan-idobject_illustrationspanobject-illustration"></a><span id="Object_Illustration"></span><span id="object_illustration"></span><span id="OBJECT_ILLUSTRATION"></span>对象插图


下图显示了对象、其属性和资源的资源之间的关系，并使用 Image 对象作为示例。

![wpd 对象](images/wpd_overview_figure2.png)

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**WPD 驱动程序概述**](wpd-drivers-overview.md)

 

 





