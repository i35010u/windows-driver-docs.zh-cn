---
title: Iasphelp get \_ IsCluster 方法
description: 使用 IsCluster 属性，ASP 网页可以确定群集服务是否在群集节点上运行。
MS-HAID:
- webfnc\_96d39d88-6d6f-49af-93d7-0f6668af9564.xml
- print.iasphelp\_iscluster
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
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
ms.openlocfilehash: 93d5d8b1f77c889e34ce3adfcc576896fce6a6e1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796811"
---
# <a name="iasphelpget_iscluster-method"></a>Iasphelp：： get \_ IsCluster 方法

使用 **IsCluster** 属性，ASP 网页可以确定群集服务是否在群集节点上运行。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_IsCluster(
  [out] BOOL *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[弄\]  
调用方提供的指向内存位置的指针，该内存位置在节点上安装、配置和运行群集服务时接收 **TRUE** ; 否则为 **FALSE** 。

<a name="return-value"></a>返回值
------------

此属性始终返回 S \_ OK。

## <a name="vbscript-example"></a>VBScript 示例

此方法调用 **GetNodeClusterState** 函数来确定群集服务的状态。 有关此函数的详细信息，请参阅 Windows SDK 文档。

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
<td>台式机</td>
</tr>
</tbody>
</table>
