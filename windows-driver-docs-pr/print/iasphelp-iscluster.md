---
title: Iasphelp get\_IsCluster 方法
description: IsCluster 属性启用 ASP 网页，以确定是否正在群集节点上运行的群集服务。
MS-HAID:
- webfnc\_96d39d88-6d6f-49af-93d7-0f6668af9564.xml
- print.iasphelp\_iscluster
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 78573fe7-d264-4d3c-8654-a85c2abfb93a
keywords:
- get_IsCluster 方法打印设备
- get_IsCluster 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_IsCluster 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_IsCluster
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12413c461bc41762f30f7fb91edc9e568946ef1c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523421"
---
# <a name="iasphelpgetiscluster-method"></a>Iasphelp::get\_IsCluster 方法

**IsCluster**属性启用 ASP 网页，以确定是否正在群集节点上运行的群集服务。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_IsCluster(
  [out] BOOL *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[out\]  
指向接收的内存位置的调用方提供指针 **，则返回 TRUE**群集服务是否已安装、 配置和运行的节点上，并**FALSE**否则为。

<a name="return-value"></a>返回值
------------

此属性始终返回 S\_确定。

## <a name="vbscript-example"></a>VBScript 示例

此方法调用**GetNodeClusterState**函数来确定群集服务的状态。 有关此函数的详细信息，请参阅 Windows SDK 文档。

```vb
Dim objPrinter, ClusterRunning
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
ClusterRunning = objPrinter.IsCluster
```

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>目标平台</p></td>
<td>桌面设备</td>
</tr>
</tbody>
</table>
